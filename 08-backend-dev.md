<div align="center">

# ⚙️ Chapter 08 · Backend Dev

### APIs · Authentication · Node.js / Django

![Backend Development](https://media.giphy.com/media/l3vRfNA1p0rvhMSvS/giphy.gif)

> *"Frontend is what users see. Backend is what makes it work."*

[🔙 Back to Chapter 07](./07-data-management.md)

</div>

---

## 🎭 Frontend vs Backend

Every web application has two sides:

| 🎨 Frontend | ⚙️ Backend |
|-------------|-----------|
| What users see | What users don't see |
| UI/UX | Business logic |
| HTML, CSS, JavaScript | Server-side code |
| Runs in browser | Runs on server |
| Client-side | Server-side |

### 🧠 Mental Model

```
User → Frontend → API → Backend → Database
        (React)    (REST)  (Node.js)  (PostgreSQL)
```

Think of it like a restaurant:
- **Frontend** = Dining room (what customers experience)
- **Backend** = Kitchen (where the real work happens)
- **API** = Waiter (connects both sides)

---

## 🌐 Part 1 · APIs (Application Programming Interfaces)

### *The Bridge Between Systems*

An **API** is a way for different software to talk to each other.

**Without APIs:**
- ❌ Every app would need its own data
- ❌ No integration between services
- ❌ Frontend and backend couldn't communicate

### 🔗 REST APIs

**REST** (Representational State Transfer) is the most common API style.

#### Key Concepts:

| Concept | Description |
|---------|-------------|
| **Endpoint** | A specific URL that performs an action |
| **HTTP Method** | The type of action (GET, POST, etc.) |
| **Request** | Data sent to the server |
| **Response** | Data returned from the server |
| **Status Code** | Result of the request (200, 404, etc.) |

### 📋 HTTP Methods (CRUD Mapping)

| Method | Purpose | SQL Equivalent | Example |
|--------|---------|----------------|---------|
| **GET** | Retrieve data | SELECT | Get list of users |
| **POST** | Create new data | INSERT | Create new user |
| **PUT/PATCH** | Update data | UPDATE | Modify user info |
| **DELETE** | Remove data | DELETE | Delete user |

### 🎯 API Endpoint Examples

```
GET    /api/users           → Get all users
GET    /api/users/123       → Get user with ID 123
POST   /api/users           → Create new user
PUT    /api/users/123       → Update user 123
DELETE /api/users/123       → Delete user 123

GET    /api/posts?author=5  → Get posts by author 5
POST   /api/posts           → Create new post
```

### 📊 HTTP Status Codes

| Code | Meaning | When to Use |
|------|---------|-------------|
| **200** | OK | Successful request |
| **201** | Created | Successfully created resource |
| **400** | Bad Request | Invalid input |
| **401** | Unauthorized | Not authenticated |
| **403** | Forbidden | Not authorized |
| **404** | Not Found | Resource doesn't exist |
| **500** | Server Error | Something broke on server |

### 🔄 Request/Response Flow

```json
// REQUEST
POST /api/users
Content-Type: application/json

{
  "name": "Alice",
  "email": "alice@email.com",
  "age": 28
}

// RESPONSE
HTTP/1.1 201 Created
Content-Type: application/json

{
  "id": 123,
  "name": "Alice",
  "email": "alice@email.com",
  "age": 28,
  "created_at": "2026-01-11T10:30:00Z"
}
```

---

## 🔐 Part 2 · Authentication & Authorization

### *Who Are You? What Can You Do?*

**Authentication** = Verifying identity (who you are)  
**Authorization** = Verifying permissions (what you can do)

### 🎯 Authentication Methods

#### 1. Session-Based Auth (Traditional)

```
1. User logs in with credentials
2. Server creates a session
3. Server sends session ID as cookie
4. Client sends cookie with each request
5. Server validates session ID
```

**Pros:** Simple, secure, easy to invalidate  
**Cons:** Doesn't scale well, requires server storage

#### 2. Token-Based Auth (Modern)

**JWT (JSON Web Tokens)** - Most popular approach

```
1. User logs in with credentials
2. Server generates JWT token
3. Client stores token (localStorage/cookie)
4. Client sends token in headers
5. Server verifies token signature
```

**Token Structure:**
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJ1c2VySWQiOjEyMywiZW1haWwiOiJhbGljZUBlbWFpbC5jb20ifQ.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

Header.Payload.Signature
```

**Pros:** Stateless, scalable, works across domains  
**Cons:** Can't invalidate easily, larger than session ID

#### 3. OAuth 2.0 (Third-Party)

**"Login with Google/GitHub/Facebook"**

```
1. User clicks "Login with Google"
2. Redirected to Google
3. User approves access
4. Google sends authorization code
5. Your server exchanges code for access token
6. You can now access user's Google data
```

### 🔒 Password Security

```javascript
// ❌ NEVER store plain passwords
user.password = "password123";

// ✅ Always hash passwords
const bcrypt = require('bcrypt');
const hashedPassword = await bcrypt.hash(password, 10);

// ✅ Verify password
const isValid = await bcrypt.compare(inputPassword, hashedPassword);
```

### 🛡️ Securing APIs

```javascript
// Require authentication for protected routes
app.get('/api/profile', authenticateToken, (req, res) => {
  res.json(req.user);
});

// Verify JWT token
function authenticateToken(req, res, next) {
  const token = req.headers['authorization']?.split(' ')[1];
  
  if (!token) {
    return res.status(401).json({ error: 'Access denied' });
  }
  
  jwt.verify(token, SECRET_KEY, (err, user) => {
    if (err) {
      return res.status(403).json({ error: 'Invalid token' });
    }
    req.user = user;
    next();
  });
}
```

---

## 🟢 Part 3 · Node.js & Express

### *JavaScript on the Server*

**Node.js** lets you run JavaScript outside the browser.  
**Express** is the most popular Node.js framework for building APIs.

### 🚀 Basic Express Server

```javascript
const express = require('express');
const app = express();
const PORT = 3000;

// Middleware to parse JSON
app.use(express.json());

// Basic route
app.get('/', (req, res) => {
  res.json({ message: 'Hello, World!' });
});

// Start server
app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
```

### 📋 Complete CRUD API Example

```javascript
const express = require('express');
const app = express();

app.use(express.json());

// In-memory database (for demo)
let users = [
  { id: 1, name: 'Alice', email: 'alice@email.com' },
  { id: 2, name: 'Bob', email: 'bob@email.com' }
];

// CREATE - Add new user
app.post('/api/users', (req, res) => {
  const newUser = {
    id: users.length + 1,
    name: req.body.name,
    email: req.body.email
  };
  users.push(newUser);
  res.status(201).json(newUser);
});

// READ - Get all users
app.get('/api/users', (req, res) => {
  res.json(users);
});

// READ - Get single user
app.get('/api/users/:id', (req, res) => {
  const user = users.find(u => u.id === parseInt(req.params.id));
  if (!user) {
    return res.status(404).json({ error: 'User not found' });
  }
  res.json(user);
});

// UPDATE - Modify user
app.put('/api/users/:id', (req, res) => {
  const user = users.find(u => u.id === parseInt(req.params.id));
  if (!user) {
    return res.status(404).json({ error: 'User not found' });
  }
  user.name = req.body.name || user.name;
  user.email = req.body.email || user.email;
  res.json(user);
});

// DELETE - Remove user
app.delete('/api/users/:id', (req, res) => {
  const index = users.findIndex(u => u.id === parseInt(req.params.id));
  if (index === -1) {
    return res.status(404).json({ error: 'User not found' });
  }
  users.splice(index, 1);
  res.status(204).send();
});

app.listen(3000, () => {
  console.log('API running on http://localhost:3000');
});
```

### 🔧 Essential Express Middleware

```javascript
const cors = require('cors');
const helmet = require('helmet');
const morgan = require('morgan');

// Security headers
app.use(helmet());

// Enable CORS (allow frontend to call API)
app.use(cors());

// Logging
app.use(morgan('dev'));

// Parse JSON bodies
app.use(express.json());

// Error handling
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Something went wrong!' });
});
```

---

## 🐍 Part 4 · Django & Python

### *Batteries Included Framework*

**Django** is a full-featured Python framework for building web applications.

### 🚀 Django Project Structure

```
myproject/
├── manage.py
├── myproject/
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── myapp/
    ├── models.py      # Database models
    ├── views.py       # Request handlers
    ├── urls.py        # Route definitions
    ├── serializers.py # API serialization
    └── admin.py       # Admin interface
