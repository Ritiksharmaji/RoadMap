Here’s a detailed **roadmap to learning Express.js** from basic to advanced:

---

## **Getting Started with Express.js**
### **1. Introduction to Express.js**
- What is Express.js?
- Advantages of using Express.js.
- Setting up a basic Express server.

**Example:**
```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, Express!');
});

app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

---

## **Basic Concepts**
### **2. Routing**
- Basic Routing (`GET`, `POST`, `PUT`, `DELETE`).
- Route Parameters and Query Parameters.

**Example:**
```javascript
app.get('/user/:id', (req, res) => {
  res.send(`User ID: ${req.params.id}`);
});

app.get('/search', (req, res) => {
  res.send(`Search Query: ${req.query.q}`);
});
```

### **3. Middleware**
- What is Middleware?
- Built-in Middleware (`express.json()`, `express.static()`).
- Custom Middleware.

**Example:**
```javascript
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
});
```

---

## **Intermediate Concepts**
### **4. Working with Requests and Responses**
- Parsing Request Bodies (`express.json()`, `express.urlencoded()`).
- Setting Headers and Cookies.
- Sending Responses (`res.json()`, `res.sendFile()`).

**Example:**
```javascript
app.post('/data', express.json(), (req, res) => {
  res.send(`Received Data: ${JSON.stringify(req.body)}`);
});
```

### **5. Express Router**
- Modularizing routes using `express.Router`.
- Organizing routes in separate files.

**Example:**
```javascript
const router = express.Router();

router.get('/', (req, res) => res.send('Welcome to the home page!'));
router.get('/about', (req, res) => res.send('About Us'));

app.use('/', router);
```

### **6. Static Files**
- Serving static files like HTML, CSS, and JavaScript using `express.static()`.

**Example:**
```javascript
app.use('/static', express.static('public'));
```

---

## **Database Integration**
### **7. Connecting to a Database**
- MongoDB with Mongoose.
- Performing CRUD operations with MongoDB.

**Example:**
```javascript
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost:27017/mydb', { useNewUrlParser: true, useUnifiedTopology: true });

const userSchema = new mongoose.Schema({ name: String });
const User = mongoose.model('User', userSchema);

app.post('/user', async (req, res) => {
  const user = new User({ name: req.body.name });
  await user.save();
  res.send('User Created!');
});
```

---

## **Advanced Topics**
### **8. Error Handling**
- Default Error Handling Middleware.
- Custom Error Handling Middleware.

**Example:**
```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something went wrong!');
});
```

### **9. Authentication and Authorization**
- Password hashing with `bcrypt`.
- Using JSON Web Tokens (JWT).
- Role-based access control.

**Example:**
```javascript
const jwt = require('jsonwebtoken');

app.post('/login', (req, res) => {
  const token = jwt.sign({ userId: 1 }, 'secretKey');
  res.json({ token });
});

app.get('/protected', (req, res) => {
  const token = req.headers['authorization'];
  if (!token) return res.status(403).send('Access Denied');
  jwt.verify(token, 'secretKey', (err, user) => {
    if (err) return res.status(403).send('Invalid Token');
    res.send('Protected Data');
  });
});
```

---

## **Optimization and Security**
### **10. Performance Optimization**
- Compress responses with `compression`.
- Caching responses.
- Using asynchronous patterns with Promises or `async/await`.

**Example:**
```javascript
const compression = require('compression');
app.use(compression());
```

### **11. Security Best Practices**
- Using `helmet` for securing HTTP headers.
- Enabling CORS with `cors`.
- Sanitizing inputs to prevent NoSQL injections.

**Example:**
```javascript
const helmet = require('helmet');
const cors = require('cors');

app.use(helmet());
app.use(cors());
```

---

## **Advanced Applications**
### **12. Real-Time Applications**
- Using Socket.IO for WebSocket-based real-time communication.

**Example:**
```javascript
const http = require('http');
const { Server } = require('socket.io');
const server = http.createServer(app);
const io = new Server(server);

io.on('connection', (socket) => {
  console.log('A user connected');
  socket.on('message', (msg) => {
    console.log(`Message: ${msg}`);
  });
});

server.listen(3000, () => console.log('Server with Socket.IO running'));
```

### **13. Building RESTful APIs**
- Creating a full CRUD API with Express and MongoDB.
- Versioning APIs (`/api/v1`).

### **14. Building GraphQL APIs**
- Setting up Apollo Server with Express for GraphQL.

---

## **Testing**
### **15. Testing Express Applications**
- Unit Testing with Mocha/Chai.
- Integration Testing with Supertest.

**Example:**
```javascript
const request = require('supertest');
describe('GET /', () => {
  it('should return Hello, Express!', async () => {
    const res = await request(app).get('/');
    expect(res.text).toBe('Hello, Express!');
  });
});
```

---

## **Deployment**
### **16. Deploying Express.js Applications**
- Deploying on Heroku, Render, or AWS.
- Using `PM2` to manage server processes.
- Environment variable management (`dotenv`).

**Example:**
```javascript
const dotenv = require('dotenv');
dotenv.config();

app.listen(process.env.PORT || 3000, () => {
  console.log(`Server running on port ${process.env.PORT}`);
});
```

---

## **Express.js Practice Projects**
1. **Task Manager API**:
   - CRUD operations for managing tasks.
   - User authentication.
2. **Blog Platform**:
   - Create and manage posts.
   - Add comments to posts.
3. **Chat Application**:
   - Real-time chat using Socket.IO.
   - Authentication with JWT.

---

Would you like a detailed example or code for any specific concept or project?