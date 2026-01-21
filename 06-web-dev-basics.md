<div align="center">

# 🌐 Chapter 06 · Web Dev Basics

### HTML5 · CSS3 · DOM Manipulation

![Web Development](https://media.giphy.com/media/13FrpeVH09Zrb2/giphy.gif)

> *"Every website you've ever visited is just HTML, CSS, and JavaScript working together."*

[🔙 Back to Chapter 05](./05-version-control.md) • [Next Chapter 🔜](./07-data-management.md)

[🔙 Back to Chapter 05](./05-version-control.md)

</div>

---

## 🏗️ The Three Pillars of the Web

Every website is built with three core technologies:

| Technology | Purpose | Analogy |
|------------|---------|---------|
| 🏛️ **HTML** | Structure & Content | The skeleton of a house |
| 🎨 **CSS** | Style & Design | The paint and decoration |
| ⚡ **JavaScript** | Behavior & Interactivity | The electricity and plumbing |

> 💡 **HTML** defines WHAT is on the page  
> 💡 **CSS** defines HOW it looks  
> 💡 **JavaScript** defines HOW it behaves

---

## 🏛️ Part 1 · HTML5

### *The Foundation of Every Website*

**HTML** (HyperText Markup Language) is the skeleton of the web.

It uses **tags** to structure content:

```html
<tagname>Content goes here</tagname>
```

### 🧱 Basic HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First Website</title>
</head>
<body>
    <h1>Hello, World!</h1>
    <p>This is my first webpage.</p>
</body>
</html>
```

### 📋 Common HTML Tags

#### Text Content
```html
<h1>Main Heading</h1>
<h2>Subheading</h2>
<p>This is a paragraph.</p>
<strong>Bold text</strong>
<em>Italic text</em>
<a href="https://example.com">This is a link</a>
```

#### Lists
```html
<!-- Unordered List -->
<ul>
    <li>Coffee</li>
    <li>Tea</li>
    <li>Milk</li>
</ul>

<!-- Ordered List -->
<ol>
    <li>First step</li>
    <li>Second step</li>
    <li>Third step</li>
</ol>
```

#### Images & Media
```html
<img src="photo.jpg" alt="Description of image">
<video controls>
    <source src="video.mp4" type="video/mp4">
</video>
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
</audio>
```

#### Forms
```html
<form action="/submit" method="POST">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    
    <button type="submit">Submit</button>
</form>
```

### 🆕 HTML5 Semantic Tags

Semantic tags make your HTML more meaningful:

```html
<header>
    <nav>
        <a href="#home">Home</a>
        <a href="#about">About</a>
    </nav>
</header>

<main>
    <article>
        <h2>Article Title</h2>
        <p>Article content...</p>
    </article>
    
    <aside>
        <h3>Related Links</h3>
    </aside>
</main>

<footer>
    <p>&copy; 2026 My Website</p>
</footer>
```

### 🧠 Why Semantic HTML Matters

- ♿ **Accessibility** - Screen readers understand structure
- 🔍 **SEO** - Search engines rank better
- 🧹 **Maintainability** - Code is easier to read

---

## 🎨 Part 2 · CSS3

### *Making the Web Beautiful*

**CSS** (Cascading Style Sheets) controls how your HTML looks.

### 🎯 Three Ways to Add CSS

#### 1. Inline (not recommended)
```html
<p style="color: blue;">This is blue text</p>
```

#### 2. Internal
```html
<head>
    <style>
        p {
            color: blue;
        }
    </style>
</head>
```

#### 3. External (best practice)
```html
<head>
    <link rel="stylesheet" href="styles.css">
</head>
```

### 🎨 CSS Syntax

```css
selector {
    property: value;
}
```

**Example:**
```css
h1 {
    color: navy;
    font-size: 32px;
    text-align: center;
}
```

### 🎯 CSS Selectors

```css
/* Element selector */
p {
    color: black;
}

/* Class selector */
.highlight {
    background-color: yellow;
}

/* ID selector */
#header {
    background-color: blue;
}

/* Descendant selector */
div p {
    margin: 10px;
}