```

### 📋 Django Models (ORM)

```python
from django.db import models

class User(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField(unique=True)
    age = models.IntegerField()
    created_at = models.DateTimeField(auto_now_add=True)
    
    def __str__(self):
        return self.name

class Post(models.Model):
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    title = models.CharField(max_length=200)
    content = models.TextField()
    published_at = models.DateTimeField(auto_now_add=True)
```

### 🔧 Django REST Framework API

```python
from rest_framework import viewsets
from rest_framework.decorators import api_view
from rest_framework.response import Response
from .models import User
from .serializers import UserSerializer

# ViewSet approach (automatic CRUD)
class UserViewSet(viewsets.ModelViewSet):
    queryset = User.objects.all()
    serializer_class = UserSerializer

# Function-based views
@api_view(['GET', 'POST'])
def user_list(request):
    if request.method == 'GET':
        users = User.objects.all()
        serializer = UserSerializer(users, many=True)
        return Response(serializer.data)
    
    elif request.method == 'POST':
        serializer = UserSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=201)
        return Response(serializer.errors, status=400)

@api_view(['GET', 'PUT', 'DELETE'])
def user_detail(request, pk):
    try:
        user = User.objects.get(pk=pk)
    except User.DoesNotExist:
        return Response(status=404)
    
    if request.method == 'GET':
        serializer = UserSerializer(user)
        return Response(serializer.data)
    
    elif request.method == 'PUT':
        serializer = UserSerializer(user, data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=400)
    
    elif request.method == 'DELETE':
        user.delete()
        return Response(status=204)
