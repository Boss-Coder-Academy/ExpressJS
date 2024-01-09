Assignment: Express 



Agenda

1. Introduction
   - Overview of Express.js
   - Why use Express.js?

2. Getting Started
   - Installation
   - Hello World example
   - Project structure

3. Basic Concepts
   - Middleware
   - Routing
   - Request and Response objects
   - Error handling

4. Routing
   - Route parameters
   - Route handlers
   - Route methods (GET, POST, etc.)
   - Route paths and patterns

5. Middleware
   - Built-in middleware
   - Third-party middleware
   - Writing custom middleware
   - Error-handling middleware

6. Request and Response Handling
   - Parsing request data
   - Sending responses
   - Cookies and sessions
   - File uploads

7. Views and Templates
   - Integrating template engines (e.g., EJS, Handlebars)
   - Rendering views
   - Template variables

8. Database Integration
   - Connecting to databases (e.g., MongoDB, MySQL)
   - Using an ORM (e.g., Mongoose, Sequelize)
   - CRUD operations with databases

9. Authentication and Authorizatio
     - Passport.js integration
     - JSON Web Tokens (JWT)
     - Role-based access control


**10. Middleware for Advanced Features**   
    - WebSockets  
    - Compression  
    - Caching

**11. Deployment and Production Considerations**  
    - Environment variables  
    - Reverse proxy setup  
    - Performance optimization  

**12. API Development**  
    - RESTful API design  
    - Versioning  
    - Documentation using tools like Swagger

**13. Scaling Express.js Applications**    
    - Load balancing  
    - Microservices architecture  
    - Containerization with Docker  

**14. Assignment** 



## 1. Introduction to Express.js

**1.1 Overview of Express.js:**

Express.js is a minimal and flexible Node.js web application framework that provides a robust set of features to develop web and mobile applications. It is designed to make building web applications and APIs with Node.js easier and more efficient. Express.js is widely used for its simplicity, performance, and extensibility.


**1.2 Why use Express.js?**

  **1.2.1. Simplicity and Minimalism:**

Express.js provides a straightforward and minimalistic framework, allowing developers to focus on building features rather than dealing with unnecessary complexity.

**1.2.2. Middleware Architecture:**

The middleware architecture of Express.js enables the creation of modular and reusable components that can handle various tasks, such as authentication, logging, and error handling.

**1.2.3. Routing:**

Express.js offers a powerful routing system that makes it easy to define how an application responds to client requests. Routes can handle different HTTP methods and parameters, providing flexibility in defining API endpoints.

**1.2.4. Extensibility:**

Express.js is highly extensible, and developers can use a wide range of middleware and third-party packages to enhance the functionality of their applications.

**1.2.5. Active Community:**

Express.js has a large and active community, which means ample resources, tutorials, and third-party modules are available. This makes problem-solving and development more efficient.




## 2. Getting Started with Express.js

**2.1 Installation:**

Before you can start using Express.js, you need to install it in your project. Open your terminal and navigate to your project's directory. Then, run the following command:

```bash
npm install express
```

This command installs the Express.js module and adds it to your project's `node_modules` folder.

**2.2 Hello World Example:**

Now, let's create a simple "Hello, World!" example using Express.js. Create a file named `app.js` in your project's root directory and add the following code:

```javascript
// Import the Express module
const express = require('express');

// Create an Express application
const app = express();

// Define a route for the root URL
app.get('/', (req, res) => {
  res.send('Hello, World!');
});

// Start the server on port 3000
const port = 3000;
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

Save the file and run the application using the following command:

```bash
node app.js
```

Visit http://localhost:3000 in your web browser, and you should see "Hello, World!" displayed. This simple example demonstrates the basic structure of an Express.js application:

- Import Express: Require the Express module at the beginning of your file.

- Create an Express Application: Create an instance of the Express application using `express()`.

- Define a Route: Use the `app.get()` method to define a route for handling GET requests. In this case, the route is the root URL ("/"), and the callback function specifies the response to send when the route is accessed.

- Start the Server: Use the `app.listen()` method to start the server. It listens on a specified port (in this case, 3000), and the callback function logs a message to the console when the server is running.

**2.3 Project Structure:**

Express.js does not enforce a specific project structure, but organizing your code is crucial for maintainability. Here's a simple project structure example:

```
/my-express-app
  /controllers
    homeController.js
  /routes
    homeRoute.js
  /views
    index.ejs
  app.js
```

- Controllers: The `controllers` directory might contain route handlers. For example, `homeController.js` could handle logic for the home route.

- Routes: The `routes` directory might contain route definitions. `homeRoute.js` could define routes for the home-related functionality.

- Views: The `views` directory might contain template files if you are using a templating engine like EJS. For example, `index.ejs` could be the template for the home page.

- App.js: This file is the entry point of your application where you configure and start the Express server.

## 3. Basic Concepts in Express.js

**3.1 Middleware:**

Middleware functions in Express.js are functions that have access to the request (`req`) object, the response (`res`) object, and the next middleware function in the application's request-response cycle. Middleware functions can perform various tasks, modify request and response objects, and terminate the request-response cycle.

**Example:**

Let's create a simple middleware function that logs information about each incoming request. Add the following code to your `app.js` file:

```javascript
const express = require('express');
const app = express();

// Custom middleware to log request information
app.use((req, res, next) => {
  console.log(`Request received at ${new Date().toLocaleString()}`);
  next(); // Pass control to the next middleware in the stack
});

// Define a route
app.get('/', (req, res) => {
  res.send('Hello, World!');
});

