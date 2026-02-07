<div align="center">

# ⚙️ Chapter 08 · Backend Dev

![Backend](https://img.shields.io/badge/Backend-Developer-blueviolet?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Server-success?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Backend_Engineer-orange?style=for-the-badge)

### *APIs · Authentication · Node.js / Django*

<img src="https://media.giphy.com/media/l3vRfNA1p0rvhMSvS/giphy.gif" width="500">

</div>

---

> [!NOTE]
> *"Frontend is what users see. Backend is what makes it work."*

<div align="center">

[![Back to Chapter 07](https://img.shields.io/badge/🔙-Chapter_07-blue?style=flat-square)](./07-data-management.md)
[![Next Chapter](https://img.shields.io/badge/Next_Chapter-🔜-green?style=flat-square)](./09-front-end-dev.md)

</div>

<br>

## 🎭 Frontend vs Backend

<div align="center">

Every web application has two sides:

</div>

<br>

<table>
<tr>
<td width="50%" align="center" bgcolor="#e3f2fd">

### 🎨 Frontend

**What users see**  
UI/UX  
HTML, CSS, JavaScript  
Runs in browser  
Client-side

</td>
<td width="50%" align="center" bgcolor="#f3e5f5">

### ⚙️ Backend

**What users don't see**  
Business logic  
Server-side code  
Runs on server  
Server-side

</td>
</tr>
</table>

---

<br>

### 🧠 Mental Model

<br>

<div align="center">

```mermaid
graph LR
    A[👤 User] --> B[🎨 Frontend<br/>React]
    B --> C[🔌 API<br/>REST]
    C --> D[⚙️ Backend<br/>Node.js]
    D --> E[🗄️ Database<br/>PostgreSQL]
    E --> D
    D --> C
    C --> B
    B --> A
    
    style A fill:#e3f2fd
    style B fill:#f3e5f5
    style C fill:#fff9c4
    style D fill:#c8e6c9
    style E fill:#ffccbc
```

</div>

<br>

> [!TIP]
> **Think of it like a restaurant:**
> - **Frontend** = Dining room (what customers experience)
> - **Backend** = Kitchen (where the real work happens)
> - **API** = Waiter (connects both sides)

---

<br>

## 🌐 Part 1 · APIs (Application Programming Interfaces)

<div align="center">

### *The Bridge Between Systems*

An **API** is a way for different software to talk to each other.

</div>

<br>

<table>
<tr>
<td width="50%" bgcolor="#ffebee" valign="top">

### ❌ Without APIs:

- Every app needs its own data
- No integration between services
- Frontend and backend can't communicate
- Duplicate code everywhere
- Hard to maintain

</td>
<td width="50%" bgcolor="#e8f5e9" valign="top">

### ✅ With APIs:

- Share data across platforms
- Services work together
- Clean separation of concerns
- Reusable endpoints
- Easy to scale

</td>
</tr>
</table>

---

<br>

### 🔗 REST APIs

<div align="center">

**REST** (Representational State Transfer) is the most common API style.

</div>

<br>

#### Key Concepts:

<br>

<div align="center">

| Concept | Description |
|:---|:---|
| **Endpoint** | A specific URL that performs an action |
| **HTTP Method** | The type of action (GET, POST, etc.) |
| **Request** | Data sent to the server |
| **Response** | Data returned from the server |
| **Status Code** | Result of the request (200, 404, etc.) |

</div>

---

<br>

### 📋 HTTP Methods (CRUD Mapping)

<br>

<div align="center">

| Method | Purpose | SQL | Example |
|:---:|:---|:---:|:---|
| **GET** | Retrieve data | SELECT | Get list of users |
| **POST** | Create new data | INSERT | Create new user |
| **PUT/PATCH** | Update data | UPDATE | Modify user info |
| **DELETE** | Remove data | DELETE | Delete user |

</div>

---

<br>

### 🎯 API Endpoint Examples

<br>

<details>
<summary><b>📡 RESTful Endpoint Patterns</b></summary>

<br>

```
GET    /api/users           → Get all users
GET    /api/users/123       → Get user with ID 123
POST   /api/users           → Create new user
PUT    /api/users/123       → Update user 123
DELETE /api/users/123       → Delete user 123

GET    /api/posts?author=5  → Get posts by author 5
POST   /api/posts           → Create new post
GET    /api/users/123/posts → Get posts by user 123
```

</details>

---

<br>

### 📊 HTTP Status Codes

<br>

<table>
<tr>
<td width="50%" valign="top">

#### ✅ Success Codes (2xx)

| Code | Meaning | Use Case |
|:---:|:---|:---|
| **200** | OK | Successful request |
| **201** | Created | Resource created |
| **204** | No Content | Successful deletion |

</td>
<td width="50%" valign="top">

#### ❌ Error Codes (4xx, 5xx)

| Code | Meaning | Use Case |
|:---:|:---|:---|
| **400** | Bad Request | Invalid input |
| **401** | Unauthorized | Not authenticated |
| **403** | Forbidden | Not authorized |
| **404** | Not Found | Resource missing |
| **500** | Server Error | Server crashed |

</td>
</tr>
</table>

---

<br>

### 🔄 Request/Response Flow

<br>

<details>
<summary><b>📨 Complete HTTP Transaction</b></summary>

<br>

**REQUEST:**
```json
POST /api/users
Content-Type: application/json

{
  "name": "Alice",
  "email": "alice@email.com",
  "age": 28
}
```

**RESPONSE:**
```json
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

</details>

---

<br>

## 🔐 Part 2 · Authentication & Authorization

<div align="center">

### *Who Are You? What Can You Do?*

</div>

<br>

> [!IMPORTANT]
> **Authentication** = Verifying identity (who you are)  
> **Authorization** = Verifying permissions (what you can do)

---

<br>

### 🎯 Authentication Methods

<br>

#### 1. Session-Based Auth (Traditional)

<br>

<details>
<summary><b>🔐 How Session Auth Works</b></summary>

<br>

```mermaid
sequenceDiagram
    participant U as User
    participant S as Server
    participant D as Database
    
    U->>S: Login (username, password)
    S->>D: Verify credentials
    D-->>S: User found
    S->>S: Create session
    S-->>U: Session ID (cookie)
    U->>S: Request + Session ID
    S->>S: Validate session
    S-->>U: Protected data
```

<br>

**Process:**
1. User logs in with credentials
2. Server creates a session
3. Server sends session ID as cookie
4. Client sends cookie with each request
5. Server validates session ID

**Pros:** Simple, secure, easy to invalidate  
**Cons:** Doesn't scale well, requires server storage

</details>

---

<br>

#### 2. Token-Based Auth (Modern)

<br>

<details>
<summary><b>🎫 JWT (JSON Web Tokens)</b></summary>

<br>

```mermaid
sequenceDiagram
    participant U as User
    participant S as Server
    
    U->>S: Login (username, password)
    S->>S: Verify credentials
    S->>S: Generate JWT
    S-->>U: JWT Token
    U->>U: Store token (localStorage)
    U->>S: Request + JWT Header
    S->>S: Verify token signature
    S-->>U: Protected data
```

<br>

**Token Structure:**
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJ1c2VySWQiOjEyMywiZW1haWwiOiJhbGljZUBlbWFpbC5jb20ifQ.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

Header.Payload.Signature
```

**Pros:** Stateless, scalable, works across domains  
**Cons:** Can't invalidate easily, larger than session ID

</details>

---

<br>

#### 3. OAuth 2.0 (Third-Party)

<br>

<details>
<summary><b>🔗 "Login with Google/GitHub/Facebook"</b></summary>

<br>

```mermaid
sequenceDiagram
    participant U as User
    participant Y as Your App
    participant G as Google
    
    U->>Y: Click "Login with Google"
    Y-->>U: Redirect to Google
    U->>G: Approve access
    G-->>Y: Authorization code
    Y->>G: Exchange code for token
    G-->>Y: Access token
    Y->>G: Request user data
    G-->>Y: User profile
    Y-->>U: Logged in!
```

<br>

**Process:**
1. User clicks "Login with Google"
2. Redirected to Google
3. User approves access
4. Google sends authorization code
5. Your server exchanges code for access token
6. You can now access user's Google data

</details>

---

<br>

### 🔒 Password Security

<br>

<table>
<tr>
<td width="50%" bgcolor="#ffebee" valign="top">

#### ❌ NEVER Do This:

```javascript
// Storing plain passwords
user.password = "password123";

// Weak hashing
user.password = md5(password);
```

</td>
<td width="50%" bgcolor="#e8f5e9" valign="top">

#### ✅ Always Do This:

```javascript
const bcrypt = require('bcrypt');

// Hash password
const hash = await bcrypt.hash(
  password, 
  10 // salt rounds
);

// Verify password
const isValid = await bcrypt.compare(
  inputPassword, 
  hashedPassword
);
```

</td>
</tr>
</table>

---

<br>

### 🛡️ Securing APIs

<br>

<details>
<summary><b>🔐 JWT Authentication Middleware</b></summary>

<br>

```javascript
const jwt = require('jsonwebtoken');

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

</details>

---

<br>

## 🟢 Part 3 · Node.js & Express

<div align="center">

### *JavaScript on the Server*

**Node.js** lets you run JavaScript outside the browser.  
**Express** is the most popular Node.js framework for building APIs.

</div>

---

<br>

### 🚀 Basic Express Server

<br>

<details>
<summary><b>⚡ Minimal Express Setup</b></summary>

<br>

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

</details>

---

<br>

### 📋 Complete CRUD API Example

<br>

<details>
<summary><b>🔧 Full REST API Implementation</b></summary>

<br>

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

</details>

---

<br>

### 🔧 Essential Express Middleware

<br>

<details>
<summary><b>🛡️ Security & Utilities Middleware</b></summary>

<br>

```javascript
const cors = require('cors');
const helmet = require('helmet');
const morgan = require('morgan');
const compression = require('compression');

// Security headers
app.use(helmet());

// Enable CORS (allow frontend to call API)
app.use(cors({
  origin: 'https://yourfrontend.com',
  credentials: true
}));

// Logging
app.use(morgan('dev'));

// Parse JSON bodies
app.use(express.json());

// Compression
app.use(compression());

// Error handling
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Something went wrong!' });
});
```

</details>

---

<br>

## 🐍 Part 4 · Django & Python

<div align="center">

### *Batteries Included Framework*

**Django** is a full-featured Python framework for building web applications.

</div>

---

<br>

### 🚀 Django Project Structure

<br>

<details>
<summary><b>📁 Project Organization</b></summary>

<br>

```
myproject/
├── manage.py              # Command-line utility
├── myproject/
│   ├── settings.py        # Configuration
│   ├── urls.py            # URL routing
│   └── wsgi.py            # WSGI config
└── myapp/
    ├── models.py          # Database models
    ├── views.py           # Request handlers
    ├── urls.py            # App routes
    ├── serializers.py     # API serialization
    ├── admin.py           # Admin interface
    └── tests.py           # Unit tests
```

</details>

---

<br>

### 📋 Django Models (ORM)

<br>

<details>
<summary><b>🗄️ Database Models with Django ORM</b></summary>

<br>

```python
from django.db import models

class User(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField(unique=True)
    age = models.IntegerField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    is_active = models.BooleanField(default=True)
    
    class Meta:
        ordering = ['-created_at']
        indexes = [
            models.Index(fields=['email']),
        ]
    
    def __str__(self):
        return self.name

class Post(models.Model):
    author = models.ForeignKey(
        User, 
        on_delete=models.CASCADE,
        related_name='posts'
    )
    title = models.CharField(max_length=200)
    content = models.TextField()
    published_at = models.DateTimeField(auto_now_add=True)
    views = models.IntegerField(default=0)
    
    def __str__(self):
        return self.title
```

</details>

---

<br>

### 🔧 Django REST Framework API

<br>

<details>
<summary><b>🔌 ViewSet Approach (Automatic CRUD)</b></summary>

<br>

```python
from rest_framework import viewsets
from rest_framework.permissions import IsAuthenticatedOrReadOnly
from .models import User
from .serializers import UserSerializer

class UserViewSet(viewsets.ModelViewSet):
    """
    API endpoint for users
    Provides: list, create, retrieve, update, destroy
    """
    queryset = User.objects.all()
    serializer_class = UserSerializer
    permission_classes = [IsAuthenticatedOrReadOnly]
    
    def get_queryset(self):
        # Custom filtering
        queryset = User.objects.all()
        age = self.request.query_params.get('age')
        if age is not None:
            queryset = queryset.filter(age=age)
        return queryset
```

</details>

<details>
<summary><b>⚙️ Function-Based Views</b></summary>

<br>

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response
from rest_framework import status
from .models import User
from .serializers import UserSerializer

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
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

@api_view(['GET', 'PUT', 'DELETE'])
def user_detail(request, pk):
    try:
        user = User.objects.get(pk=pk)
    except User.DoesNotExist:
        return Response(status=status.HTTP_404_NOT_FOUND)
    
    if request.method == 'GET':
        serializer = UserSerializer(user)
        return Response(serializer.data)
    
    elif request.method == 'PUT':
        serializer = UserSerializer(user, data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
    
    elif request.method == 'DELETE':
        user.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```

</details>

---

<br>

### 🔐 Django Authentication

<br>

<details>
<summary><b>🔑 JWT Authentication with Django</b></summary>

<br>

```python
from rest_framework.decorators import api_view, permission_classes
from rest_framework.permissions import IsAuthenticated
from django.contrib.auth import authenticate
from rest_framework_simplejwt.tokens import RefreshToken
from rest_framework.response import Response
from rest_framework import status

@api_view(['POST'])
def login(request):
    username = request.data.get('username')
    password = request.data.get('password')
    
    user = authenticate(username=username, password=password)
    if user:
        refresh = RefreshToken.for_user(user)
        return Response({
            'access': str(refresh.access_token),
            'refresh': str(refresh),
            'user': {
                'id': user.id,
                'username': user.username,
                'email': user.email
            }
        })
    return Response(
        {'error': 'Invalid credentials'}, 
        status=status.HTTP_401_UNAUTHORIZED
    )

@api_view(['GET'])
@permission_classes([IsAuthenticated])
def protected_route(request):
    return Response({
        'message': f'Hello, {request.user.username}!',
        'user_id': request.user.id
    })
```

</details>

---

<br>

## 🎯 Node.js vs Django

<br>

<div align="center">

| Aspect | 🟢 Node.js/Express | 🐍 Django |
|:---|:---:|:---:|
| **Language** | JavaScript | Python |
| **Learning Curve** | Moderate | Steeper |
| **Philosophy** | Minimalist, flexible | Batteries included |
| **Performance** | Fast (async I/O) | Good (but slower) |
| **Best For** | Real-time, APIs | Full-stack, admin |
| **Ecosystem** | npm (huge) | pip (mature) |
| **Admin Panel** | Build your own | Built-in ✨ |
| **ORM** | Sequelize, Prisma | Django ORM ⭐ |

</div>

---

<br>

### 🧠 Choose Node.js when:

<table>
<tr>
<td width="50%" bgcolor="#e8f5e9" valign="top">

- Building real-time applications (chat, gaming)
- Need maximum flexibility
- Team knows JavaScript
- Microservices architecture
- High concurrency requirements
- Streaming applications

</td>
<td width="50%" bgcolor="#e3f2fd" valign="top">

### 🧠 Choose Django when:

- Building full-stack applications
- Need rapid development
- Team knows Python
- Want built-in admin interface
- Complex data models
- Content management systems

</td>
</tr>
</table>

---

<br>

## 🛡️ Part 5 · Backend Best Practices

<br>

### 📋 API Design Principles

<br>

<table>
<tr>
<td width="50%" bgcolor="#e8f5e9" valign="top">

#### ✅ Good Practices:

```javascript
// Use plural nouns for resources
GET /api/users
GET /api/posts

// Nested routes for relationships
GET /api/users/123/posts

// Version your API
GET /api/v1/users

// Query parameters for filtering
GET /api/users?age=25&role=admin
```

</td>
<td width="50%" bgcolor="#ffebee" valign="top">

#### ❌ Avoid:

```javascript
// Don't use verbs
GET /api/getUsers
POST /api/createUser

// Don't use actions in URLs
POST /api/users/delete

// Don't mix plural/singular
GET /api/user
GET /api/posts
```

</td>
</tr>
</table>

---

<br>

### 🔒 Security Checklist

<br>

<table>
<tr>
<td width="50%" valign="top">

#### 🛡️ Authentication & Data:

- [ ] Hash all passwords (bcrypt)
- [ ] Use HTTPS in production
- [ ] Validate all inputs
- [ ] Sanitize user data
- [ ] Use environment variables for secrets
- [ ] Implement CSRF protection

</td>
<td width="50%" valign="top">

#### 🔐 API & Infrastructure:

- [ ] Implement rate limiting
- [ ] Enable CORS properly
- [ ] Use security headers (helmet.js)
- [ ] Keep dependencies updated
- [ ] Log security events
- [ ] Implement proper error handling

</td>
</tr>
</table>

---

<br>

### ⚡ Performance Tips

<br>

<details>
<summary><b>🚀 Caching with Redis</b></summary>

<br>

```javascript
const redis = require('redis');
const client = redis.createClient();

app.get('/api/users/:id', async (req, res) => {
  const { id } = req.params;
  const cacheKey = `user:${id}`;
  
  // Check cache first
  const cached = await client.get(cacheKey);
  if (cached) {
    return res.json(JSON.parse(cached));
  }
  
  // Fetch from database
  const user = await User.findById(id);
  
  // Store in cache (expire in 1 hour)
  await client.setEx(cacheKey, 3600, JSON.stringify(user));
  
  res.json(user);
});
```

</details>

<details>
<summary><b>📊 Database Connection Pooling</b></summary>

<br>

```javascript
const { Pool } = require('pg');

const pool = new Pool({
  max: 20,                    // Max connections
  connectionTimeoutMillis: 2000,
  idleTimeoutMillis: 30000
});

// Use pool for queries
app.get('/api/users', async (req, res) => {
  const result = await pool.query('SELECT * FROM users');
  res.json(result.rows);
});
```

</details>

<details>
<summary><b>📄 Pagination</b></summary>

<br>

```javascript
app.get('/api/users', async (req, res) => {
  const page = parseInt(req.query.page) || 1;
  const limit = parseInt(req.query.limit) || 10;
  const offset = (page - 1) * limit;
  
  const users = await User.find()
    .limit(limit)
    .skip(offset);
  
  const total = await User.countDocuments();
  
  res.json({
    data: users,
    pagination: {
      page,
      limit,
      total,
      pages: Math.ceil(total / limit)
    }
  });
});
```

</details>

<details>
<summary><b>🗜️ Compression</b></summary>

<br>

```javascript
const compression = require('compression');
app.use(compression());
```

</details>

---

<br>

### 📝 Environment Variables

<br>

<details>
<summary><b>🔐 .env Configuration</b></summary>

<br>

```bash
# .env file (NEVER commit this!)
DATABASE_URL=postgresql://user:pass@localhost:5432/mydb
JWT_SECRET=your-super-secret-key-change-this
PORT=3000
NODE_ENV=production
REDIS_URL=redis://localhost:6379
API_KEY=your-api-key-here
```

```javascript
// Usage
require('dotenv').config();

const dbUrl = process.env.DATABASE_URL;
const jwtSecret = process.env.JWT_SECRET;
const port = process.env.PORT || 3000;
```

</details>

---

<br>

## 🤖 AI Tip · Backend Development

<br>

### ✅ Smart Prompts:

<table>
<tr>
<td width="50%">

```
💡 "Create a REST API endpoint for user 
   registration with validation"
```
```
💡 "Explain JWT vs session authentication"
```
```
💡 "Implement rate limiting in Express"
```

</td>
<td width="50%">

```
💡 "Debug this SQL query performance issue"
```
```
💡 "Design a scalable authentication system"
```
```
💡 "Optimize database queries for this endpoint"
```

</td>
</tr>
</table>

<br>

### 🎯 AI Can Help With:

| Area | Application |
|:---|:---|
| ✅ Boilerplate code | API scaffolding |
| ✅ Authentication flows | Security implementation |
| ✅ Debugging | Error analysis |
| ✅ Database queries | Optimization |
| ✅ Security | Best practices |
| ✅ Testing | Unit & integration tests |

---

<br>

## 🎯 Mission · Day 08

<div align="center">

### 🚀 Build your first API

</div>

<br>

### Core Tasks:

- [ ] 🟢 **Set up Express server** — OR 🐍 Django project
- [ ] 📋 **Create CRUD API** — For users, posts, or todos
- [ ] 🔐 **Implement auth** — Login/register endpoints
- [ ] 🧪 **Test endpoints** — Use Postman or curl
- [ ] 🛡️ **Add validation** — Input sanitization
- [ ] 📊 **HTTP status codes** — Return proper codes

<br>

<details>
<summary><b>⭐ Bonus Challenges</b></summary>

<br>

- [ ] 🎫 Implement JWT token authentication
- [ ] 📄 Add pagination to GET endpoints
- [ ] 🔗 Create relationships between models
- [ ] ⏱️ Implement rate limiting
- [ ] 📚 Add API documentation (Swagger/OpenAPI)
- [ ] 🚀 Deploy to cloud (Railway, Render)
- [ ] 🎨 Connect API to frontend application
- [ ] 🧪 Write integration tests

</details>

---

<br>

<div align="center">

## 🏆 Achievement Unlocked

### **The Backend Engineer**

<br>

**You now understand:**
- REST API design
- Authentication & Authorization
- Node.js/Express development
- Django/Python development
- Security best practices

<br>

*You're no longer just building interfaces.*  
**You're building the engine that powers them.**

<br>

![Achievement](https://img.shields.io/badge/🏆-Achievement_Unlocked-gold?style=for-the-badge)

</div>

---

<br>

<div align="center">

### 🎓 Pro Tip

> "A great API is invisible.  
> Users never think about it—it just works.  
> That's when you know you've succeeded."

</div>

---

<br>

<div align="center">

[![Continue](https://img.shields.io/badge/➡️_Continue_to_Chapter_09-Front_End_Development-success?style=for-the-badge)](./09-front-end-dev.md)

</div>

<br>