```

### 🔐 Django Authentication

```python
from rest_framework.decorators import api_view, permission_classes
from rest_framework.permissions import IsAuthenticated
from django.contrib.auth import authenticate
from rest_framework_simplejwt.tokens import RefreshToken

@api_view(['POST'])
def login(request):
    username = request.data.get('username')
    password = request.data.get('password')
    
    user = authenticate(username=username, password=password)
    if user:
        refresh = RefreshToken.for_user(user)
        return Response({
            'access': str(refresh.access_token),
            'refresh': str(refresh)
        })
    return Response({'error': 'Invalid credentials'}, status=401)

@api_view(['GET'])
@permission_classes([IsAuthenticated])
def protected_route(request):
    return Response({'message': f'Hello, {request.user.username}!'})
```

---

## 🎯 Node.js vs Django

| Aspect | 🟢 Node.js/Express | 🐍 Django |
|--------|-------------------|----------|
| **Language** | JavaScript | Python |
| **Learning Curve** | Moderate | Steeper |
| **Philosophy** | Minimalist, flexible | Batteries included |
| **Performance** | Fast (async I/O) | Good (but slower) |
| **Best For** | Real-time apps, APIs | Full-stack apps, admin panels |
| **Ecosystem** | npm (huge) | pip (mature) |
| **Admin Panel** | Build your own | Built-in |
| **ORM** | Sequelize, Prisma | Django ORM (excellent) |

### 🧠 Choose Node.js when:
- Building real-time applications (chat, gaming)
- Need maximum flexibility
- Team knows JavaScript
- Microservices architecture

### 🧠 Choose Django when:
- Building full-stack applications
- Need rapid development
- Team knows Python
- Want built-in admin interface

---

## 🛡️ Part 5 · Backend Best Practices

### 📋 API Design Principles

```javascript
// ✅ Use plural nouns for resources
GET /api/users
GET /api/posts