// Start the server on port 3000
const port = 3000;
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

In this example, the `app.use()` method is used to register middleware. The middleware function logs the timestamp of each incoming request to the console. The `next()` function is called to pass control to the next middleware in the stack. If `next()` is not called, the request-response cycle stops, and the client receives no response.

**3.2 Routing:**

Routing in Express.js refers to determining how an application responds to client requests to a particular endpoint, which is a URI (or path) and a specific HTTP request method (GET, POST, etc.).

**Example:**

Let's create a more elaborate example with multiple routes. Modify your `app.js` file as follows:

```javascript
const express = require('express');
const app = express();

// Middleware to log request information
app.use((req, res, next) => {
  console.log(`Request received at ${new Date().toLocaleString()}`);
  next();
});

// Define routes
app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.get('/about', (req, res) => {
  res.send('About Us Page');
});

app.get('/contact', (req, res) => {
  res.send('Contact Us Page');
});

// Start the server on port 3000
const port = 3000;
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

Now, visiting different URLs like http://localhost:3000/about and http://localhost:3000/contact will trigger different route handlers.

In the upcoming sections, we'll explore more advanced routing features, such as handling parameters, using route middleware, and organizing routes in separate files.

**3.3 Request and Response Objects:**

The `req` (request) and `res` (response) objects are essential components in Express.js. The `req` object represents the HTTP request, and the `res` object represents the HTTP response that an Express app sends when it receives an HTTP request.

**Example:**

Let's create a route that demonstrates using the `req` and `res` objects. Modify your `app.js` file as follows:

```javascript
const express = require('express');
const app = express();

// Middleware to log request information
app.use((req, res, next) => {
  console.log(`Request received at ${new Date().toLocaleString()}`);
  next();
});

// Define a route that uses req and res objects
app.get('/greet/:name', (req, res) => {
  const { name } = req.params;
  res.send(`Hello, ${name}!`);
});

// Start the server on port 3000
const port = 3000;
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

In this example, the route `/greet/:name` uses a route parameter (`:name`) to capture a value from the URL. The captured value is then accessed through `req.params`. For example, visiting http://localhost:3000/greet/John will respond with "Hello, John!"





## 4. Routing in Express.js

Routing in Express.js involves determining how an application responds to client requests to specific endpoints. Each route is associated with a URI (Uniform Resource Identifier) and an HTTP request method (GET, POST, etc.). Express provides a convenient way to define routes and handle different parts of your application's functionality.
 

**4.1 Route Parameters:**

Route parameters allow you to capture values from the URL and use them in your route handlers. They are specified in the route path using a colon followed by the parameter name.

**Example:**

Let's create an example where we have a dynamic route parameter to greet users by name. Update your `app.js` file:

```javascript
const express = require('express');
const app = express();

// Middleware to log request information
app.use((req, res, next) => {
  console.log(`Request received at ${new Date().toLocaleString()}`);
  next();
});

// Define a route with a route parameter
app.get('/greet/:name', (req, res) => {
  const { name } = req.params;
  res.send(`Hello, ${name}!`);
});

// Start the server on port 3000
const port = 3000;
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

In this example, the route `/greet/:name` captures the value of `:name` from the URL. When you visit http://localhost:3000/greet/John, it responds with "Hello, John!"



**4.2 Route Methods:**

Express.js supports various HTTP request methods, such as GET, POST, PUT, DELETE, etc. You can use these methods to define how your application responds to different types of requests.

**Example:**

Let's create an example where we use different route methods to handle GET and POST requests. Update your `app.js` file:

```javascript
const express = require('express');
const app = express();

// Middleware to log request information
app.use((req, res, next) => {
  console.log(`Request received at ${new Date().toLocaleString()}`);
  next();
});

// Handling GET requests
app.get('/', (req, res) => {
  res.send('This is a GET request');
});

// Handling POST requests
app.post('/', (req, res) => {
  res.send('This is a POST request');
});

// Start the server on port 3000
const port = 3000;
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

In this example, the routes for GET and POST requests are defined using `app.get()` and `app.post()` methods, respectively. When you visit http://localhost:3000 with a browser, it responds with "This is a GET request." To simulate a POST request, you can use tools like cURL or Postman.

**4.3 Route Paths and Patterns:**

Express.js allows you to use regular expressions and pattern matching in route paths. This can be useful when you need more complex routing logic.

**Example:**

Let's create an example where we use a regular expression to match paths with a specific format. Update your `app.js` file:

```javascript
const express = require('express');
const app = express();

// Middleware to log request information
app.use((req, res, next) => {
  console.log(`Request received at ${new Date().toLocaleString()}`);
  next();
});

// Define a route with a regular expression pattern
app.get(/^\/users\/(\d+)$/, (req, res) => {
  const userId = req.params[0];
  res.send(`User ID: ${userId}`);
});

// Start the server on port 3000
const port = 3000;
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

In this example, the route path is defined using a regular expression `^\/users\/(\d+)$`, which matches paths like "/users/123" and captures the numeric user ID. When you visit http://localhost:3000/users/456, it responds with "User ID: 456."


**4.4 Route Middleware:**

Middleware functions in Express.js are functions that have access to the req, res, and next objects. They can perform tasks, modify request and response objects, and pass control to the next middleware in the stack.

**Example:**

javascript
Copy code
const express = require('express');
const app = express();

// Custom middleware to log request information
app.use((req, res, next) => {
  console.log(`Request received at ${new Date().toLocaleString()}`);
  next();
});

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
Here, the app.use() method registers a middleware function that logs information about each incoming request before passing control to the route handler.

**4.5 Route Stacks and Chaining:**

Middleware functions and route handlers can be organized into a stack, and the next() function is used to pass control to the next function in the stack. Middleware and route handlers can be chained together.

**Example:**

```javascript
const express = require('express');
const app = express();