/* Multiple selectors */
h1, h2, h3 {
    font-family: Arial, sans-serif;
}
```

### 📦 The Box Model

Every HTML element is a box with:

```
┌─────────────────────────────┐
│         Margin              │
│  ┌──────────────────────┐   │
│  │      Border          │   │
│  │  ┌───────────────┐   │   │
│  │  │   Padding     │   │   │
│  │  │  ┌────────┐   │   │   │
│  │  │  │Content │   │   │   │
│  │  │  └────────┘   │   │   │
│  │  └───────────────┘   │   │
│  └──────────────────────┘   │
└─────────────────────────────┘
```

```css
.box {
    width: 200px;
    padding: 20px;
    border: 2px solid black;
    margin: 10px;
}
```

### 🎨 Modern CSS Layout

#### Flexbox (1D Layout)
```css
.container {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
}
```

#### Grid (2D Layout)
```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}
```

### ✨ CSS3 Features

```css
/* Gradients */
.gradient {
    background: linear-gradient(to right, #ff6b6b, #4ecdc4);
}

/* Shadows */
.card {
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Transitions */
.button {
    transition: all 0.3s ease;
}

.button:hover {
    transform: scale(1.1);
    background-color: #3498db;
}

/* Animations */
@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

.animated {
    animation: fadeIn 1s ease-in;
}
```

### 📱 Responsive Design

```css
/* Mobile First Approach */
.container {
    width: 100%;
    padding: 10px;
}

/* Tablet */
@media (min-width: 768px) {
    .container {
        width: 750px;
        margin: 0 auto;
    }
}

/* Desktop */
@media (min-width: 1024px) {
    .container {
        width: 960px;
    }
}
```

---

## ⚡ Part 3 · DOM Manipulation

### *Bringing Pages to Life*

The **DOM** (Document Object Model) is how JavaScript sees your HTML.

Think of it as:
> 🌳 A tree structure representing your webpage

### 🎯 Selecting Elements

```javascript
// Select by ID
const header = document.getElementById('header');

// Select by class
const buttons = document.getElementsByClassName('btn');

// Modern way (recommended)
const header = document.querySelector('#header');
const buttons = document.querySelectorAll('.btn');
```

### ✏️ Changing Content

```javascript
// Change text
document.querySelector('h1').textContent = 'New Title';

// Change HTML
document.querySelector('.content').innerHTML = '<p>New content</p>';

// Change attributes
document.querySelector('img').src = 'new-image.jpg';
```

### 🎨 Changing Styles

```javascript
const box = document.querySelector('.box');

// Direct style changes
box.style.backgroundColor = 'blue';
box.style.padding = '20px';

// Adding/removing classes (better practice)
box.classList.add('active');
box.classList.remove('hidden');
box.classList.toggle('highlight');
```

### ➕ Creating & Adding Elements

```javascript
// Create new element
const newDiv = document.createElement('div');
newDiv.textContent = 'I am new!';
newDiv.classList.add('new-item');

// Add to page
document.body.appendChild(newDiv);

// Insert before another element
const container = document.querySelector('.container');
container.insertBefore(newDiv, container.firstChild);
```

### 🗑️ Removing Elements

```javascript
const element = document.querySelector('.remove-me');
element.remove();
```

### 🖱️ Event Listeners

```javascript
// Click event
const button = document.querySelector('button');
button.addEventListener('click', function() {
    alert('Button clicked!');
});

// Input event
const input = document.querySelector('input');
input.addEventListener('input', function(e) {
    console.log('Current value:', e.target.value);
});

// Form submit
const form = document.querySelector('form');
form.addEventListener('submit', function(e) {
    e.preventDefault(); // Prevent page reload
    console.log('Form submitted!');
});
```

### 🎯 Practical Example: Interactive Counter

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        .counter {
            text-align: center;
            font-size: 48px;
            margin: 20px;
        }
        button {
            font-size: 20px;
            padding: 10px 20px;
            margin: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="counter" id="count">0</div>
    <button id="increment">+</button>
    <button id="decrement">-</button>
    <button id="reset">Reset</button>

    <script>
        let count = 0;
        const countDisplay = document.getElementById('count');

        document.getElementById('increment').addEventListener('click', () => {
            count++;
            countDisplay.textContent = count;
        });

        document.getElementById('decrement').addEventListener('click', () => {
            count--;
            countDisplay.textContent = count;
        });

        document.getElementById('reset').addEventListener('click', () => {
            count = 0;
            countDisplay.textContent = count;
        });
    </script>
</body>
</html>
```

---

## 🤖 AI Tip · Web Development

### ✅ Smart Prompts:

- *"Create a responsive navbar with HTML and CSS"*
- *"How do I center a div vertically and horizontally?"*
- *"Explain the difference between classList and className"*
- *"Debug this CSS flexbox layout"*

### 🎨 AI Can Help With:

- Generating boilerplate HTML structures
- Creating CSS animations
- Explaining browser compatibility
- Debugging layout issues

---

## 🎯 Mission · Day 06

**Build your first webpage** 🚀

- [ ] 📄 Create an HTML file with proper structure
- [ ] 🎨 Style it with CSS (external stylesheet)
- [ ] 🎯 Use at least 3 semantic HTML5 tags
- [ ] 📱 Make it responsive with media queries
- [ ] ⚡ Add a button that changes content with JavaScript
- [ ] 🖱️ Implement at least 2 different event listeners

### Bonus Challenge ⭐

- [ ] Create a todo list app with add/remove functionality
- [ ] Build a simple form with validation
- [ ] Implement a dark mode toggle
- [ ] Create a photo gallery with CSS Grid

---

## 📚 Common Patterns

### ✅ Good Practices

```css
/* Use meaningful class names */
.btn-primary { }
.card-header { }
.navigation-menu { }

/* Group related properties */
.box {
    /* Positioning */
    position: relative;
    
    /* Box model */
    width: 200px;
    padding: 20px;
    
    /* Visual */
    background: white;
    border-radius: 8px;
}
```

### ❌ Avoid

```css
/* Don't use inline styles */
<div style="color: red; font-size: 20px;">Bad</div>

/* Don't use !important unless necessary */
.text {
    color: blue !important; /* Avoid */
}

/* Don't use too many IDs for styling */
#header #nav #menu { } /* Use classes instead */
```

---

<div align="center">

## 🏆 Achievement Unlocked

### *"The Web Builder"*

**You now understand:**
- HTML5 structure and semantics
- CSS3 styling and layouts
- DOM manipulation with JavaScript
- Event-driven programming

You're no longer just a coder.  
**You're a web developer.**

---

### 🎓 Pro Tip

> "View Source is your friend.  
> Every website is a learning opportunity."

**Try it:** Right-click → View Page Source on any website!

---

➡️ [Continue to Chapter 07 · Data Management](./07-data-management.md)

</div>