// ❌ Don't use verbs
GET /api/getUsers
POST /api/createUser

// ✅ Use nested routes for relationships
GET /api/users/123/posts

// ✅ Version your API
GET /api/v1/users
GET /api/v2/users

// ✅ Use query parameters for filtering
GET /api/users?age=25&role=admin
```

### 🔒 Security Checklist

- [ ] Hash all passwords (never store plain text)
- [ ] Use HTTPS in production
- [ ] Implement rate limiting
- [ ] Validate and sanitize all inputs
- [ ] Use environment variables for secrets
- [ ] Enable CORS properly
- [ ] Implement proper error handling
- [ ] Use security headers (helmet.js)
- [ ] Keep dependencies updated
- [ ] Log security events

### ⚡ Performance Tips

```javascript
// Use caching
const redis = require('redis');
const client = redis.createClient();

// Database connection pooling
const pool = new Pool({
  max: 20,
  connectionTimeoutMillis: 2000
});

// Pagination
app.get('/api/users', (req, res) => {
  const page = parseInt(req.query.page) || 1;
  const limit = parseInt(req.query.limit) || 10;
  const offset = (page - 1) * limit;
  
  // Query with limit and offset
});

// Compression
const compression = require('compression');
app.use(compression());
```

### 📝 Environment Variables

```javascript
// .env file (never commit this!)
DATABASE_URL=postgresql://user:pass@localhost:5432/mydb
JWT_SECRET=your-super-secret-key
PORT=3000
NODE_ENV=production

// Usage
require('dotenv').config();

const dbUrl = process.env.DATABASE_URL;
const jwtSecret = process.env.JWT_SECRET;
```

---

## 🤖 AI Tip · Backend Development

### ✅ Smart Prompts:

- *"Create a REST API endpoint for user registration with validation"*
- *"Explain the difference between JWT and session authentication"*
- *"How do I implement rate limiting in Express?"*
- *"Debug this SQL query performance issue"*
- *"Design a scalable authentication system"*

### 🎯 AI Can Help With:

- Generating boilerplate API code
- Explaining authentication flows
- Debugging server errors
- Optimizing database queries
- Security best practices

---

## 🎯 Mission · Day 08

**Build your first API** 🚀

- [ ] 🟢 Set up a basic Express server OR 🐍 Django project
- [ ] 📋 Create a CRUD API for a resource (users, posts, todos)
- [ ] 🔐 Implement basic authentication (login/register)
- [ ] 🧪 Test all endpoints with Postman or curl
- [ ] 🛡️ Add input validation
- [ ] 📊 Return proper HTTP status codes

### Bonus Challenge ⭐

- [ ] Implement JWT token authentication
- [ ] Add pagination to your GET endpoints
- [ ] Create a relationship between two models
- [ ] Implement rate limiting
- [ ] Add API documentation (Swagger/OpenAPI)
- [ ] Deploy your API to a cloud platform (Heroku, Railway, Render)
- [ ] Connect your API to a frontend application

---

<div align="center">

## 🏆 Achievement Unlocked

### *"The Backend Engineer"*

**You now understand:**
- REST API design
- Authentication & Authorization
- Node.js/Express development
- Django/Python development
- Security best practices

You're no longer just building interfaces.  
**You're building the engine that powers them.**

---

### 🎓 Pro Tip

> "A great API is invisible.  
> Users never think about it—it just works.  
> That's when you know you've succeeded."

---

➡️ [Continue to Chapter 09 · Testing & Debugging](../09-Testing/README.md)

</div>