// Middleware to log request information
app.use((req, res, next) => {
  console.log(`Request received at ${new Date().toLocaleString()}`);
  next();
});

// Route handler
app.get('/', (req, res) => {
  res.send('Hello, World!');
});

// Another middleware
app.use((req, res, next) => {
  console.log('This middleware runs after the route handler');
  next();
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

In this example, middleware functions and a route handler are part of the middleware stack, and they run in the order they are defined.







## 5. Middleware in Express.js

Middleware functions in Express.js are functions that have access to the `req` (request) and `res` (response) objects in the application's request-response cycle. Middleware functions can perform various tasks, modify request and response objects, and end the request-response cycle. They play a crucial role in Express.js applications by allowing you to execute code at different points during the handling of a request.

**5.1. Built-in Middleware:**

Express.js comes with several built-in middleware functions that perform common tasks. These functions can be used by invoking the `app.use()` method with the desired middleware function.

**Example - `express.static`:**

```javascript
const express = require('express');
const app = express();

// Serve static files from the 'public' directory
app.use(express.static('public'));

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

In this example, the `express.static` middleware serves static files from the "public" directory. Files in the "public" directory can be accessed directly from the browser. For instance, a file named `styles.css` in the "public" directory can be accessed at http://localhost:3000/styles.css.

**5.2. Third-party Middleware:**

Express.js allows you to use third-party middleware to extend the functionality of your application. Third-party middleware is typically available as npm packages. Popular examples include `body-parser` for parsing request bodies and `morgan` for logging.

**Example - `body-parser`:**

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const app = express();

// Parse incoming JSON requests
app.use(bodyParser.json());

// Route handling
app.post('/api/data', (req, res) => {
  const data = req.body;
  res.json({ receivedData: data });
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

In this example, the `body-parser` middleware is used to parse incoming JSON requests. The parsed JSON data is then accessible through `req.body` in the route handler.

**5.3. Writing Custom Middleware:**

You can create custom middleware functions to perform specific tasks for your application. A middleware function takes three arguments: `req`, `res`, and `next`. The `next` function is a callback that passes control to the next middleware function.

**Example - Custom Logging Middleware:**

```javascript
const express = require('express');
const app = express();

// Custom middleware for logging
const logger = (req, res, next) => {
  console.log(`Request received at ${new Date().toLocaleString()}`);
  next();
};

app.use(logger);

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

Here, the `logger` middleware logs the timestamp of each incoming request before passing control to the next middleware or route handler.

**5.4. Error-handling Middleware:**

Error-handling middleware functions have four arguments instead of three (`err`, `req`, `res`, `next`). They are used to catch errors during the request-response cycle. If an error occurs, the control is passed to the next error-handling middleware.

**Example:**

```javascript
const express = require('express');
const app = express();

// Custom middleware for logging
const logger = (req, res, next) => {
  console.log(`Request received at ${new Date().toLocaleString()}`);
  next();
};

// Error-handling middleware
const errorHandler = (err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something went wrong!');
};

app.use(logger);
app.use(errorHandler);

app.get('/', (req, res) => {
  throw new Error('Simulated error');
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

In this example, the `errorHandler` middleware catches any errors thrown during the request processing and sends a generic error response with a 500 status code.

Understanding middleware is essential for creating modular and maintainable Express.js applications. In practice, middleware allows you to add functionality to your application in a clean and organized way.





## 6. Request and Response Handling in Express.js

Express.js provides powerful tools for handling incoming requests and generating responses. In this section, we'll explore various aspects of request and response handling.

**6.1 Parsing Request Data:**

**Parsing JSON and Form Data:**

Express.js allows you to parse different types of data from incoming requests, such as JSON and form data. The `body-parser` middleware, which is now part of the Express.js package, is commonly used for this purpose.

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const app = express();

// Parse incoming JSON requests
app.use(bodyParser.json());

// Parse incoming form data
app.use(bodyParser.urlencoded({ extended: true }));

app.post('/api/data', (req, res) => {
  const jsonData = req.body; // Access JSON data
  const formData = req.body.formField; // Access form data
  res.json({ receivedData: { jsonData, formData } });
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

In this example, the `body-parser` middleware is used to parse incoming JSON and form data. The parsed data is then accessible through `req.body` in the route handler.

**6.2 Sending Responses:**

**Sending JSON Responses:**

Express.js makes it easy to send JSON responses using the `res.json()` method.

```javascript
const express = require('express');
const app = express();

app.get('/api/data', (req, res) => {
  const responseData = { message: 'Hello, JSON!' };
  res.json(responseData);
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

In this example, the route handler responds with a JSON object. The `res.json()` method automatically sets the appropriate `Content-Type` header.

**Sending HTML Responses:**

You can also send HTML responses using the `res.send()` method.

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  const htmlContent = '<h1>Hello, HTML!</h1>';
  res.send(htmlContent);
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

Here, the route handler responds with an HTML string. The `res.send()` method sets the `Content-Type` header based on the provided content.

**6.3 Cookies and Sessions:**

Express.js provides middleware like `cookie-parser` to work with cookies. Additionally, for sessions, you can use packages like `express-session`.

**Example - Using `cookie-parser`:**

```javascript
const express = require('express');
const cookieParser = require('cookie-parser');
const app = express();

app.use(cookieParser());

app.get('/set-cookie', (req, res) => {
  res.cookie('user', 'John Doe');
  res.send('Cookie set!');
});

app.get('/get-cookie', (req, res) => {
  const username = req.cookies.user || 'Guest';
  res.send(`Hello, ${username}!`);
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

In this example, the `cookie-parser` middleware is used to parse and set cookies. The `/set-cookie` route sets a cookie, and the `/get-cookie` route reads and uses the cookie.

**6.4 File Uploads:**

Handling file uploads in Express.js often involves using a middleware like `multer`.

**Example - Using `multer`:**

```javascript
const express = require('express');
const multer = require('multer');
const app = express();

// Set up multer for handling file uploads
const storage = multer.diskStorage({
  destination: (req, file, cb) => {
    cb(null, 'uploads/');
  },
  filename: (req, file, cb) => {
    cb(null, file.originalname);
  },
});

const upload = multer({ storage: storage });

app.post('/upload', upload.single('file'), (req, res) => {
  res.send('File uploaded successfully!');
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

In this example, the `multer` middleware is used to handle file uploads. The `upload.single('file')` middleware processes a single file upload with the field name 'file'. The uploaded file is then available in the `req.file` object.



## 7. Views and Templates in Express.js

Express.js supports the use of template engines to generate dynamic HTML content on the server side. This allows you to create reusable templates and inject data into them before sending the HTML to the client. In this section, we'll explore how to integrate template engines, render views, and work with template variables.

**7.1 Integrating Template Engines:**

Express.js supports various template engines, including EJS (Embedded JavaScript) and Handlebars. For demonstration purposes, let's focus on EJS.

**Example - Integrating EJS:**

**7.1.1. Install the EJS package:**

```bash
npm install ejs
```

**7.1.2. Set up EJS in your Express application:**

```javascript
const express = require('express');
const app = express();

// Set 'views' as the directory for templates
app.set('views', __dirname + '/views');

// Set EJS as the view engine
app.set('view engine', 'ejs');

// Example route rendering an EJS view
app.get('/ejs-example', (req, res) => {
  const data = { message: 'Hello from EJS!' };
  res.render('ejs-example', { data });
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

**7.1.3. Create an EJS template (e.g., `views/ejs-example.ejs`):**

```ejs
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>EJS Example</title>
</head>
<body>
  <h1><%= data.message %></h1>
</body>
</html>
```

In this example, the `app.set()` method is used to configure Express to use EJS as the view engine. The `res.render()` method is then used to render the `ejs-example.ejs` template, passing the `data` object to inject dynamic content.

**7.2 Rendering Views:**

Once you've set up a template engine, rendering views is straightforward using the `res.render()` method.

**Example:**

```javascript
const express = require('express');
const app = express();

// Set 'views' as the directory for templates
app.set('views', __dirname + '/views');

// Set EJS as the view engine
app.set('view engine', 'ejs');

// Example route rendering a view
app.get('/example', (req, res) => {
  const data = { message: 'Hello from Express!' };
  res.render('example', { data });
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

In this example, a template named `example.ejs` in the `views` directory is rendered using the `res.render()` method.

**7.3 Template Variables:**

Template engines allow you to pass variables from your route handlers to your views. These variables can then be used to dynamically generate HTML content.

**Example:**

```javascript
const express = require('express');
const app = express();

// Set 'views' as the directory for templates
app.set('views', __dirname + '/views');

// Set EJS as the view engine
app.set('view engine', 'ejs');

// Example route with template variables
app.get('/user/:id', (req, res) => {
  const userId = req.params.id;
  const userData = getUserData(userId); // Assume a function to get user data
  res.render('user-profile', { user: userData });
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```


In this example, the route handler retrieves user data based on the `userId` parameter and passes it to the `user-profile.ejs` template as a variable named `user`. The template can then use `<%= user.name %>` to display the user's name, for example.



## 8. Database Integration in Express.js

Integrating databases with Express.js is a crucial aspect of building dynamic and data-driven web applications. In this section, we'll explore connecting to databases, using Object-Relational Mapping (ORM) libraries, and performing CRUD (Create, Read, Update, Delete) operations.

**8.1 Connecting to Databases:**

Express.js can connect to various types of databases, and two popular choices are MongoDB (a NoSQL database) and MySQL (a relational database). We'll cover both.

**MongoDB with Mongoose:**

**8.1.1. Install the required packages:**

```bash
npm install mongoose
```

**8.1.2. Set up the connection in your Express app:**

```javascript
const express = require('express');
const mongoose = require('mongoose');
const app = express();

// Connect to MongoDB
mongoose.connect('mongodb://localhost:27017/mydatabase', { useNewUrlParser: true, useUnifiedTopology: true });

const db = mongoose.connection;

db.on('error', console.error.bind(console, 'MongoDB connection error:'));
db.once('open', () => {
  console.log('Connected to MongoDB');
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

**MySQL with Sequelize:**

**1. Install the required packages:**

```bash
npm install sequelize mysql2
```

**2. Set up the connection in your Express app:**

```javascript
const express = require('express');
const { Sequelize, DataTypes } = require('sequelize');
const app = express();

// Connect to MySQL
const sequelize = new Sequelize('database', 'username', 'password', {
  host: 'localhost',
  dialect: 'mysql',
});

(async () => {
  try {
    await sequelize.authenticate();
    console.log('Connected to MySQL');
  } catch (error) {
    console.error('Unable to connect to MySQL:', error);
  }
})();

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```


**8.2 Using an ORM:**

ORMs (Object-Relational Mapping) simplify database interactions by allowing you to work with JavaScript objects instead of raw SQL queries. Two popular ORMs for Express.js are Mongoose (for MongoDB) and Sequelize (for SQL databases).

**Mongoose for MongoDB:**

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

// Define a schema
const userSchema = new Schema({
  name: String,
  email: String,
});

// Create a model
const User = mongoose.model('User', userSchema);

// Example: Create a new user
const newUser = new User({ name: 'John Doe', email: 'john@example.com' });
newUser.save((err, user) => {
  if (err) throw err;
  console.log('User created:', user);
});
```

**Sequelize for MySQL:**

```javascript
const { Sequelize, DataTypes } = require('sequelize');

// Define a model
const User = sequelize.define('User', {
  name: {
    type: DataTypes.STRING,
    allowNull: false,
  },
  email: {
    type: DataTypes.STRING,
    allowNull: false,
  },
});

// Example: Create a new user
(async () => {
  try {
    await sequelize.sync(); // Create tables if they don't exist
    const newUser = await User.create({ name: 'John Doe', email: 'john@example.com' });
    console.log('User created:', newUser.toJSON());
  } catch (error) {
    console.error('Error creating user:', error);
  }
})();
```

**8.3 CRUD Operations with Databases:**

Once connected to a database and set up with an ORM, you can perform CRUD operations.

**Example - CRUD with Mongoose (MongoDB):**

```javascript
// Create
const newUser = new User({ name: 'Jane Doe', email: 'jane@example.com' });
newUser.save((err, user) => {
  if (err) throw err;
  console.log('User created:', user);
});

// Read
User.find({}, (err, users) => {
  if (err) throw err;
  console.log('All users:', users);
});

// Update
User.updateOne({ name: 'John Doe' }, { email: 'john.doe@example.com' }, (err, result) => {
  if (err) throw err;
  console.log('User updated:', result);
});

// Delete
User.deleteOne({ name: 'Jane Doe' }, (err) => {
  if (err) throw err;
  console.log('User deleted');
});
```

**Example - CRUD with Sequelize (MySQL):**

```javascript
// Create
(async () => {
  try {
    const newUser = await User.create({ name: 'Jane Doe', email: 'jane@example.com' });
    console.log('User created:', newUser.toJSON());
  } catch (error) {
    console.error('Error creating user:', error);
  }
})();

// Read
(async () => {
  try {
    const users = await User.findAll();
    console.log('All users:', users.map((user) => user.toJSON()));
  } catch (error) {
    console.error('Error fetching users:', error);
  }
})();

// Update
(async () => {
  try {
    const [updatedRows] = await User.update({ email: 'john.doe@example.com' }, { where: { name: 'John Doe' } });
    console.log('User updated:', updatedRows);
  } catch (error) {
    console.error('Error updating user:', error);
  }
})();

// Delete
(async () => {
  try {
    const deletedRows = await User.destroy({ where: { name: 'Jane Doe' } });
    console.log('User deleted:', deletedRows);
  } catch (error) {
    console.error('Error deleting user:', error);
  }
})();
```

Understanding how to connect to databases, use ORMs, and perform CRUD operations is essential for building data-driven applications with Express.js. The examples provided cover MongoDB with Mongoose and MySQL with Sequelize, but similar principles apply to other databases and ORMs.





## 9. Authentication and Authorization in Express.js

Authentication and authorization are crucial aspects of web applications to ensure secure access and protect sensitive information. In this section, we'll explore integrating Passport.js for authentication, using JSON Web Tokens (JWT) for token-based authorization, and implementing role-based access control.

**9.1 Passport.js Integration:**

Passport.js is a widely used authentication middleware for Node.js applications. It supports various authentication strategies, including local username/password, OAuth, and more.

**Example - Local Authentication with Passport.js:**

**1. Install the required packages:**

```bash
npm install express passport passport-local express-session
```

**2. Set up Passport.js in your Express app:**

```javascript
const express = require('express');
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;
const expressSession = require('express-session');
const app = express();

// Set up express-session for session management
app.use(expressSession({ secret: 'secret-key', resave: false, saveUninitialized: false }));

// Initialize Passport.js
app.use(passport.initialize());
app.use(passport.session());

// Configure local strategy
passport.use(new LocalStrategy(
  (username, password, done) => {
    // Replace this with your actual user authentication logic
    if (username === 'user' && password === 'password') {
      return done(null, { id: 1, username: 'user' });
    } else {
      return done(null, false, { message: 'Invalid credentials' });
    }
  }
));

// Serialize and deserialize user
passport.serializeUser((user, done) => {
  done(null, user.id);
});

passport.deserializeUser((id, done) => {
  // Replace this with your actual user retrieval logic
  const user = { id: 1, username: 'user' };
  done(null, user);
});

// Example route for login
app.post('/login',
  passport.authenticate('local', { successRedirect: '/', failureRedirect: '/login', failureFlash: true })
);

// Example route for protected resource
app.get('/profile', isAuthenticated, (req, res) => {
  res.send(`Welcome, ${req.user.username}!`);
});

// Function to check if the user is authenticated
function isAuthenticated(req, res, next) {
  if (req.isAuthenticated()) {
    return next();
  }
  res.redirect('/login');
}

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

**9.2 JSON Web Tokens (JWT):**

JSON Web Tokens (JWT) are a compact, URL-safe means of representing claims between two parties. They can be used for authorization by exchanging tokens between the client and server.

**Example - Generating and Verifying JWTs:**

**1. Install the required packages:**

```bash
npm install express jsonwebtoken express-jwt
```

**2. Set up JWT in your Express app:**

```javascript
const express = require('express');
const jwt = require('jsonwebtoken');
const expressJwt = require('express-jwt');
const app = express();

// Secret key for signing and verifying JWTs
const secretKey = 'your-secret-key';

// Example route for generating a JWT
app.get('/generate-token', (req, res) => {
  const payload = { userId: 1, username: 'user' };
  const token = jwt.sign(payload, secretKey, { expiresIn: '1h' });
  res.json({ token });
});

// Example route for verifying a JWT
app.get('/protected-resource', expressJwt({ secret: secretKey }), (req, res) => {
  res.json({ message: 'This is a protected resource' });
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

**9.3 Role-Based Access Control:**

Role-based access control (RBAC) is a method of regulating access to computer or network resources based on the roles of individual users.

**Example - Implementing RBAC:**

```javascript
const express = require('express');
const app = express();

// Example middleware for role-based access control
function hasRole(role) {
  return (req, res, next) => {
    // Replace this with your actual role-checking logic
    const userRoles = ['admin', 'user'];
    if (userRoles.includes(role)) {
      next();
    } else {
      res.status(403).send('Permission denied');
    }
  };
}

// Example route with role-based access control
app.get('/admin-dashboard', hasRole('admin'), (req, res) => {
  res.send('Admin Dashboard');
});

app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

In this example, the `hasRole` middleware checks if the user has the specified role before allowing access to the route.






## 10. Middleware for Advanced Features in Express.js

Middleware in Express.js can be leveraged for advanced features that enhance the functionality and performance of web applications. In this section, we'll explore middleware for handling WebSockets, compression, and caching.

**10.1 WebSockets:**

WebSockets provide a full-duplex communication channel over a single, long-lived connection. Express.js can be extended with middleware to handle WebSocket connections.

**Example - WebSockets with `socket.io`:**

**1. Install the required packages:**

```bash
npm install express socket.io
```

**2. Set up WebSocket support in your Express app:**

```javascript
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = socketIO(server);

// Serve static files
app.use(express.static('public'));

// Set up a WebSocket connection
io.on('connection', (socket) => {
  console.log('A user connected');

  // Listen for messages from the client
  socket.on('chat message', (msg) => {
    console.log(`Message: ${msg}`);
    // Broadcast the message to all connected clients
    io.emit('chat message', msg);
  });

  // Disconnect event
  socket.on('disconnect', () => {
    console.log('User disconnected');
  });
});

// Start the server
server.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

**3. Create a basic HTML file (e.g., `public/index.html`):**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>WebSocket Example</title>
</head>
<body>
  <ul id="messages"></ul>
  <form id="form" action="">
    <input id="m" autocomplete="off" /><button>Send</button>
  </form>

  <script src="/socket.io/socket.io.js"></script>
  <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
  <script>
    $(function () {
      var socket = io();

      $('form').submit(function () {
        socket.emit('chat message', $('#m').val());
        $('#m').val('');
        return false;
      });

      socket.on('chat message', function (msg) {
        $('#messages').append($('<li>').text(msg));
      });
    });
  </script>
</body>
</html>
```

This example sets up a simple chat application using WebSockets with `socket.io`. When a user sends a message, it is broadcasted to all connected clients in real-time.

**10.2 Compression:**

Compression middleware can reduce the size of responses, improving the speed of data transfer between the server and clients.

**Example - Compression with `compression` middleware:**

**1. Install the required package:**

```bash
npm install express compression
```

**2. Set up compression in your Express app:**

```javascript
const express = require('express');
const compression = require('compression');

const app = express();

// Use compression middleware
app.use(compression());

// Route handling
app.get('/', (req, res) => {
  res.send('This response will be compressed.');
});

// Start the server
app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

In this example, the `compression` middleware is used to compress responses. This can significantly reduce the size of assets like HTML, CSS, and JavaScript.

**10.3 Caching:**

Caching middleware can improve performance by storing and serving previously generated responses.

**Example - Caching with `helmet` middleware:**

**1. Install the required package:**

```bash
npm install express helmet
```

**2. Set up caching in your Express app:**

```javascript
const express = require('express');
const helmet = require('helmet');

const app = express();

// Use helmet middleware for security and caching headers
app.use(helmet());

// Route handling
app.get('/', (req, res) => {
  // Set cache control headers
  res.set('Cache-Control', 'public, max-age=86400'); // Cache for 24 hours
  res.send('This response is cached.');
});

// Start the server
app.listen(3000, () => {
  console.log('Server is running on http://localhost:3000');
});
```

In this example, the `helmet` middleware is used to set caching headers. The `Cache-Control` header instructs clients to cache the response for a specified duration.





## 11. Deployment and Production 

**Considerations in Express.js**

Deploying an Express.js application involves considerations for environment variables, setting up a reverse proxy, and optimizing performance. These steps are crucial for a smooth transition from development to production. Let's explore each aspect with code examples.

**11.1 Environment Variables:**

Environment variables allow you to configure your application differently based on the environment it's running in (e.g., development, testing, production). They are essential for managing sensitive information and application configurations.

**Example - Using Environment Variables:**

**Create a `.env` file in your project's root directory:**

```env
PORT=3000
DATABASE_URL=mongodb://localhost:27017/mydatabase
SECRET_KEY=mysecretkey
```

**Install the `dotenv` package to load environment variables:**

```bash
npm install dotenv
```

**Modify your `app.js` or `index.js` file:**

```javascript
// Import dotenv and load environment variables
require('dotenv').config();

const express = require('express');
const app = express();

// Use environment variables
const port = process.env.PORT || 3000;
const databaseUrl = process.env.DATABASE_URL || 'mongodb://localhost:27017/default';
const secretKey = process.env.SECRET_KEY || 'mysecret';

// ... rest of your code ...

// Start the server
app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

**11.2 Reverse Proxy Setup:**

In a production environment, it's common to use a reverse proxy like Nginx or Apache to handle tasks such as load balancing, SSL termination, and serving static files.

**Example - Nginx Configuration:**

Assuming your Express.js app is running on `http://localhost:3000`, configure Nginx to act as a reverse proxy:

```nginx
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

**11.3 Performance Optimization:**

Optimizing performance is crucial for delivering a responsive and efficient application. Consider techniques such as compression, caching, and using a process manager like PM2.

**Example - Using PM2 for Process Management:**

Install PM2 globally:

```bash
npm install -g pm2
```

Run your Express.js app using PM2:

```bash
pm2 start your-app.js
```

PM2 provides features like automatic restarts, logging, and process monitoring.



## 12. API Development in Express.js

API development is a critical aspect of many web applications, allowing them to communicate with each other or with front-end clients. In this section, we'll cover RESTful API design, versioning, and documentation using tools like Swagger.

**12.1 RESTful API Design:**

RESTful APIs adhere to the principles of Representational State Transfer (REST) and provide a standard way to expose resources and perform operations on those resources.

**Example - Basic RESTful API:**

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const app = express();
const port = 3000;

app.use(bodyParser.json());

// Sample data (in-memory database)
let users = [
  { id: 1, name: 'John Doe' },
  { id: 2, name: 'Jane Doe' },
];

// Get all users
app.get('/api/users', (req, res) => {
  res.json(users);
});

// Get a specific user by ID
app.get('/api/users/:id', (req, res) => {
  const userId = parseInt(req.params.id);
  const user = users.find((u) => u.id === userId);

  if (!user) {
    res.status(404).json({ error: 'User not found' });
  } else {
    res.json(user);
  }
});

// Create a new user
app.post('/api/users', (req, res) => {
  const newUser = req.body;
  newUser.id = users.length + 1;
  users.push(newUser);
  res.status(201).json(newUser);
});

// Update an existing user
app.put('/api/users/:id', (req, res) => {
  const userId = parseInt(req.params.id);
  const updatedUser = req.body;
  users = users.map((u) => (u.id === userId ? updatedUser : u));

  res.json(updatedUser);
});

// Delete a user
app.delete('/api/users/:id', (req, res) => {
  const userId = parseInt(req.params.id);
  users = users.filter((u) => u.id !== userId);
  res.json({ message: 'User deleted successfully' });
});

app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

This basic example demonstrates CRUD operations (Create, Read, Update, Delete) for a resource (users). Adjust and expand the routes based on your API's needs.

**12.2 Versioning:**

Versioning allows you to make changes to your API while ensuring backward compatibility for existing clients. There are different approaches to versioning, including path-based and header-based versioning.

**Example - Path-Based Versioning:**

```javascript
// Version 1
app.get('/api/v1/users', (req, res) => {
  res.json(users);
});

// Version 2
app.get('/api/v2/users', (req, res) => {
  // New implementation for version 2
  res.json(users.map((user) => ({ id: user.id, fullName: user.name })));
});
```

**12.3 Documentation using Swagger:**

Swagger is a popular tool for API documentation. It allows you to describe, document, and visualize your APIs.

**Example - Swagger Documentation with `swagger-jsdoc` and `swagger-ui-express`:**

**Install the required packages:**

```bash
npm install swagger-jsdoc swagger-ui-express
```

**Set up Swagger documentation in your Express app:**

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const swaggerJsdoc = require('swagger-jsdoc');
const swaggerUi = require('swagger-ui-express');
const app = express();
const port = 3000;

app.use(bodyParser.json());

// Define Swagger options
const swaggerOptions = {
  definition: {
    openapi: '3.0.0',
    info: {
      title: 'Express API with Swagger',
      version: '1.0.0',
      description: 'A sample API with Swagger documentation',
    },
  },
  apis: ['app.js'], // Point to the file containing the routes
};

// Initialize Swagger-jsdoc
const swaggerSpec = swaggerJsdoc(swaggerOptions);

// Serve Swagger UI
app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerSpec));

/**
 * @swagger
 * /api/users:
 *   get:
 *     summary: Get all users
 *     responses:
 *       200:
 *         description: Successful response with user data
 */
app.get('/api/users', (req, res) => {
  res.json(users);
});

// ... other API routes ...

app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

This example includes Swagger documentation for the `/api/users` route. Visit `http://localhost:3000/api-docs` to access the Swagger UI.

Remember to customize the Swagger options and documentation according to your API's structure and requirements.




## 13. Scaling Express.js Applications

Scaling an Express.js application involves handling increased traffic and ensuring the application's availability and performance. In this section, we'll explore scaling options, including load balancing, a microservices architecture, and containerization with Docker.

**13.1 Load Balancing:**

Load balancing is a technique used to distribute incoming network traffic across multiple servers to ensure no single server becomes a bottleneck. In Express.js, you can achieve load balancing by running multiple instances of your application and using a load balancer.

**Example - Load Balancing with `pm2`:**

Assuming you have an Express.js application (`app.js`), you can use the `pm2` process manager to run multiple instances:

**Install `pm2` globally:**

```bash
npm install -g pm2
```

**Run multiple instances of your application:**

```bash
pm2 start app.js -i max
```

This command starts as many instances as there are CPU cores on your machine (`-i max`). `pm2` handles load balancing between the instances.

**13.2 Microservices Architecture:**

Microservices architecture involves breaking down a large application into smaller, independently deployable services, each responsible for a specific business capability.

**Example - Microservices Communication:**

Assuming you have two Express.js microservices (`user-service` and `order-service`), you can use HTTP requests or a message broker for communication.

**1. HTTP Communication:**

   ```javascript
   // user-service.js
   const express = require('express');
   const app = express();
   const port = 3001;

   app.get('/api/users/:userId', (req, res) => {
     const userId = req.params.userId;
     // Fetch user information from the database
     res.json({ userId, name: 'John Doe' });
   });

   app.listen(port, () => {
     console.log(`User service is running on http://localhost:${port}`);
   });
   ```

   ```javascript
   // order-service.js
   const express = require('express');
   const axios = require('axios');
   const app = express();
   const port = 3002;

   app.get('/api/orders/:orderId', async (req, res) => {
     const orderId = req.params.orderId;
     // Fetch order information from the database
     const order = { orderId, total: 100 };
     
     // Fetch user information from the user-service
     const userId = '123';
     const user = await axios.get(`http://localhost:3001/api/users/${userId}`);
     order.user = user.data;

     res.json(order);
   });

   app.listen(port, () => {
     console.log(`Order service is running on http://localhost:${port}`);
   });
   ```

**2. Message Broker Communication (using RabbitMQ):**

   ```javascript
   // user-service.js
   const express = require('express');
   const amqp = require('amqplib');
   const app = express();
   const port = 3001;

   // Connect to RabbitMQ
   const connect = async () => {
     const connection = await amqp.connect('amqp://localhost');
     const channel = await connection.createChannel();
     const queue = 'user_queue';

     channel.assertQueue(queue, { durable: false });

     channel.consume(queue, (msg) => {
       const userId = msg.content.toString();
       // Fetch user information from the database
       channel.sendToQueue(msg.properties.replyTo, Buffer.from(JSON.stringify({ userId, name: 'John Doe' })));
       channel.ack(msg);
     });
   };

   connect();

   app.listen(port, () => {
     console.log(`User service is running on http://localhost:${port}`);
   });
   ```

   ```javascript
   // order-service.js
   const express = require('express');
   const amqp = require('amqplib');
   const app = express();
   const port = 3002;

   // Connect to RabbitMQ
   const connect = async () => {
     const connection = await amqp.connect('amqp://localhost');
     const channel = await connection.createChannel();
     const queue = 'user_queue';

     channel.assertQueue(queue, { durable: false });

     app.get('/api/orders/:orderId', async (req, res) => {
       const orderId = req.params.orderId;
       // Fetch order information from the database
       const order = { orderId, total: 100 };

       // Fetch user information from the user-service via RabbitMQ
       const userId = '123';
       channel.sendToQueue(queue, Buffer.from(userId), { replyTo: 'order_queue' });
       
       const user = await new Promise((resolve) => {
         channel.consume('order_queue', (msg) => {
           const userData = JSON.parse(msg.content.toString());
           resolve(userData);
         });
       });

       order.user = user;
       res.json(order);
     });
   };

   connect();

   app.listen(port, () => {
     console.log(`Order service is running on http://localhost:${port}`);
   });
   ```

**13.3 Containerization with Docker:**

Docker allows you to containerize your applications, providing consistency and portability across different environments.

**Example - Dockerizing an Express.js App:**

**Assuming you have an Express.js application (`app.js`), create a `Dockerfile`:**

```Dockerfile
# Use the official Node.js image as a base image
FROM node:14

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install app dependencies
RUN npm install

# Copy the application code to the container
COPY . .

# Expose the port on which the app will run
EXPOSE 3000

# Command to run the application
CMD ["node", "app.js"]
```

**Build the Docker image:**

```bash
docker build -t my-express-app .
```

**Run the Docker container:**

```bash
docker run -p 3000:3000 my-express-app
```



## 14. Assignment 

**Task1: Create a REST API for Netflix users** 

**Desired Output:**

![AltImage](https://i.postimg.cc/D0WwWhvb/image.png)

**Consider the following file structure:**

![AltImage](https://i.postimg.cc/gj06N1YY/image.png)


For this file structure create a project folder and open with it VS code, Now run the following commands in the terminal of VS Code:

```bash
npm init
``` 

```bash
npm i  express
```

**And write the following code in the respective files:**

**Index.js**

```javascript

const express = require("express");
const app = express();
const users = require('./MOCK_DATA.json')
const PORT = 8000;




app.get('/api/users', (req, res)=>{
    return res.json(users)
})


app.get('/users', (req, res)=>{
    const html = `
    <ul>${users.map(user => `<li>${user.first_name}</li>`).join("")}</ul>
    `;
    res.send(html)
})


app.listen(PORT, ()=>{
    console.log(`Server started at PORT : ${PORT}`)
})
```

For MOCK_DATA.json you can visit https://www.mockaroo.com/ and get the dataset from there.

 

**Task2: In the same API add a feature so that individual records can be fetched as well**


**Desired Output:**



![AltImage](https://i.postimg.cc/DZSSGL5Z/image.png)



