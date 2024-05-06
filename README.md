# BACKEND

Certainly! Let's dive into each of the topics in more detail, providing comprehensive explanations and examples.


# Comprehensive Guide to Node.js

## 1. Introduction to Node.js

Node.js is an open-source, cross-platform runtime environment designed for executing JavaScript code outside the browser. It utilizes the V8 JavaScript engine and supports server-side scripting, making it ideal for constructing scalable and efficient network applications.

## 2. Installing Node.js

### Instructions:

1. Visit the official [Node.js website](https://nodejs.org/).
2. Download the suitable installer for your operating system (Windows, macOS, Linux).
3. Execute the installer and adhere to the installation instructions.

### Verification:

After installation, confirm by running the following commands in your terminal:

```docs
node -v
npm -v
```

## 3. Node.js REPL (Read-Eval-Print Loop)

Node.js provides a built-in interactive environment, the REPL, allowing real-time experimentation with JavaScript code. To access the REPL, open your terminal and type `node`. A prompt (>) will appear, enabling you to input JavaScript expressions and observe immediate output.

### Example:

```javascript
> 2 + 3
5
> const greeting = "Hello, Node.js!"
undefined
> greeting
'Hello, Node.js!'
```

To exit the REPL, press Ctrl + C twice or type `.exit`.

## 4. Working with Node.js Files

Node.js enables the creation and execution of JavaScript files. Save your code in a .js file and run it using the `node` command followed by the file name.

### Example (hello.js):

```javascript
console.log("Hello, Node.js!");
```

Execute the file in your terminal:

```docs
node hello.js
```

## 5. The Node.js Process Object

The `process` object provides information and control over the Node.js process, facilitating interaction with the current process, environment variables, and more.

### Example:

```javascript
console.log("Process ID:", process.pid);
console.log("Node.js Version:", process.version);
console.log("Platform:", process.platform);
```

## 6. Node.js Process.argv

In Node.js, the `process.argv` property is an array storing command-line arguments passed to a Node.js script, including the Node.js executable path and the script being run, along with any additional arguments.

### Example (myScript.js):

```javascript
// myScript.js
console.log(process.argv);
```

When running `node myScript.js arg1 arg2`, `process.argv` will be `['node', 'myScript.js', 'arg1', 'arg2']`.

This array proves useful for accessing and manipulating command-line inputs in Node.js applications.

## 7. Exporting and Importing in Node.js Files

In Node.js, code can be divided across multiple files using `module.exports` and `exports` mechanisms to share code.

### Example (math.js):

```javascript
// math.js
module.exports = {
  add: (a, b) => a + b,
  subtract: (a, b) => a - b
};
```

Equivalent using `exports`:

```javascript
// exports.add = (a, b) => a + b;
// exports.subtract = (a, b) => a - b;
```

In the main.js file:

```javascript
const math = require('./math');
console.log(math.add(5, 3));       // Output: 8
console.log(math.subtract(10, 4)); // Output: 6
```

This approach allows importing functions from math.js regardless of whether `module.exports` or `exports` was used for exporting in math.js.

## 8. Exporting and Importing from Directories

Related files can be organized in directories, utilizing an index.js file to export from the directory.

### Example (utils/index.js):

```javascript
// utils/index.js
exports.math = require('./math');
exports.strings = require('./strings');
```

In the main.js file:

```javascript
const utils = require('./utils');
console.log(utils.math.add(7, 2));
console.log(utils.strings.capitalize('node.js'));
```

This structured approach aids in managing larger projects effectively.

## 9. Understanding npm (Node Package Manager)

`npm` is the default package manager for Node.js, providing access to a vast ecosystem of open-source packages and tools.

## 10. Installing and Managing Packages

To install a package using npm:

```docs
npm install package-name
```

To install a package globally:

```docs
npm install -g package-name
```

To uninstall a package:

```docs
npm uninstall package-name
```

## 11. package.json and Dependency Management

The `package.json` file contains metadata about your project and its dependencies. It is crucial for managing project dependencies and scripts.

To create a `package.json` file:

```docs
npm init
```

## 12. Local vs Global Package Installation

Local installation (`npm install package-name`) installs packages in the current project. Global installation (`npm install -g package-name`) installs packages globally on your system.

## 13. Importing External Modules

To import a specific function or variable from a module, use the import statement, a feature of ECMAScript modules (ESM) introduced in later Node.js versions.

### Example (main.js):

```javascript
import { sum } from "./math.js"; // Importing the 'sum' function from math.js

const result = sum(5, 3); // Using the imported 'sum' function
console.log(result);
```

In the math.js file:

```javascript
// math.js
export function sum(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}
```

Ensure ESM (ECMAScript modules) functionality by specifying `"type": "module"` in your `package.json` file:

```json
{
  "type": "module",
  "dependencies": {
    // Your dependencies here
  }
}
```

Note: Using import and export is part of the ECMAScript module system and may not be fully supported in older Node.js versions without additional configurations. In such cases, the CommonJS require and module.exports pattern (as explained in point 6) is commonly used.

Node.js is a powerful platform empowering developers to build a wide range of applications. Understanding its core concepts and tools like npm is essential for efficient development.


---------------------------------------------------------------------------------------


# Express.js In-Depth Notes

## What is Express.js?

Express.js is a minimal and flexible web application framework built on Node.js. It provides a robust set of features for developing web and mobile applications. Express.js simplifies the creation of scalable, maintainable server-side applications by offering an intuitive API for handling HTTP requests, managing routes, and incorporating middleware.

## Getting Started with Express.js

### Steps:

1. **Initialize Your Project:**
   - Create a new project directory and navigate to it in your terminal.
   - Run the following command to initialize a new Node.js project:

     ```docs
     npm init -y
     ```

2. **Install Express:**
   - Install Express.js as a dependency using npm:

     ```docs
     npm install express
     ```

3. **Create Your Server:**
   - Define and configure your Express application in a file (e.g., app.js):

     ```javascript
     const express = require('express');
     const app = express();
     const PORT = 3000;

     app.listen(PORT, () => {
       console.log(`Server is running on port ${PORT}`);
     });
     ```

4. **Run Your Server:**
   - In the terminal, run your Express application:

     ```docs
     node app.js
     ```

   - You should see the message "Server is running on port 3000" in the terminal.

## Handling Requests in Express.js

Express.js allows you to define routes to handle different HTTP methods and request URLs.

### Basic Route Handling

Create route handlers using `app.get()`, `app.post()`, `app.put()`, `app.use()`, etc. methods:

```javascript
app.use('/about', (req, res) => { res.send('Welcome to the About Page'); });

app.get('/', (req, res) => {
  res.send('Hello, Express!');
});

app.post('/submit', (req, res) => {
  res.send('Form submitted');
});
```

### Catch-All Route

Handle unmatched routes using a catch-all route:

```javascript
app.get('*', (req, res) => {
  res.status(404).send('Page not found');
});
```

### Sending Responses

You can send various types of responses using `res` object methods.

#### Sending HTML Response

```javascript
app.get('/html', (req, res) => {
  res.send('<h1>Hello, Express!</h1>');
});
```

#### Sending JSON Response

```javascript
app.get('/json', (req, res) => {
  res.json({ message: 'Hello, Express in JSON!' });
});
```

## Routing in Express.js

Organize your routes for better maintainability.

### Creating Router Instances

In a separate file (e.g., routes.js):

```javascript
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  res.send('Home Page');
});

module.exports = router;
```

In your main app.js file:

```javascript
const routes = require('./routes');
app.use('/', routes);
```

## Installing Nodemon

Nodemon restarts the server automatically when code changes are detected, making development smoother.

### Install Nodemon Globally

```docs
npm install -g nodemon
```

### Use Nodemon

Replace the `node` command with `nodemon` to run your server:

```docs
nodemon app.js
```

## Path Parameters

Path parameters in Node.js Express allow you to extract dynamic values from the URL, enabling flexible routing and data retrieval.

```javascript
// Define a route with a path parameter
app.get('/users/:id', (req, res) => {
  const userId = req.params.id;
  // Use userId for data retrieval or processing
});
```

Path parameters enhance the versatility of your Express routes, making it easy to handle various requests with a single route handler.

## Query Strings

Access query parameters from the URL.

```javascript
app.get('/search', (req, res) => {
  const query = req.query.q;
  res.send(`Search Query: ${query}`);
});
```

These detailed Express.js notes cover various aspects of building web applications, including handling requests, routing, response handling, and key concepts like path parameters and query strings. By following these steps and examples, you'll be well-equipped to start creating powerful server-side applications using Express.js.


---------------------------------------------------------------------------------------


# Node: EJS (Embedded JavaScript) - Templating Engine

## What is Templating?

Templating is a technique used in web development to dynamically generate HTML content. It allows developers to separate the structure of a web page from its data, making it easier to manage and maintain.

## Using EJS (Embedded JavaScript)

EJS is a popular templating engine for Node.js that allows you to embed JavaScript code within your HTML templates.

### Installation

Install EJS using npm (Node Package Manager) in your Node.js project:

```docs
npm install ejs
```

### Views Directory

To use EJS, create a directory for your views/templates. Conventionally, this directory is named "views."

```javascript
const express = require("express");
const app = express();
const path = require("path");
const port = 8080;

app.set('view engine', 'ejs'); // Set EJS as the view engine
app.set('views', path.join(__dirname, "/views")); // Set the views directory
```

### Interpolation Syntax

EJS uses `<%= %>` to perform variable interpolation within HTML templates.

#### Example:

```ejs
<h1>Welcome, <%= username %>!</h1>
```

### Tags

- `<%`: 'Scriptlet' tag, for control-flow, no output
- `<%_`: 'Whitespace Slurping' Scriptlet tag, strips all whitespace before it
- `<%=`: Outputs the value into the template (HTML escaped)
- `<%-`: Outputs the unescaped value into the template
- `<%#`: Comment tag, no execution, no output
- `<%%`: Outputs a literal '<%'
- `%>`: Plain ending tag
- `-%>`: Trim-mode ('newline slurp') tag, trims following newline
- `_%>`: 'Whitespace Slurping' ending tag, removes all whitespace after it

Read Docs: [EJS Documentation](https://ejs.co/#docs)

### Passing Data to EJS

To render EJS templates with data, pass an object containing the data when rendering the view.

#### Example: Instagram EJS

Assuming we have an EJS template file named instagram.ejs:

```ejs
<!DOCTYPE html>
<html>
<head>
  <title>Instagram</title>
</head>
<body>
  <h1>Welcome to Instagram, <%= username %>!</h1>
  <div>
    <% posts.forEach((post) => { %>
      <div class="post">
        <img src="<%= post.imageUrl %>" alt="<%= post.caption %>">
        <p><%= post.caption %></p>
      </div>
    <% }); %>
  </div>
</body>
</html>
```

In your Node.js application:

```javascript
const express = require('express');
const app = express();

app.set('view engine', 'ejs'); // Set EJS as the view engine
app.set('views', path.join(__dirname, "/views")); // Set the views directory

app.get('/instagram', (req, res) => {
  const data = {
    username: 'john_doe',
    posts: [
      { imageUrl: 'image1.jpg', caption: 'A beautiful sunset' },
      { imageUrl: 'image2.jpg', caption: 'Delicious food' },
    ],
  };
  res.render('instagram', data); // Render the Instagram template with data
});

app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
```

### Conditional Statements

EJS supports conditional statements using `<% if (condition) { %> ... <% } %>`.

#### Example:

```ejs
<% if (user.loggedIn) { %>
  <p>Welcome, <%= user.username %>!</p>
<% } else { %>
  <p>Please log in to continue.</p>
<% } %>
```

### Loops

You can use JavaScript loops within EJS templates.

```ejs
<ul>
  <% for (let i = 0; i < items.length; i++) { %>
    <li><%= items[i] %></li>
  <% } %>
</ul>
```

### Serving Static Files

Use `express.static` to serve static files (e.g., CSS, images).

```javascript
app.use(express.static('public')); // Serve static files from the "public" directory
```

### Includes

EJS allows you to include reusable templates using `<%- include('filename') %>`.

```ejs
<%- include('header.ejs') %>
<h1>Welcome, <%= username %>!</h1>
<%- include('footer.ejs') %>
```

In summary, EJS is a powerful templating engine for Node.js that enables you to create dynamic web pages with ease. You can pass data, use conditional statements and loops, and include reusable components in your templates to build complex web applications.

## GET & POST Requests

### Overview

HTTP (Hypertext Transfer Protocol) is the foundation of data communication on the internet. It enables clients (e.g., web browsers) to request and interact with resources (e.g., web pages) hosted on servers. Two common HTTP request methods are GET and POST, each with distinct purposes and characteristics.

### GET Request

- Used for retrieving data from a specified resource.
- Commonly used for read-only operations that don't change server state.
- Data is appended to the URL as query parameters.
- Suitable for fetching data like articles, search queries, or product listings.

### POST Request

- Used for submitting data to a specified resource, often for creating or updating data.
- Appropriate for actions that modify server state, such as form submissions or file uploads.
- Data is sent in the request body, not visible in the URL.
- More secure for sensitive data and can handle larger payloads.

### Handling POST Requests

#### Server Setup

To handle POST requests, you need a web server and code to process incoming requests. Below is an example using Express.js.

```javascript
const express = require("express");
const app = express();
const port = 4040;
app.use(express.urlencoded({ extended: true }));
```

- Express.js is used to create the web server.
- The server listens on port 4040.
- Middleware is added to parse incoming URL-encoded form data.

#### Receiving POST Data

```javascript
app.post("/register", (req, res) => {
    let { user, password } = req.body;
    res.send(`post response, Welcome to ${user}`);
});
```

- Defines a route for handling POST requests to "/register".
- Extracts user and password from the request's body.
- Responds with a message including the extracted user.

#### Starting the Server

```javascript
app.listen(port, () => {
    console.log(`listening to port : ${port}`)
});
```

- Initiates the Express server, making it listen on port 4040.
- Logs a message to indicate the server is running.

#### HTML Forms for Testing

```html
<h3>Get Request form</h3>
<form method="get" action="http://localhost:4040/register">
    <input placeholder="enter username" name="user" type="text">
    <input placeholder="enter password" name="password" type="password">
    <button>SUBMIT</button>
</form>
<hr>
<h3>Post Request form</h3>


<form method="post" action="http://localhost:4040/register">
    <input placeholder="enter username" name="user" type="text">
    <input placeholder="enter password" name="password" type="password">
    <button>SUBMIT</button>
</form>
```

- HTML forms are provided for testing GET and POST requests.
- The "Get Request form" sends a GET request to "/register" with username and password fields.
- The "Post Request form" sends a POST request to "/register" with username and password fields.


---------------------------------------------------------------------------------------


# JavaScript Object-Oriented Programming (OOP)

## Introduction to JavaScript OOP

JavaScript is a versatile and dynamic programming language that supports object-oriented programming (OOP) paradigms. In JavaScript, everything is an object or can be treated as an object. This allows developers to create modular and organized code by defining objects with properties and methods. In this comprehensive guide, we'll explore various aspects of JavaScript OOP, including object prototypes, factory functions, the new operator, classes, and inheritance.

## Object Prototype

### Understanding Prototypes

In JavaScript, each object has a prototype. Prototypes allow objects to inherit properties and methods from other objects. Objects can share functionality through their prototypes, creating a hierarchical structure.

```javascript
// Creating an object
const person = {
  firstName: 'John',
  lastName: 'Doe',
};

// Accessing properties through the prototype chain
console.log(person.firstName); // John
```

### Modifying Prototypes

You can modify an object's prototype to add new methods or properties that will be shared among all instances of that object type.

```javascript
// Creating a constructor function
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

// Adding a method to the prototype
Person.prototype.getFullName = function () {
  return `${this.firstName} ${this.lastName}`;
};

const john = new Person('John', 'Doe');
console.log(john.getFullName()); // John Doe
```

**__proto__ Property (Reference)**

The `__proto__` property allows you to access the prototype of an object directly. Here's an example of modifying the `push` method of an array's prototype through `__proto__`:

```javascript
// Creating an array
let arr = [1, 2, 3];

// Accessing the prototype using __proto__
arr.__proto__;

// Modifying the push method of the array's prototype
arr.__proto__.push = (n) => {
  console.log("pushing number:", n);
};

// Pushing a new element to the array
arr.push(4);

// The modified push method is called
console.log(arr); // Output: [1, 2, 3, 4]
```

In this example, we access the `push` method of the array's prototype using `arr.__proto__` and then modify it to log a message when pushing a number. When we later call `arr.push(4)`, it uses the modified push method to log the message and add the element to the array.

## Factory Functions

### Creating Objects with Factory Functions

Factory functions are functions that create and return objects. They encapsulate the object creation process and allow you to create multiple instances with shared properties and methods.

```javascript
function createPerson(firstName, lastName) {
  return {
    firstName,
    lastName,
    getFullName() {
      return `${this.firstName} ${this.lastName}`;
    },
  };
}

const jane = createPerson('Jane', 'Smith');
console.log(jane.getFullName()); // Jane Smith
```

## The `new` Operator

### Constructors and Instances

JavaScript provides constructors that allow you to create objects using the `new` operator. Constructors are functions that are intended to be used with `new`. They create instances with their own properties and methods.

```javascript
function Car(make, model) {
  this.make = make;
  this.model = model;
}

const myCar = new Car('Toyota', 'Camry');
console.log(myCar.make); // Toyota
```

### Prototype Linkage with Constructors

Constructors also have prototypes, which are linked to the instances created with them. This allows sharing methods among instances.

```javascript
Car.prototype.startEngine = function () {
  console.log(`Starting the engine of a ${this.make} ${this.model}`);
};

myCar.startEngine(); // Starting the engine of a Toyota Camry
```

## Classes in JavaScript

### Introduction to ES6 Classes

ECMAScript 2015 (ES6) introduced a class syntax that simplifies object creation and inheritance in JavaScript.

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a sound.`);
  }
}

const dog = new Animal('Dog');
dog.speak(); // Dog makes a sound.
```

### Extends and Super

ES6 classes support inheritance through the `extends` keyword and the `super` keyword to call the constructor of the parent class.

```javascript
class Dog extends Animal {
  constructor(name, breed) {
    super(name); // Calling the parent class constructor
    this.breed = breed;
  }

  speak() {
    console.log(`${this.name} (a ${this.breed}) barks.`);
  }
}

const goldenRetriever = new Dog('Buddy', 'Golden Retriever');
goldenRetriever.speak(); // Buddy (a Golden Retriever) barks.
```

In this example, `extends` is used to create a subclass `Dog` that inherits from the parent class `Animal`. The `super(name)` call in the `Dog` constructor invokes the constructor of the `Animal` class, ensuring that both the parent and child class properties are properly initialized.

## Conclusion

JavaScript OOP offers multiple ways to create and structure objects, allowing you to design scalable and organized applications. Whether you choose prototypes, factory functions, constructors, or ES6 classes, understanding these concepts is crucial for effective JavaScript development.


---------------------------------------------------------------------------------------


# Backend (REST)

## What is REST?

REST, or Representational State Transfer, is an architectural style for designing networked applications. It follows a set of constraints and principles that aim to make web services simple, scalable, and modifiable. RESTful APIs (Application Programming Interfaces) adhere to these principles to create easily understandable and usable web services.

## REST Principles

1. **Stateless:** Each client request to the server must contain all the necessary information for the request's processing. The server should not store any client state between requests.

2. **Client-Server Architecture:** Separates client and server concerns, allowing them to evolve independently.

3. **Uniform Interface:** Maintains a consistent and standardized set of operations, including HTTP methods, for interacting with resources.

4. **Resource-Based:** Identifies resources, such as data objects or services, using URLs (Uniform Resource Locators).

5. **Representation:** Allows resources to have multiple representations (e.g., JSON, XML, HTML), enabling clients to choose their preferred representation.

## Example Code (index.js):

```javascript
const express = require("express");
const app = express();
const port = 3030;
const path = require("path");
const { v4: uuidv4 } = require("uuid");
const methodOverride = require("method-override");

app.set("view engine", "ejs");
app.set("views", path.join(__dirname, "views"));

app.use(express.static(path.join(__dirname, "public")));
app.use(express.urlencoded({ extended: true }));
app.use(methodOverride('_method'));

let posts = [];
// ... (other code)
```

## CRUD Operations

CRUD stands for Create, Read, Update, and Delete, which are the four fundamental operations for managing resources in a RESTful API.

### 1. Create (POST)

The Create operation uses the HTTP POST method to create a new resource on the server. It typically involves sending data in the request body to create the resource.

```javascript
app.post("/posts", (req, res) => {
    let { username, content } = req.body;
    let id = uuidv4();
    posts.push({ id, username, content });
    res.redirect("/posts");
});
```

### 2. Read (GET)

The Read operation employs the HTTP GET method to retrieve a resource or a list of resources from the server. It commonly requires providing a URL to specify the resource(s) to retrieve.

```javascript
app.get("/posts", (req, res) => {
    res.render("index.ejs", { posts });
});
```

### 3. Update (PUT and PATCH)

The Update operation utilizes the HTTP PUT or PATCH method to modify an existing resource on the server. PUT often involves sending the entire resource, while PATCH can be used for partial updates.

```javascript
app.patch("/posts/:id", (req, res) => {
    let { id } = req.params;
    let newContent = req.body.content;
    let post = posts.find((p) => id === p.id);
    post.content = newContent;
    res.redirect("/posts");
});
```

### 4. Delete (DELETE)

The Delete operation employs the HTTP DELETE method to remove a resource from the server. Typically, you specify the resource to delete using its URL.

```javascript
app.delete("/post/:id", (req, res) => {
    let { id } = req.params;
    posts = posts.filter((p) => id !== p.id);
    res.redirect("/posts");
});
```

These routes and actions follow REST principles and provide a structured way to interact with your API. Remember to use appropriate HTTP status codes (e.g., 200 OK, 201 Created, 204 No Content, 404 Not Found) to indicate the outcome of each operation.

In summary, RESTful APIs provide a standardized and scalable way to design web services, using HTTP methods for CRUD operations and following RESTful principles for resource management. By adhering to these conventions and integrating code examples, you can create well-organized and user-friendly web applications.


---------------------------------------------------------------------------------------


# Database Concepts and SQL Fundamentals

## What is a Database?

A **database** is a structured collection of data that is organized in a way that allows efficient retrieval, storage, and management of information. It serves as a repository for various types of data, such as customer records, product information, and financial transactions. Databases are used in software applications to store and retrieve data quickly and accurately.

## SQL vs. NoSQL

**SQL** (Structured Query Language) and **NoSQL** (Not Only SQL) are two primary approaches to managing and querying data in databases. The choice between them depends on the specific needs of the application:

- **SQL databases** are relational and use structured schemas. They are ideal for applications requiring complex queries and transactions.
  
- **NoSQL databases** are non-relational, flexible, and best suited for applications with rapidly changing data requirements.

## What is SQL?

**SQL** (Structured Query Language) is a domain-specific language used for managing and manipulating relational databases. SQL provides a standardized way to interact with databases, allowing users to perform tasks like querying data, inserting new records, updating existing records, and more.

## Tables in SQL

In SQL, data is organized into **tables**, which are like spreadsheets with rows and columns. Each table represents a specific entity or concept, and each row in the table represents a single instance of that entity, while columns represent attributes of the entity.

### Creating Databases and Tables

#### Creating a Database

To create a database in SQL, you can use the `CREATE DATABASE` statement:

```sql
CREATE DATABASE mydatabase;
```

#### Creating a Table

To create a table within a database, you can use the `CREATE TABLE` statement:

```sql
CREATE TABLE employees (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    hire_date DATE
);
```

### Database Queries

#### `USE` Database

The `USE` statement is used to switch to a specific database within your database management system. This statement is used in systems that support multiple databases:

```sql
USE mydatabase;
```

#### `CREATE DATABASE IF NOT EXISTS`

The `CREATE DATABASE IF NOT EXISTS` statement is used to create a new database if it does not already exist:

```sql
CREATE DATABASE IF NOT EXISTS mydatabase;
```

#### `DROP DATABASE`

The `DROP DATABASE` statement is used to delete an existing database and all its associated tables and data. Be cautious when using this statement, as it permanently removes the database:

```sql
DROP DATABASE mydatabase;
```

#### `SHOW DATABASES`

The `SHOW DATABASES` statement is used to list all the databases available in your database management system. It provides a list of database names:

```sql
SHOW DATABASES;
```

### Table Queries

#### `SELECT` Statement

The `SELECT` statement is used to retrieve data from one or more tables:

```sql
SELECT * FROM employees;
```

#### `INSERT` Statement

The `INSERT` statement is used to add new records to a table:

```sql
INSERT INTO employees (employee_id, first_name, last_name, hire_date)
VALUES (1, 'John', 'Doe', '2023-01-15');
```

#### `UPDATE` Statement

The `UPDATE` statement is used to modify existing records:

```sql
UPDATE employees
SET first_name = 'Jane'
WHERE employee_id = 1;
```

#### `DELETE` Statement

The `DELETE` statement is used to remove records from a table:

```sql
DELETE FROM employees
WHERE employee_id = 1;
```

#### `ALTER TABLE` Statement (Continued)

- **ADD Column:** To add a new column to an existing table, you can use the `ADD` clause:

  ```sql
  ALTER TABLE employees
  ADD COLUMN email VARCHAR(100);
  ```

- **DROP Column:** To remove an existing column from a table, you can use the `DROP` clause:

  ```sql
  ALTER TABLE employees
  DROP COLUMN email;
  ```

- **RENAME Table:** To rename an existing table, use the `RENAME TO` clause:

  ```sql
  ALTER TABLE old_table_name
  RENAME TO new_table_name;
  ```

- **RENAME Column:** To rename an existing column in a table, use the `CHANGE` or `MODIFY` clause:
  - Using `CHANGE`:

    ```sql
    ALTER TABLE employees
    CHANGE old_column_name new_column_name data_type;
    ```

  - Using `MODIFY` (used in some database systems):

    ```sql
    ALTER TABLE employees
    MODIFY COLUMN old_column_name new_column_name data_type;
    ```

These `ALTER TABLE` operations allow you to make structural changes to an existing table in your database as needed.

#### `TRUNCATE TABLE` Statement

The `TRUNCATE TABLE` statement is used to remove all data from a table:

```sql
TRUNCATE TABLE employees;
```

#### `DROP TABLE` Statement

The `DROP TABLE` statement is used to delete a table and all its data:

```sql
DROP TABLE employees;
```

### Data Types in SQL

SQL supports various data types, including:

- **INTEGER:** Whole numbers.
- **VARCHAR(size):** Variable-length character strings.
- **DATE:** Date values.
- **DECIMAL(precision, scale):** Fixed-point numbers.
- **BOOLEAN:** True or false values.

### Constraints in SQL

**Constraints** are rules applied to columns to enforce data integrity.

- **Primary Key Constraint:** Ensures uniqueness of values in a column.

  ```sql
  CREATE TABLE students (
      student_id INT PRIMARY KEY,
      name VARCHAR(50)
  );
  ```

- **Foreign Key Constraint:** Enforces referential integrity between tables.

  ```sql
  CREATE TABLE orders (
      order_id INT PRIMARY KEY,
      customer_id INT,
      FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
  );
  ```

- **Unique Constraint:** Ensures that values in a column are unique.

  ```sql
  CREATE TABLE products (
      product_id INT UNIQUE,
      name VARCHAR(50)
  );
  ```

- **Check Constraint:** Enforces specific conditions on data.

  ```sql
  CREATE TABLE employees (
      age INT CHECK (age >= 18),
      salary DECIMAL(10, 2) CHECK (salary >= 0)
  );
  ```

- **Default Constraint:** Sets a default value for a column.

  ```sql
  CREATE TABLE tasks (
      task_id INT,
      status VARCHAR(20) DEFAULT 'Pending'
  );
  ```

### Key Constraints

Key constraints include Primary Key, Unique Key, and Foreign Key constraints. They ensure data integrity and relationships between tables.

### `WHERE` Clause and Operators

The `WHERE` clause is used to filter records in a `SELECT`, `UPDATE`, or `DELETE` statement. Common operators include `=`, `<>`,

 `>`, `<`, `>=`, `<=`, `AND`, `OR`, and `NOT`.

```sql
SELECT * FROM employees WHERE salary > 50000;
```

### Aggregate Functions

Aggregate functions perform calculations on data and return a single value.

- **SUM:** Calculates the sum of values.
- **AVG:** Calculates the average of values.
- **COUNT:** Counts the number of rows.
- **MAX:** Returns the maximum value.
- **MIN:** Returns the minimum value.

```sql
SELECT AVG(salary) FROM employees;
```

### `GROUP BY` Clause

The `GROUP BY` clause is used with aggregate functions to group rows based on one or more columns.

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department;
```

### `HAVING` Clause

The `HAVING` clause filters the results of a `GROUP BY` query.

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 50000;
```

### General Order for SQL Commands

The general order for SQL commands in a query is:

1. **SELECT**
2. **FROM**
3. **JOIN**
4. **WHERE**
5. **GROUP BY**
6. **HAVING**
7. **ORDER BY**

These SQL concepts and commands provide a solid foundation for working with databases and managing data effectively. Remember to adapt these principles to your specific database system (e.g., MySQL, PostgreSQL, SQL Server) as there may be slight variations in syntax.


---------------------------------------------------------------------------------------


# SQL with Node.js

## Using SQL From Terminal and CLI

### Using SQL From Terminal

You can interact with your MySQL database from the terminal using the MySQL command-line client. Here's how to do it:

1. **Open a Terminal:** Open your terminal or command prompt.
2. **Log In to MySQL:** To log in to your MySQL server, use the following command. Replace `<username>` with your MySQL username, and `<password>` with your MySQL password:

    ```bash
    mysql -u <username> -p
    ```

    After running this command, you will be prompted to enter your MySQL password. Once you've successfully entered your password, you'll be logged in to MySQL.

3. **Select a Database:** If you have multiple databases on your MySQL server, you can select the one you want to work with using the `USE` statement:

    ```sql
    USE <database_name>;
    ```

4. **Execute SQL Statements:** You can now execute SQL statements directly in the terminal. For example, to retrieve all records from a table named `users`, you can use the `SELECT` statement:

    ```sql
    SELECT * FROM users;
    ```

   To exit the MySQL client, type:

    ```sql
    exit;
    ```

### Install Required Packages

Before you can work with SQL in Node.js, you'll need to install some essential packages. These packages will help you interact with databases and generate fake data for testing.

```bash
npm install mysql2 @faker-js/faker express path method-override
```

- **mysql2:** This package provides a MySQL client for Node.js, allowing you to connect to and interact with MySQL databases.
- **@faker-js/faker:** Faker.js is a library for generating fake data, which is useful for populating your database with test data during development.
- **express:** Express.js is a popular web application framework for Node.js. We'll use it to create routes and handle HTTP requests.
- **path:** The path module is built into Node.js and is used here to handle file paths.
- **method-override:** This middleware for Express.js allows you to use HTTP verbs like `PATCH` and `DELETE` by faking them as HTTP POST requests with a specific parameter. It's useful for supporting these HTTP methods in traditional HTML forms.

### Import Dependencies and Configure Express

In your `index.js` file, you import the necessary libraries and set up your Express application:

```javascript
const { faker } = require('@faker-js/faker');
const mysql = require('mysql2');
const express = require("express");
const app = express();
const path = require("path");
const methodOverride = require('method-override');

// Enable method overriding for HTTP verbs other than GET and POST
app.use(methodOverride('_method'));

// Parse incoming form data
app.use(express.urlencoded({ extended: true }));

const port = 8080;

// Set the views directory for EJS templates
app.set("views", path.join(__dirname, "/views"));
app.set("view engine", "ejs");

// Create a MySQL database connection
const connection = mysql.createConnection({
    host: 'localhost',
    user: 'root',
    database: 'delta_app',
    password: 'TMK0C/95'
});
```

In this setup:

- We import the necessary modules and libraries for our application.
- `methodOverride` middleware is used to enable HTTP methods like `PATCH` and `DELETE`, which are not natively supported in HTML forms.
- We set up Express to parse incoming form data and specify the port for our application.
- The views directory is set as the location for EJS templates.
- We create a MySQL database connection using the provided credentials.

## Routes and Database Operations

### Home Route

#### Display Users

The home route `/users` is responsible for displaying a list of users from the database. Here's how it works:

```javascript
app.get("/users", (req, res) => {
    // SQL query to select all users from the 'user' table
    let q = "SELECT * FROM user";

    try {
        // Execute the SQL query
        connection.query(q, (err, users) => {
            if (err) throw err;

            // Query to count the total number of users
            let q2 = "SELECT COUNT(*) FROM user";

            try {
                // Execute the count query
                connection.query(q2, (err, result) => {
                    if (err) throw err;

                    // Extract the count from the query result
                    let count = result[0]["COUNT(*)"];

                    // Render the 'show.ejs' template with user data and count
                    res.render("show.ejs", { users, count });
                });
            } catch (err) {
                console.log(err);
                res.send("Some error in the database");
            }
        });
    } catch (err) {
        console.log(err);
        res.send("Some error in the database");
    }
});
```

In this route:

- We execute a SQL query to select all users from the `user` table.
- We also execute a separate SQL query to count the total number of users in the table.
- Both queries

 are executed within nested `try...catch` blocks to handle errors.
- If successful, we render the `show.ejs` template, passing in the user data and count for display.

### Edit Route

#### Edit User

The edit route `/user/:id/edit` allows users to edit the details of a specific user. Here's how it's implemented:

```javascript
app.get("/user/:id/edit", (req, res) => {
    let { id } = req.params;

    // SQL query to select a user with the specified ID
    let q = `SELECT * FROM user WHERE id = '${id}'`;

    try {
        // Execute the SQL query
        connection.query(q, (err, result) => {
            if (err) throw err;

            // Extract the user data from the query result
            let user = result[0];

            // Render the 'edit.ejs' template with the user data
            res.render("edit.ejs", { user });
        });
    } catch (err) {
        console.log(err);
        res.send("Some error in the database");
    }
});
```

In this route:

- We extract the `id` parameter from the URL to identify the user to be edited.
- We execute a SQL query to select the user with the specified ID.
- The user data is extracted from the query result and passed to the `edit.ejs` template for rendering.

### Update Route

#### Update User

The update route `/user/:id` allows users to update the details of a specific user. It validates the user's password before making any changes:

```javascript
app.patch("/user/:id", (req, res) => {
    let { id } = req.params;
    let { password: formPass, username: newUsername } = req.body;

    // SQL query to select a user with the specified ID
    let q = `SELECT * FROM user WHERE id = '${id}'`;

    try {
        // Execute the SQL query
        connection.query(q, (err, result) => {
            if (err) throw err;

            // Extract the user data from the query result
            let user = result[0];

            if (formPass != user.password) {
                // Check if the provided password matches the user's password
                res.send("Wrong Password");
            } else {
                // Update the user's username
                let q2 = `UPDATE user SET username = '${newUsername}' WHERE id = '${id}'`;

                connection.query(q2, (err, result) => {
                    if (err) throw err;

                    // Render the 'update.ejs' template to confirm the update
                    res.render("update.ejs");
                });
            }
        });
    } catch (err) {
        res.send("Some error in the database");
    }
});
```

In this route:

- We extract the `id` parameter from the URL to identify the user to be updated.
- We retrieve the user's current password and the new username from the form data.
- A SQL query is executed to select the user with the specified ID.
- We check if the provided password matches the user's password. If not, we display an error message.
- If the password is correct, we execute another SQL query to update the user's username.
- Finally, we render the `update.ejs` template to confirm the update.

### Delete Route

#### Delete User

The delete route `/user/:id/del` allows users to initiate the deletion of a specific user:

```javascript
app.get("/user/:id/del", (req, res) => {
    let { id } = req.params;

    // SQL query to select a user with the specified ID
    let q = `SELECT * FROM user WHERE id = '${id}'`;

    try {
        // Execute the SQL query
        connection.query(q, (err, result) => {
            if (err) throw err;

            // Extract the user data from the query result
            let user = result[0];

            // Render the 'del.ejs' template with the user data
            res.render("del.ejs", { user });
        });
    } catch (err) {
        console.log(err);
        res.send("Some error in the database");
    }
});
```

In this route:

- We extract the `id` parameter from the URL to identify the user to be deleted.
- We execute a SQL query to select the user with the specified ID.
- The user data is extracted from the query result and passed to the `del.ejs` template for rendering.

### Delete Done Route

#### Confirm Deletion

The delete done route `/user/:id` confirms the successful deletion of a user:

```javascript
app.delete("/user/:id", (req, res) => {
    let { id } = req.params;
    let { password: formPass } = req.body;

    // SQL query to select a user with the specified ID
    let q = `SELECT * FROM user WHERE id = '${id}'`;

    try {
        // Execute the SQL query
        connection.query(q, (err, result) => {
            if (err) throw err;

            // Extract the user data from the query result
            let user = result[0];

            if (formPass != user.password) {
                // Check if the provided password matches the user's password
                res.send("Wrong Password");
            } else {
                // Delete the user from the database
                let q2 = `DELETE FROM user WHERE id = '${id}'`;

                connection.query(q2, (err, result) => {
                    if (err) throw err;

                    // Render the 'del_done.ejs' template to confirm the deletion
                    res.render("del_done.ejs");
                });
            }
        });
    } catch (err) {
        res.send("Some error in the database");
    }
});
```

In this route:

- We extract the `id` parameter from the URL to identify the user to be deleted.
- We retrieve the user's password from the form data.
- A SQL query is executed to select the user with the specified ID.
- We check if the provided password matches the user's password. If not, we display an error message.
- If the password is correct, we execute another SQL query to delete the user from the database.
- Finally, we render the `del_done.ejs` template to confirm the deletion.

### Add Route

#### Add User Form

The add route `/user/add` displays a form for users to create a new user:

```javascript
app.get("/user/add", (req, res) => {
    res.render("add.ejs");
});
```

In this route:

- We simply render the `add.ejs` template, which includes a form for creating a new user.

### Add Done Route

#### Create New User

The add done route `/user/add` handles the creation of a new user based on the form data provided by the user:

```javascript
app.post("/user/add", (req, res) => {
    let { username: newUsername, email: newEmail, password: newPass } = req.body;
    let q = "INSERT INTO user (id, username, email, password) VALUES (?, ?, ?, ?)";

    // Generate a random UUID using the faker library
    let id = faker.string.uuid();
    let data = [id, newUsername, newEmail, newPass];

    try {
        // Execute the SQL query to insert a new user
        connection.query(q, data, (err, result) => {
            if (err) throw err;

            console.log(result);

            // Render the 'add_done.ejs' template to confirm the user creation
            res.render("add_done.ejs");
        });
    } catch (err) {
        res.send("Some error in the database");
    }
});
```

In this route:

- We extract the new user's username, email, and password from the form data.
- A SQL query is executed to insert a new user into the `user` table. A random UUID is generated for the `id` field using the Faker library.
- After successful insertion, we render the `add_done.ejs` template to confirm the user's creation.

## Views (EJS Templates)

### Show Users (`show.ejs`)

The `show.ejs` template displays a table of users and the total user count:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Metadata and Styles -->
</head>
<body>
    <h2>The total number of users are: <%= count %></h2>
    <a href="http://localhost:8080/user/add">CREATE</a>
    <hr>
    <table>
        <tr>
            <th>ID</th>
            <th>Username</th>
            <th>Email</th>
        </tr>
        <% for (user of users) { %>
            <tr>
                <td><%= user.id %></td>
                <td><%= user.username %></td>
                <td><%= user.email %></td>
                <td>
                    <form method="GET" action="/user/<%= user.id %>/edit">
                        <button>EDIT</button>
                    </form>
                </td>
                <td>
                    <form method="GET" action="/user/<%= user.id %>/del">
                        <button>DELETE</button>
                    </form>
                </td>
            </tr>
        <% } %>
    </table>
</body>
</html>
```

In this template:

- We use EJS syntax `<%= count %>` to display the total user count dynamically.
- The user data is displayed in an HTML table.
- Edit and delete buttons are provided for each user.

### Edit User (`edit.ejs`)

The `edit.ejs` template allows users to edit the details of a specific user:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Metadata and Styles -->
</head>
<body>
    <h2>You are about to edit this user: <%= user.id %></h2>
    <form method="POST" action="/user/<%= user.id %>?_method=PATCH">
        <textarea name="username"><%= user.username %></textarea>
        <input type="password" name="password" placeholder="Enter your password">
        <button>Edit</button>
    </form>
</body>
</html>
```

In this template:

- We display a message indicating which user is being edited.
- A form for editing user details is included.

### Update User Success (`update.ejs`)

The `update.ejs` template confirms the successful update of a user's details:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Metadata and Styles -->
</head>
<body>
    <h2>Username edited successfully</h2>
    <a href="http://localhost:8080/users">Go to HOME!</a>
</body>
</html>
```

In this template:

- We display a success message after a user's username has been updated.
- A link is provided to return to the home page.

### Delete User (`del.ejs`)

The `del.ejs` template allows users to confirm the deletion of a specific user:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Metadata and Styles -->
</head>
<body>
    <h2>You are about to DELETE this user: <%= user.id %></h2>
    <form method="POST" action="/user/<%= user.id %>?_method=DELETE">
        <input type="password" name="password" placeholder="Enter your password">
        <button>DELETE</button>
    </form>
</body>
</html>
```

In this template:

- We display a message indicating which user is about to be deleted.
- A form for confirming the deletion is included.

### Delete User Success (`del_done.ejs`)

The `del_done.ejs` template confirms the successful deletion of a user:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Metadata and Styles -->
</head>
<body>
    <h2>User deleted successfully</h2>
    <a href="http://localhost:8080/users">Go to HOME!</a>
</body>
</html>
```

In this template:

- We display a success message after a user has been deleted.
- A link is provided to return to the home page.

### Add User (`add.ejs`)

The `add.ejs` template displays a form for creating a new user:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Metadata and Styles -->
</head>
<body>
    <h2>Create your new user</h2>
    <form method="POST" action="/user/add">
        <textarea name="username" placeholder="Enter your new username"></textarea>
        <textarea name="email" placeholder="Enter your new email"></textarea>
        <input type="password" name="password" placeholder="Create your own password">
        <button>SUBMIT</button>
    </form>
</body>
</html>
```

In this template:

- We provide a form for users to input their desired username, email, and password for creating a new user.

### Add User Success (`add_done.ejs`)

The `add_done.ejs` template confirms the successful creation of a new user:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- Metadata and Styles -->
</head>
<body>
    <h2>User Created Successfully</h2>
    <a href="http://localhost:8080/users">Go to HOME!</a>
</body>
</html>
```

In this template:

- We display a success message after a new user has been created.
- A link is provided to return to the home page.

These detailed explanations and code snippets cover various aspects of building a Node.js application with SQL database interactions using MySQL and EJS templates. Feel free to adapt and expand upon this foundation to meet your specific project requirements.


---------------------------------------------------------------------------------------


# MongoDB

## The Mongo Shell 'mongosh'

MongoDB provides a powerful command-line interface called `mongosh` to interact with the database. You can use `mongosh` to connect to your MongoDB server, perform queries, and manage your data.

### Connect to MongoDB Server

To start using `mongosh`, open your terminal and run:

```bash
mongosh
```

By default, it connects to a MongoDB server running on localhost at port 27017.

### How We Store Data? (BSON)

MongoDB stores data in a format called BSON (Binary JSON). BSON is a binary-encoded serialization of JSON-like documents. It is efficient for storing and retrieving data and supports various data types, including strings, numbers, dates, arrays, and nested documents.

### Document & Collection

In MongoDB, data is organized into collections, and each collection contains documents. A document is a JSON-like data structure that stores data as key-value pairs. Documents within a collection can have different structures, allowing for flexibility in data modeling.

### Basic Commands

#### Show All Databases

To list all the databases on the MongoDB server:

```bash
show dbs
```

#### Switch to a Database

To switch to a specific database or create a new one if it doesn't exist:

```bash
use mydatabase
```

#### Show Collections in Current Database

To list all collections in the current database:

```bash
show collections
```

#### Insert Data in DB

##### Insert a Single Document

To insert a single document into a collection:

```bash
db.myCollection.insertOne({
    name: "John Doe",
    age: 30,
    email: "john@example.com"
})
```

##### Insert Multiple Documents

To insert multiple documents into a collection:

```bash
db.myCollection.insertMany([
    {
        name: "Alice",
        age: 25,
        email: "alice@example.com"
    },
    {
        name: "Bob",
        age: 28,
        email: "bob@example.com"
    }
])
```

#### Find Data in DB

##### Find All Documents

To retrieve all documents from a collection:

```bash
db.myCollection.find()
```

##### Find Documents with a Condition

To find documents that match specific criteria, use the find method with a query filter:

```bash
db.myCollection.find({ age: { $gte: 25 } })
```

##### Query Operators (Important Ones)

- `$eq` (Equals)
  
  ```bash
  db.myCollection.find({ age: { $eq: 30 } })
  ```

- `$gt` (Greater Than)
  
  ```bash
  db.myCollection.find({ age: { $gt: 25 } })
  ```

- `$lt` (Less Than)
  
  ```bash
  db.myCollection.find({ age: { $lt: 30 } })
  ```

- `$gte` (Greater Than or Equal To)
  
  ```bash
  db.myCollection.find({ age: { $gte: 25 } })
  ```

- `$lte` (Less Than or Equal To)
  
  ```bash
  db.myCollection.find({ age: { $lte: 30 } })
  ```

- `$in` (In Array)
  
  ```bash
  db.myCollection.find({ name: { $in: ["John", "Alice"] } })
  ```

- `$and` (Logical AND)
  
  ```bash
  db.myCollection.find({
      $and: [
          { age: { $gte: 25 } },
          { name: "John" }
      ]
  })
  ```

- `$or` (Logical OR)
  
  ```bash
  db.myCollection.find({
      $or: [
          { age: { $lt: 25 } },
          { name: "Alice" }
      ]
  })
  ```

These query operators allow you to perform complex queries and filter documents based on specific conditions in your MongoDB collections.

#### Update Data in DB

##### Update a Single Document

To update a single document:

```bash
db.myCollection.updateOne(
    { name: "John Doe" },
    { $set: { age: 31 } }
)
```

##### Update Multiple Documents

To update multiple documents:

```bash
db.myCollection.updateMany(
    { age: { $lt: 30 } },
    { $set: { status: "Young" } }
)
```

#### Nesting

MongoDB allows you to nest documents within other documents. This is useful for representing complex data structures. For example:

```bash
{
    name: "John",
    address: {
        street: "123 Main St",
        city: "New York",
        zip: "10001"
    }
}
```

#### Delete Data in DB

##### Delete a Single Document

To delete a single document:

```bash
db.myCollection.deleteOne({ name: "John Doe" })
```

##### Delete Multiple Documents

To delete multiple documents:

```bash
db.myCollection.deleteMany({ age: { $lt: 30 } })
```

These commands provide a solid foundation for working with MongoDB. As you gain experience, you can explore more advanced features and techniques for data modeling and querying.


---------------------------------------------------------------------------------------


# MongoDB with Mongoose

## Installation & Setup

To use Mongoose, you need to install it in your Node.js project. You can do this using npm or yarn:

```bash
npm install mongoose
```

Once installed, you can set up the connection to your MongoDB server and create schemas and models.

```javascript
const mongoose = require('mongoose');

async function main() {
  // Connect to the MongoDB server
  await mongoose.connect('mongodb://127.0.0.1:27017/test');

  // Use `await mongoose.connect('mongodb://user:password@127.0.0.1:27017/test');` 
  // if your database has authentication enabled
}

main()
  .then(() => {
    console.log("Connection successful");
  })
  .catch(err => console.log(err));
```

Here, we establish a connection to the MongoDB server running locally on the default port (27017) and using the "test" database. You can replace this with your specific MongoDB connection string.

## Schema & Models

### Schema

A schema defines the structure of documents within a collection. It specifies the fields, types, and constraints for the data.

```javascript
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  age: Number
});
```

This line defines a schema for a "user" collection. It specifies that documents in this collection should have "name," "email," and "age" fields of specific data types.

### Model

A model is a constructor function that corresponds to a collection in your database. It allows you to create, read, update, and delete documents within that collection.

```javascript
const user = mongoose.model("user", userSchema);
```

This line creates a model named "user" that corresponds to the "user" collection in the database. It uses the previously defined schema (`userSchema`) to define the structure of documents in this collection.

## Insert Data in Mongoose

### Insert a Single Document

To insert a single document into a collection:

```javascript
const newUser = new user({
  name: "John Doe",
  email: "john@example.com",
  age: 30
});

// Save the new user document
newUser.save()
  .then((res) => {
    console.log("User inserted successfully:", res);
  })
  .catch((err) => {
    console.error("Error inserting user:", err);
  });
```

We create a new user document with the specified name, email, and age. The `newUser.save()` method saves the new user document to the database. We use promises (`then` and `catch`) to handle the success or failure of the operation.

### Insert Multiple Documents

To insert multiple documents into a collection:

```javascript
user.insertMany([
  { name: "Alice", email: "alice@example.com", age: 25 },
  { name: "Bob", email: "bob@example.com", age: 28 }
])
  .then((res) => {
    console.log("Users inserted successfully:", res);
  })
  .catch((err) => {
    console.error("Error inserting users:", err);
  });
```

We use the `insertMany` method to insert an array of user documents into the collection.

## Find Data in Mongoose

### Find All Documents

To retrieve all documents from a collection:

```javascript
user.find()
  .then((users) => {
    console.log("All users:", users);
  })
  .catch((err) => {
    console.error("Error finding users:", err);
  });
```

This method finds all documents in the "user" collection.

### Find Documents with a Condition

To find documents that match specific criteria:

```javascript
user.find({ age: { $gte: 25 } })
  .then((users) => {
    console.log("Users aged 25 and older:", users);
  })
  .catch((err) => {
    console.error("Error finding users:", err);
  });
```

We use the `find` method with a query object to find users aged 25 and older.

## Update One or Many Documents

To update one or many documents with a condition:

```javascript
user.updateOne(
  { name: "Alice" },
  { age: 26 }
)
  .then((result) => {
    console.log("Updated one document:", result);
  })
  .catch((err) => {
    console.error("Error updating document:", err);
  });

user.updateMany(
  { age: { $lt: 30 } },
  { $set: { status: "young" } }
)
  .then((result) => {
    console.log("Updated multiple documents:", result);
  })
  .catch((err) => {
    console.error("Error updating documents:", err);
  });
```

`user.updateOne({ ... }, { ... })`: Updates the first document that matches the condition.

`user.updateMany({ ... }, { ... })`: Updates all documents that match the condition.

## Find and Update Data in Mongoose

### findOneAndUpdate

To find and update a document using `findOneAndUpdate`:

```javascript
user.findOneAndUpdate(
  { name: "John Doe" },
  { age: 31 },
  { new: true }
)
  .then((updatedUser) => {
    console.log("Updated user:", updatedUser);
  })
  .catch((err) => {
    console.error("Error updating user:", err);
  });
```

We use the `findOneAndUpdate` method to find a user document with the specified name and update their age to 31. The `{ new: true }` option ensures that the updated document is returned.

### findByIdAndUpdate

To find and update a document by its ID using `findByIdAndUpdate`:

```javascript
user.findByIdAndUpdate("65101d803e57981ee2798ae5", { age: 32 }, { new: true })
  .then((updatedUser) => {
    console.log("Updated user by ID:", updatedUser);
  })
  .catch((err) => {
    console.error("Error updating user by ID:", err);
  });
```

This method finds a user document by its ID and updates their age to 32. The `{ new: true }` option ensures that the updated document is returned.

## Delete Data in Mongoose

### Delete a Single Document

To delete a single document:

```javascript
user.findOneAndDelete({ name: "John Doe" })
  .then((deletedUser) => {
    console.log("Deleted user:", deletedUser);
  })
  .catch((err) => {
    console.error("Error deleting user:", err);
  });
```

We use the `findOneAndDelete` method to find and delete a user document with the specified name.

## Schema Validations

You can enforce schema-level validations for your data in Mongoose. For example, you can specify required fields, minimum and maximum values, and enum values.

```javascript
const bookSchema = new mongoose.Schema({
  title: {
    type: String,
    required: true // The "title" field is required
  },
  author: String,
  price: {
    type: Number,
    min: [1, "Price is too low for Amazon sale"] // Custom error message
  },
  category: {
    type: String,
    enum

: ["fiction", "non-fiction"] // Enumerated values
  },
  genre: [String]
});
```

- `required: true`: The "title" field is marked as required, meaning it must be present in the document.
- `min: [1, "Price is too low for Amazon sale"]`: The "price" field has a minimum value of 1, and a custom error message is provided if this constraint is violated.
- `enum: ["fiction", "non-fiction"]`: The "category" field is restricted to the values "fiction" or "non-fiction."

## Schema Type Options

In Mongoose, schema type options allow you to specify additional constraints and behaviors for schema fields.

Examples: In previous codes

- `min: [1, "Price is too low for Amazon sale"]`: This sets the minimum value for the "price" field to 1 and provides a custom error message if the constraint is violated.
- `enum: ["fiction", "non-fiction"]`: This specifies that the "category" field must have a value that matches one of the provided options.

## Validation in Update

When updating documents, you can apply schema-level validation to ensure that the updated data adheres to your schema constraints.

```javascript
book.findByIdAndUpdate(
  "65101d803e57981ee2798ae5",
  { price: -10 },
  { runValidators: true } // Enable schema validation during the update
)
  .then((res) => {
    console.log("Updated book:", res);
  })
  .catch((err) => {
    console.error("Error updating book:", err.errors.price.properties.message);
  });
```

- `runValidators: true`: This option enables schema validation during the update. It ensures that the updated data complies with the schema constraints, including those related to minimum and maximum values, enum values, and required fields.

These notes provide a comprehensive overview of working with MongoDB and Mongoose, covering essential concepts and operations to manage data effectively.


---------------------------------------------------------------------------------------


# MongoDB with Express: Building a Chat Application

In this tutorial, we'll create a basic chat application using MongoDB and Express. We'll cover various aspects of building the application, including setting up the environment, creating models, initializing the database, and defining routes for index, create, edit, update, and delete operations.

## Basic Setup

To begin, let's set up the basic structure of our Express application.

```javascript
const express = require("express");
const app = express();
const mongoose = require("mongoose");
const path = require("path");
const chat = require("./models/chat.js");
const methodOverride = require('method-override');

app.set("views", path.join(__dirname, "views"));
app.set("view engine", "ejs");
app.use(express.static(path.join(__dirname, "public")));
app.use(express.urlencoded({ extended: true }));
app.use(methodOverride('_method'));

main().then(() => {
    console.log("Connection Successful")
}).catch((err) => {
    console.log(err)
});

async function main() {
    await mongoose.connect('mongodb://127.0.0.1:27017/whatsapp');
}
```

**In the above code:**
- We import necessary dependencies such as Express, Mongoose, and path.
- We set up our Express app, configure the view engine to use EJS, and serve static files.
- We establish a connection to the MongoDB database named "whatsapp" using Mongoose.

## Creating the Chat Model

Next, we'll create a Mongoose model for our chat messages. This model defines the schema for our chat documents.

```javascript
const mongoose = require("mongoose");

const chatSchema = new mongoose.Schema({
    from: {
        type: String,
        required: true
    },
    to: {
        type: String,
        required: true
    },
    msg: {
        type: String,
        maxLength: 100
    },
    created_at: {
        type: String,
        required: true
    }
});

const chat = mongoose.model("chat", chatSchema);

module.exports = chat;
```

**Here:**
- We define a chat schema with fields for the sender ("from"), recipient ("to"), message ("msg"), and a timestamp ("created_at").
- We specify validation rules, such as "required" and "maxLength."

## Routes and Views

### Index Route

Now, let's create routes for our chat application, starting with the index route, which displays all chat messages.

```javascript
// Index Route
app.get("/chats", async (req, res) => {
    let chats = await chat.find();
    res.render("index.ejs", { chats });
});
```

**In this code:**
- We fetch all chat messages from the database and render them using the "index.ejs" view.

### Create Route

We also need a route for creating new chat messages.

```javascript
// New Route
app.get("/chats/new", (req, res) => {
    res.render("new.ejs");
});

// Create Route
app.post("/chats", (req, res) => {
    let { from, msg, to } = req.body;
    let newChat = new chat({
        from: from,
        msg: msg,
        to: to,
        created_at: new Date()
    });

    newChat.save().then(result => {
        console.log("Chat Was Saved:", result);
    }).catch(err => {
        console.log(err);
    });

    res.redirect("/chats");
});
```

**Here:**
- We have routes for displaying the new chat form and handling the form submission.
- We create a new chat document and save it to the database.

### Edit and Update Routes

Let's add routes for editing and updating chat messages.

```javascript
// Edit Route
app.get("/chats/:id/edit", async (req, res) => {
    let { id } = req.params;
    let chatToEdit = await chat.findById(id);
    res.render("edit.ejs", { chatToEdit });
});

// Update Route
app.put("/chats/:id", async (req, res) => {
    let { id } = req.params;
    await chat.findByIdAndUpdate(id, { msg: req.body.msg });
    res.redirect("/chats");
});
```

**These routes allow us to edit the content of an existing chat message and then update it in the database.**

### Delete Route

Finally, let's create a route for deleting chat messages.

```javascript
// Delete Route
app.delete("/chats/:id", async (req, res) => {
    let { id } = req.params;
    await chat.findByIdAndDelete(id).then(result => {
        console.log("Chat Deleted:", result);
    }).catch(err => {
        console.log(err);
    });
    res.redirect("/chats");
});
```

**This route deletes a chat message based on its ID.**

## Views

We also have views that correspond to these routes, such as "index.ejs," "new.ejs," and "edit.ejs." These views define the HTML structure and layout of our chat application's pages.

With these routes and views in place, you have a basic chat application using MongoDB and Express. Users can view, create, edit, update, and delete chat messages.

Remember to install and configure Express, Mongoose, and EJS in your project to make it functional.


---------------------------------------------------------------------------------------


# Middlewares in Express

In Express, middlewares are essential components that play a crucial role in processing HTTP requests and responses. They allow you to perform various tasks before, during, or after the request-response cycle. This guide will explore what middlewares are, how to use them, and their practical applications.

## What Are Middlewares?

Middlewares are functions in Express that have access to the request (`req`) and response (`res`) objects. They can also access the next middleware function in the application's request-response cycle. Middlewares are executed in the order they are defined in the code.

### Accessing the Request and Response Objects

When creating a middleware, you can access information from the incoming HTTP request and manipulate the outgoing HTTP response. The request object (`req`) contains details such as HTTP headers, parameters, and the request body, while the response object (`res`) allows you to send back data, such as HTML, JSON, or status codes.

### Chaining Middlewares

You can chain multiple middleware functions together in your application. This chaining can be used for various purposes, such as processing authentication, logging, and error handling. When a middleware function calls the `next()` function, it passes control to the next middleware in the chain.

```javascript
// Example of two chained middlewares
app.use((req, res, next) => {
    console.log("Hi, I am middleware");
    next(); // Call next to move to the next middleware
});

app.use((req, res, next) => {
    console.log("Hi, I am the second middleware");
    next();
});
```

In this example, the first middleware logs a message, and then it calls `next()`, passing control to the second middleware, which logs another message.

## What Do Middlewares Do?

Middlewares serve various purposes in an Express application:

- **Logging**: Middlewares can log request information, such as the HTTP method, hostname, path, and timestamps. This information is valuable for debugging and monitoring.
  
- **Authentication**: Middlewares can be used to check if a user is authenticated before allowing access to specific routes or resources.
  
- **Route-Specific Operations**: You can apply middlewares to specific routes. For example, you might want to verify an API token for specific routes or perform data validation only for certain endpoints.
  
- **Error Handling**: Middlewares can handle errors and provide meaningful error messages to the client. Express has a default error handler for unhandled exceptions.

### Using Next()

The `next()` function is a critical part of middleware functions. Calling `next()` passes control to the next middleware in the chain. If `next()` is not called, the request-response cycle will be terminated, and the response will be sent back to the client.

### Express Built-in and Third-party Middlewares

Express comes with built-in middlewares like `express.json()`, `express.urlencoded()`, and more for parsing request bodies. Additionally, you can use third-party middlewares to extend the functionality of your Express application. Common third-party middlewares include `morgan` for request logging and `helmet` for security.

```javascript
const express = require("express");
const app = express();

// Built-in middleware for parsing JSON
app.use(express.json());

// Third-party middleware for request logging
const morgan = require("morgan");
app.use(morgan("combined"));
```

### Creating Utility Middleware and Logger

You can create your own utility middlewares to perform tasks such as logging or adding custom properties to the request object.

```javascript
// Logger middleware
app.use((req, res, next) => {
    req.time = new Date(Date.now()).toString();
    console.log(req.method, req.hostname, req.path, req.time);
    next();
});
```

In the above example, the middleware adds a `time` property to the request object, logs the request method, hostname, path, and the time it was received.

### Exploring `app.use()`

The `app.use()` method is used to mount a middleware function to a specific route. Middleware functions added using `app.use()` will be executed for all HTTP methods on that route.

```javascript
app.use("/random", (req, res, next) => {
    console.log("I am only for the '/random' route");
});
```

This middleware will be executed only for requests to the `/random` route.

### API Token as Query String

You can create a middleware that checks for an API token passed as a query parameter.

```javascript
const checkToken = (req, res, next) => {
    let { token } = req.query;
    if (token === "giveaccess") {
        next();
    }
    res.send("ACCESS DENIED!");
};
```

The `checkToken` middleware checks if the token query parameter is equal to "giveaccess" and allows or denies access accordingly.

### Passing Multiple Middleware

Multiple middleware functions can be added to a route, and they will be executed in the order they are defined. This allows you to handle various aspects of a request.

```javascript
app.get("/api", checkToken, (req, res) => {
    res.send("Data from an authenticated route");
});
```

In this example, the route `/api` uses the `checkToken` middleware to ensure access is granted only with a valid API token.

### Error Handling (Express Default)

Express has a default error-handling mechanism. When an error occurs within a middleware or route handler, you can pass the error to the `next()` function, and it will be caught by the default error handler.

```javascript
app.get("/wrong", (req, res) => {
    // Simulating an error
    // Unhandled errors will be caught by the default error handler
    abc = abc;
});
```

In this example, we intentionally create an error by trying to access an undefined variable. Express will handle this error, and an error response will be sent to the client.

## Conclusion

Middleware functions in Express are powerful tools for controlling and managing the flow of HTTP requests and responses. They enable you to handle various aspects of request processing, including logging, authentication, route-specific

 operations, and error handling. By understanding and using middleware effectively, you can build robust and feature-rich web applications.


---------------------------------------------------------------------------------------


# Errors in Express.js

## Error Handling Middleware

In an Express.js application, error handling is essential to handle various types of errors that may occur during the execution of your code. This includes synchronous and asynchronous errors. To handle errors gracefully, we can set up an error handling middleware.

Here's how you can create an error handling middleware in Express:

```javascript
app.use((err, req, res, next) => {
    let { status = 500, message = "Some Error Occurred" } = err; // Default Status and Message
    res.status(status).send(message);
});
```

In this middleware, we take any error thrown in the previous middleware or route handlers and respond with an appropriate status code and error message. You can customize the response as needed for your application.

### Custom Error Class

It's a good practice to create a custom error class that extends the built-in Error class to provide more context and information about the error. In your case, you've created an `ExpressError` class:

```javascript
// ExpressError.js
class ExpressError extends Error {
    constructor(status, message) {
        super();
        this.status = status;
        this.message = message;
    }
}

module.exports = ExpressError;
```

This custom error class allows you to define a specific status code and message for each error, making it easier to handle and send meaningful error responses.

### Async Errors

#### Handling Async Errors in Specific Route

```javascript
app.get("/chats/:id", wrapAsync(async (req, res, next) => {
    let { id } = req.params;
    let Chat = await chat.findById(id);
    if (!Chat) {
        next(new ExpressError(404, "Chat not found")); // Handling Async Errors
    }
    res.render("edit.ejs", { Chat });
}));
```

In this route handler, when attempting to find a chat by ID, it checks if the chat exists. If the chat is not found, it triggers an async error by calling `next` with an `ExpressError` containing a 404 status and a "Chat not found" message. This is a common pattern to handle async errors in Express routes.

#### Using try-catch

When dealing with asynchronous operations in Express, you can also use try-catch blocks to handle errors. Here's an example:

```javascript
app.put("/chats/:id", async (req, res, next) => {
    try {
        let { id } = req.params;
        await chat.findByIdAndUpdate(id, { msg: req.body.msg });
        res.redirect("/chats");
    } catch (err) {
        next(err);
    }
});
```

In this example, we use a try-catch block to catch any errors that may occur during the `chat.findByIdAndUpdate` operation and pass them to the error handling middleware using `next`.

#### Using `wrapAsync`

In an Express.js application, handling asynchronous operations, such as database queries, is crucial. To ensure that errors in these operations are properly caught and passed to the error handling middleware, we often use a utility function called `wrapAsync`. It wraps asynchronous route handlers and catches any errors that may occur during their execution.

### How `wrapAsync` Works

Here's how `wrapAsync` is typically implemented:

```javascript
function wrapAsync(fn) {
    return function (req, res, next) {
        fn(req, res, next).catch((err) => next(err));
    }
}
```

- `wrapAsync` takes an asynchronous function `fn` as an argument.
- It returns a new function that accepts the standard Express.js request (`req`), response (`res`), and next middleware function as parameters.
- Within this new function, `fn` is invoked with `req`, `res`, and `next`.
- If `fn` returns a promise, the `.catch` method is used to catch any errors that occur during the promise execution.
- When an error is caught, it is passed to the `next` middleware function, effectively forwarding the error to the error handling middleware.

### Example Usage

Here's an example of how `wrapAsync` is used in an Express route handler:

```javascript
app.get("/chats", wrapAsync(async (req, res) => {
    let chats = await chat.find();
    res.render("index.ejs", { chats });
}));
```

In this example, the `wrapAsync` function is applied to an asynchronous route handler for fetching chat data from a database. If an error occurs during the `chat.find()` operation, it is caught by `wrapAsync` and passed to the `next` middleware, where it can be handled appropriately.

Using `wrapAsync` is a clean and effective way to ensure that asynchronous errors are properly managed and do not crash your Express application. It's a common pattern in Express.js applications to make error handling more robust and maintainable.

## Mongoose Errors

### Handling Mongoose Validation Errors

Mongoose, when used as an ODM (Object-Document Mapping) for MongoDB, provides built

-in validation. If validation fails, it throws a `ValidationError`. You can handle Mongoose validation errors specifically and provide custom error messages.

```javascript
const handleValidationError = (err) => {
    console.log("This was a validation error. Please follow rules.");
    console.log(err.message);
    return err;
};

app.use((err, req, res, next) => {
    console.log(err.name);
    if (err.name === "ValidationError") {
        err = handleValidationError(err);
    }
    next(err);
});
```

In this code, we check the error's `name` property to identify it as a validation error, and then you can customize how you want to handle and log the error.

### Validation for Schema (Using npm Joi)

#### Schema Validation Using Joi

Joi is a popular library for schema validation in Node.js applications. It helps ensure that data passed to your application follows the expected structure and rules. In your case, it appears you are using Joi for schema validation.

Here's an example of defining a schema with Joi:

```javascript
// schema.js
const Joi = require('joi');

module.exports.listingSchema = Joi.object({
    listing: Joi.object({
        title: Joi.string().required(),
        description: Joi.string().required(),
        location: Joi.string().required(),
        country: Joi.string().required(),
        price: Joi.number().required().min(0),
        Image: Joi.string().allow("", null),
    }).required()
});
```

This defines a schema using Joi for a listing object. It specifies the expected structure and validation rules for the properties.

#### Using Joi for Route Validation

You can use the defined Joi schema to validate the data sent in your Express routes. For example, you can create a middleware function to validate data before processing a POST request:

```javascript
const { listingSchema } = require("../schema.js");

const validateListing = (req, res, next) => {
    let { error } = listingSchema.validate(req.body);
    if (error) {
        let errMsg = error.details.map((el) => el.message).join(",");
        throw new ExpressError(400, errMsg);
    } else {
        next();
    }
};

// Example route using the validateListing middleware
router.post("/", validateListing, wrapAsync(async (req, res, next) => {
    const newListing = new listing(req.body.listing);
    await newListing.save();
    req.flash("success", "New Listing Created!");
    res.redirect("/listings");
}));
```

In this example, `validateListing` middleware uses the Joi schema to validate the request body. If validation fails, it throws a custom `ExpressError` with a 400 status code and a concatenated error message.

These are the key aspects of error handling, custom error class, async error handling, and schema validation using Joi in your Express.js application. They ensure your application is robust and capable of handling various types of errors gracefully.


---------------------------------------------------------------------------------------


# Database Relationships and MongoDB Schema Design

In this document, we will discuss various types of database relationships, including one-to-one, one-to-many, many-to-many, one-to-few, and one-to-squillions. We will also explore the 6 Rules of Thumb for MongoDB Schema Design. To illustrate these concepts, we will use code examples in JavaScript with MongoDB.

## 1. SQL Relationships (One-to-One, One-to-Many, Many-to-Many)

SQL databases, such as MySQL or PostgreSQL, support various types of relationships. We'll briefly explain each type.

### 1.1. One-to-One Relationship

A one-to-one relationship occurs when one record in a table is related to only one record in another table.

**Example: Employee and EmployeeDetails tables.**

```sql
CREATE TABLE Employee (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50)
);

CREATE TABLE EmployeeDetails (
    EmployeeID INT PRIMARY KEY,
    SSN VARCHAR(20),
    ContactNumber VARCHAR(20)
);
```

### 1.2. One-to-Many Relationship

A one-to-many relationship occurs when one record in one table can be associated with multiple records in another table.

**Example: Customers and Orders tables.**

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(50)
);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE,
    TotalAmount DECIMAL(10, 2),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

### 1.3. Many-to-Many Relationship

A many-to-many relationship occurs when multiple records in one table are related to multiple records in another table through a junction table.

**Example: Students and Courses tables connected by an Enrollments table.**

```sql
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50)
);

CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseName VARCHAR(50)
);

CREATE TABLE Enrollments (
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);
```

## 2. One-to-Few Relationship

A one-to-few relationship is a special case of a one-to-many relationship where the "many" side usually has a small, fixed number of records.

**Implementation in user.js**

```javascript
const userSchema = new Schema({
    username: String,
    addresses: [
        {
            _id: false,
            location: String,
            city: String
        }
    ]
});
```

The `addresses` array can store multiple address objects, making it suitable for a one-to-few relationship.

## 3. One-to-Many Relationship in MongoDB

In a one-to-many relationship, one document in one collection can be associated with multiple documents in another collection. We will illustrate this using a Customers and Orders example.

**Implementation in customer.js**

```javascript
const mongoose = require("mongoose");
const { Schema } = mongoose;

main().then(() => console.log("connection success")).catch(err => console.log(err));

async function main() {
  await mongoose.connect('mongodb://127.0.0.1:27017/relationDemo');
}

//one to many
const orderSchema = new Schema({
    item: String,
    price: Number
});

const customerSchema = new Schema({
    name: String,
    orders: [
        {
            type: Schema.Types.ObjectId,
            ref: "Order"
        }
    ]
})

const Order = mongoose.model("Order", orderSchema);
const Customer = mongoose.model("Customer", customerSchema);

const addCustomer = async() => {
    let cust1 = new Customer({
        name: "Rahul Kumar"
    });

    let order1 = await Order.findOne({item: "chips"});
    let order2 = await Order.findOne({item: "chocolate"});
    let order3 = await Order.findOne({item: "samosa"});

    cust1.orders.push(order1);
    cust1.orders.push(order2);
    cust1.orders.push(order3);

    let result = await cust1.save();
    console.log(result)
}

const addOrders = async() => {
    let res = await Order.insertMany([
        {item: "samosa", price: "12"},
        {item: "chips", price: 10},
        {item: "chocolate", price: 40}
    ]);
    console.log(res)
}

addOrders();
addCustomer();
```

Customers can have multiple orders, and each order is represented as a reference to an Order document.

## Populating the Relationship

In a one-to-many relationship in MongoDB, you often have one document (e.g., a Customer) related to multiple documents (e.g., Orders). To retrieve this data efficiently and connect the related documents, you can use the "populate" function.

**Code Description:**

In the code example in customer.js, after adding a customer and associating orders with them, you can use the "populate" function to retrieve the data with populated orders.

```javascript
//populate
const findCustomer = async () => {
    let res = await Customer.find({}).populate("orders");
    console.log(res[0])
};

findCustomer();
```

Here's what "populate" does:

- The populate function is used on the query result (in this case, `Customer.find({})`).
  
- It takes the field name to populate as an argument, which is "orders" in this case. This tells MongoDB to replace the references to orders in the customer document with the actual order documents.
  
- After executing `populate("orders")`, the result contains customer data with the "orders" field populated with actual order documents.

The output of this code is a customer document with its orders populated, making it easy to access and work with the related data.

## 4. One-to-Squillions Relationship

A one-to-squillions relationship is a special case of a one-to-many relationship where the "many" side could potentially have a large number of records.

**Implementation Example: post.js**

```javascript
const mongoose = require("mongoose");
const { Schema } = mongoose;

main().then(() => console.log("connection success")).catch(err => console.log(err));

async function main() {
  await mongoose.connect('mongodb://127.0.0.1:27017/relationDemo');
}

//one to squillions
const userSchema = new Schema({
    username: String,
    email: String
});

const postSchema = new Schema({
    content: String,
    likes: Number,
    user: {
        type: Schema.Types.ObjectId,
        ref: "User"
    }
});

const User = mongoose.model("User", userSchema);
const Post = mongoose.model("Post", postSchema);

const addData = async() => {
    let user1 = new User({
        username: "rahulkumar",
        email: "rahulkumar@gmail.com"
    });

    let post1 = new Post({
        content: "Hello World!",
        likes: 7
    });

    post1.user = user1;

    await user1.save();
    await post1.save();
};

addData();

const getData

 = async() => {
    let res = await Post.findOne({}).populate("user", "username")
    console.log(res)
};

getData();
```

Users can have a large number of posts, and each post references a User document.

## 6 Rules of Thumb for MongoDB Schema Design

MongoDB schema design requires a different approach than SQL databases. Here are six rules of thumb:

1. **Favor embedding over referencing**: Whenever data is frequently read together, consider embedding it within a single document to reduce the number of queries.

2. **Avoid deep nesting**: Do not over-nest documents, as it can lead to inefficient queries.

3. **Optimize for the most common use cases**: Design your schema based on the queries you'll perform most often.

4. **Pre-join data for one-to-many relationships**: For one-to-many relationships, consider denormalizing data by embedding it within the parent document.

5. **Use references for one-to-few and many-to-many relationships**: Use references when dealing with one-to-few or many-to-many relationships to keep data manageable.

6. **Keep data consistent**: In MongoDB, you need to manage data consistency in your application code. Be prepared for cases where documents can be updated simultaneously.

By following these rules, you can design efficient and scalable MongoDB schemas. This document provides an overview of different types of database relationships and MongoDB schema design best practices. The code examples and explanations should help you understand and implement these concepts effectively.


---------------------------------------------------------------------------------------


# Pre and Post Mongoose Middleware

Mongoose is an Object Data Modeling (ODM) library for MongoDB and Node.js. It provides several middleware functions that allow you to execute code before or after specific operations on your Mongoose models, such as `findOneAndUpdate`, `findOneAndDelete`, or `findOneAndReplace`. These middleware functions are a powerful tool for adding custom behavior to your models.

## Pre Middleware

### Introduction

Pre middleware, also known as "before" middleware, is a way to execute code before a specific operation on a Mongoose model. It can be applied to operations like `findOneAndUpdate`, `findOneAndDelete`, or `findOneAndReplace`. Pre middleware is particularly useful when you need to validate or manipulate data before it's saved or updated in the database.

### Usage

You can add pre middleware to a Mongoose model using the `.pre()` method. Here's an example of how to use pre middleware with `findOneAndUpdate`:

```javascript
const mongoose = require('mongoose');

const mySchema = new mongoose.Schema({
  name: String,
  age: Number
});

mySchema.pre('findOneAndUpdate', function(next) {
  // Your custom logic here
  // 'this' refers to the query object
  console.log('Before findOneAndUpdate operation');
  next();
});
```

In this example, we've attached a pre middleware to the `findOneAndUpdate` operation on the `mySchema` model. The `next` function should be called when your custom logic is complete to proceed with the operation.

### Access to Query Object

The `this` keyword inside pre middleware functions refers to the query object. You can access the query conditions, update options, and more within the middleware function.

### Error Handling

You can also handle errors within pre middleware. If you call `next` with an argument (e.g., `next(err)`), it will trigger an error and stop the execution of the operation.

## Post Middleware

### Introduction

Post middleware, also known as "after" middleware, allows you to execute code after a specific operation has been completed. Like pre middleware, it can be applied to operations such as `findOneAndUpdate`, `findOneAndDelete`, or `findOneAndReplace`. Post middleware is useful when you need to perform actions after a database operation, such as logging, sending notifications, or updating related data.

### Usage

You can add post middleware to a Mongoose model using the `.post()` method. Here's an example of how to use post middleware with `findOneAndDelete`:

```javascript
const mongoose = require('mongoose');

const mySchema = new mongoose.Schema({
  name: String,
  age: Number
});

mySchema.post('findOneAndDelete', function(doc) {
  // Your custom logic here
  // 'doc' refers to the document that was deleted
  console.log(`Deleted document: ${doc}`);
});
```

In this example, we've attached a post middleware to the `findOneAndDelete` operation on the `mySchema` model. The `doc` argument passed to the middleware function refers to the document that was deleted.

### Access to Resulting Document

You can access the resulting document of the operation within post middleware, allowing you to perform actions based on the changes made to the database.

### Error Handling

You can also handle errors within post middleware. If an error occurs during the operation, it will be passed to the post middleware function as the second argument.

## Example Use Case: Logging

To illustrate the use of pre and post middleware, let's consider a scenario where you want to log all changes made to a document before and after a `findOneAndUpdate` operation:

```javascript
mySchema.pre('findOneAndUpdate', function(next) {
  // Log the original document before the update
  this.findOne()
    .then(doc => {
      console.log('Before Update - Original Document:', doc);
      next();
    })
    .catch(next); // Pass any error to the next middleware
});

mySchema.post('findOneAndUpdate', function(result) {
  // Log the updated document after the update
  console.log('After Update - Updated Document:', result);
});
```

In this example, the pre middleware logs the original document before the update, and the post middleware logs the updated document after the `findOneAndUpdate` operation is completed.

Pre and post middleware provide powerful mechanisms for customizing the behavior of your Mongoose models, making it easier to add functionality such as data validation, logging, and more to your application.


---------------------------------------------------------------------------------------


# Express Router

**What is Express Router?**

Express Router is a powerful middleware in the Express.js framework for building web applications. It allows you to modularize and organize your routes and handlers in a structured manner. With Express Router, you can separate different routes and their associated logic into distinct files, making your codebase more maintainable and organized.

**Key Benefits of Using Express Router**

1. **Modularity:** Express Router allows you to organize your routes into separate files or modules, making it easier to manage and scale your application.

2. **Middleware:** You can use middleware specific to a set of routes, making it easy to add functionality such as authentication or error handling.

3. **Cleaner Code:** It promotes cleaner and more readable code by structuring your routes logically.

**Using Express Router**

To demonstrate how to use Express Router, let's consider a basic example where we have a `server.js` file and a `user.js` file, which defines routes for user-related operations.

**server.js**

In your main application file, typically `server.js`, you set up your Express application and use the routers for different resource endpoints.

```javascript
const express = require("express");
const app = express();
const users = require("./routes/user.js");
const posts = require("./routes/post.js");

// Root route
app.get("/", (req, res) => {
    res.send("Hi, I am root!");
});

// Mount user and post routers
app.use("/users", users);
app.use("/posts", posts);

app.listen(3000, () => {
    console.log("Server is listening on port 3000");
});
```

In this code:
- We import the Express framework and set up an instance of the application.
- We define a root route to handle requests to the root URL.
- We use the `app.use` method to mount the user and post routers at their respective paths (`/users` and `/posts`).

**user.js**

In your `user.js` file, you define the routes and handlers specific to user-related operations.

```javascript
const express = require("express");
const router = express.Router({ mergeParams: true });

// Index route for users
router.get("/", (req, res) => {
    res.send("Home For users");
});

// Show route for a specific user by ID
router.get("/:id", (req, res) => {
    res.send("Show For users");
});

// Update route for users
router.post("/", (req, res) => {
    res.send("Update For users");
});

// Delete route for a specific user by ID
router.delete("/:id", (req, res) => {
    res.send("Delete For users");
});

module.exports = router;
```

In this `user.js` file:
- We create a router using `express.Router()`.
- We define various routes for user operations, such as index, show, update, and delete.
- Each route is associated with a specific HTTP method (GET, POST, DELETE), and they are defined with corresponding route handlers that send responses.

**Explanation of { mergeParams: true }**

The `{ mergeParams: true }` option in the `express.Router()` constructor is used to merge the parameters from the parent router (in this case, the `server.js` file) with the child router (in this case, the `user.js` file). This means that any route defined in the child router (`user.js`) will have access to the parameters defined in the parent router (`server.js`).

In our example, because we've used `app.use("/users", users)`, the `:id` parameter in routes defined in `user.js` can access the `:id` parameter defined in the "/users" route in `server.js`. This allows you to create routes that depend on parameters from both the parent and child routers.

For example, in the `user.js` file, the `router.get("/:id")` route can access the `:id` parameter from the parent router ("/users/:id"). This can be particularly useful for building nested routes or routes that require both parent and child parameters to function correctly.

In summary, `{ mergeParams: true }` enables the child router to access and use the parameters defined in the parent router, creating a unified parameter space for your routes.

By structuring your application in this way, you can keep your code organized and maintainable, especially as your application grows and you add more routes and functionality. Express Router is a powerful tool for managing your routes and middleware in a clean and modular fashion.


---------------------------------------------------------------------------------------


# Web Cookies

Web cookies are small pieces of data that a web server sends to a user's web browser. These cookies are then stored on the user's device and are sent back to the server with every subsequent request. Cookies are widely used to maintain state, track user activity, and store information about the user's preferences.

## Sending Cookies

In your provided code, you are using the `res.cookie` method to send cookies to the client's browser.

### `res.cookie()`

The `res.cookie()` method in Express is used to set a cookie in the response. It has the following syntax:

```javascript
res.cookie(name, value, [options]);
```

- **name:** The name of the cookie.
- **value:** The value of the cookie.
- **options:** An optional object containing various cookie options.

### Example

```javascript
app.get("/getcookies", (req, res) => {
    res.cookie("greet", "Hello");
    res.send("Sent you some cookies!");
});
```

In this code, when a user visits the `/getcookies` route, a cookie named "greet" with the value "Hello" is set in their browser.

## Cookie Parser

You are also using the `cookie-parser` middleware in your code.

### `cookie-parser`

`cookie-parser` is a middleware that parses cookies in the request object and makes them accessible via `req.cookies` and `req.signedCookies`. In your code, you have used it as follows:

```javascript
const cookieParser = require("cookie-parser");
app.use(cookieParser("secretcode"));
```

The "secretcode" parameter is used to sign cookies (which we'll cover in the "Signed Cookies" section).

## Signed Cookies

Signed cookies are cookies that have been digitally signed to ensure their integrity. This helps protect the data stored in the cookies from tampering by the client.

### Creating a Signed Cookie

You can create a signed cookie using the `res.cookie()` method and setting the `signed` option to `true`.

```javascript
app.get("/getsignedcookie", (req, res) => {
    res.cookie("made-in", "India", { signed: true });
    res.send("Signed the cookie.");
});
```

In this example, a cookie named "made-in" with the value "India" is set as a signed cookie.

### Verifying Signed Cookies

To verify signed cookies, you can access them using `req.signedCookies`.

```javascript
app.get("/verify", (req, res) => {
    console.log(req.signedCookies);
    res.send("Verified signed cookie.");
});
```

In the code above, the server prints the contents of the signed cookies and sends a response. The cookies are verified using the secret code specified when configuring `cookie-parser`.

These are the fundamental concepts and code examples related to web cookies, sending cookies, and signed cookies in your Express application. Cookies are essential for maintaining state and user sessions in web applications.


---------------------------------------------------------------------------------------


# Express Sessions

## What is State?

In web development, "state" refers to the data and information that a server or application retains between different interactions with a user. It enables the server to remember user-specific information across multiple requests, providing a sense of continuity and personalization in web applications. In Node.js, the "state" can be maintained using various mechanisms, such as sessions and cookies.

## Express Sessions

### Express Session Basics

Express.js provides a middleware called `express-session` for managing sessions in your Node.js application. Sessions are essential for maintaining state, tracking user data, and providing features like user authentication.

```javascript
const session = require('express-session');

const sessionOptions = {
    secret: 'keyboard cat', // A secret key used for session data encryption
    resave: false,          // Don't save session data on every request
    saveUninitialized: true, // Save new, uninitialized sessions
    cookie: {
        expires: Date.now() + 7 * 24 * 60 * 60 * 1000, // Session expiration time
        maxAge: 7 * 24 * 60 * 60 * 1000,               // Maximum age of the session
        httpOnly: true                                // HTTP only flag for security
    }
};

app.use(session(sessionOptions));
```

### Exploring Session Options

- `secret`: A secret key used for encrypting session data, enhancing security.
- `resave`: If false, the session data won't be saved on every request. It can improve performance.
- `saveUninitialized`: Set to true to save uninitialized (new) sessions.

The `cookie` object contains settings for session cookies, such as the `expires` and `maxAge` properties that determine session duration.

### Storing and Using Session Info

Sessions can store user-specific data between requests. In the example, `req.session.name` stores the user's name.

```javascript
app.get("/register", (req, res) => {
    let { name = "Unknown" } = req.query;
    req.session.name = name;
    // Flash messages to provide feedback
    if (name === "Unknown") {
        req.flash("error", "user not registered");
    } else {
        req.flash("success", "user registered successfully");
    }
    res.redirect("/hello");
});
```

### Using `connect-flash`

`connect-flash` is a middleware used to store and display flash messages. It allows you to temporarily store messages between requests.

```javascript
const flash = require('connect-flash');
app.use(flash());
```

In the example, `req.flash("error", "user not registered")` and `req.flash("success", "user registered successfully")` are used to set flash messages.

### Using `res.locals`

`res.locals` is an object that provides a way to pass data to your view templates. It is accessible in your EJS template (`page.ejs`) and can be used to display flash messages.

```javascript
app.get("/hello", (req, res) => {
    res.locals.successmsg = req.flash("success");
    res.locals.error = req.flash("error");
    res.render("page.ejs", { name: req.session.name });
});
```

In this code, `res.locals.successmsg` and `res.locals.error` make flash messages available in the `page.ejs` template.

### Cookies in `sessionOptions`

The `cookie` object within the `sessionOptions` configuration is used to control the behavior of session cookies.

- `expires`: Specifies the date when the session cookie will expire.
- `maxAge`: Sets the maximum age of the session cookie in milliseconds.
- `httpOnly`: When set to true, the cookie is accessible only through HTTP.

These settings control the lifespan and security of the session cookies used for user session management.

These notes provide an in-depth understanding of state management, sessions, cookies, and related concepts in a Node.js application using Express.js. The provided code snippets illustrate the practical implementation of these concepts in your `server.js` and EJS templates.


---------------------------------------------------------------------------------------


# User Authentication and Login System in Node.js Application

## Authentication

**Definition:** Authentication is the process of verifying the identity of a user or system.

**Purpose:** It ensures that the user is who they claim to be.

**In Development:** Authentication is achieved using Passport.js, which provides various strategies for authentication, including the local strategy.

## Authorization

**Definition:** Authorization is the process of granting or denying access to specific resources or actions based on the authenticated user's permissions.

**Purpose:** It controls what a user can and cannot do after they have been authenticated.

**In Development:** Authorization logic needs to be set up in your routes to determine what actions a user can perform.

### Key Points

- Never authenticate a user without proper authorization. Authentication alone doesn't guarantee access to specific resources.

- Always ensure proper access control mechanisms are in place to prevent unauthorized access.

## How Passwords Are Stored?

- Passwords should never be stored in plaintext in a database, as this poses a significant security risk.

### Hashing

**Definition:** Hashing is the process of converting a plaintext password into a fixed-length string of characters (the hash) using a one-way cryptographic algorithm.

**Purpose:** It protects passwords by making it extremely difficult to reverse the process and recover the original password from the hash.

- Always hash passwords before storing them in a database.

### Salting

**Definition:** Salting is the process of adding a random value (the salt) to the password before hashing it.

**Purpose:** It adds an extra layer of security by ensuring that the same password will have a different hash for each user.

- Always use a unique salt for each user.

- Always store the salt along with the hash in the database.

## Passport Getting Started

### What is Passport.js?

**Definition:** Passport is a popular Node.js library for authentication.

**Purpose:** It provides a flexible and modular framework for implementing various authentication strategies, including local authentication.

### Local Strategy with Local-Mongoose

- We are using the Local Strategy with Passport.js and the passport-local-mongoose plugin.

### User Model

- The User model schema defines the user data structure, including the email field.

### Configuring Strategy

- We configure the local strategy by using `passport.use(new LocalStrategy(User.authenticate()))`.

### Signup User

- The `/signup` route allows users to create an account.

- It uses `User.register(newUser, password)` to securely register the user.

### Key Points

- Always handle user registration securely and validate input.

- Never store passwords in plaintext. Use Passport's `passport-local-mongoose` for secure password storage.

```javascript
// Import the 'express' framework and create an instance of it.
const express = require("express");
const app = express();

// ... (other imports)

// Middleware and route setup

// Initialize Passport.js for authentication.
app.use(passport.initialize());

// Set up Passport.js sessions for user authentication.
app.use(passport.session());

// Configure and use the LocalStrategy for Passport.js, using the User model for authentication.
passport.use(new LocalStrategy(User.authenticate()));

// Serialize the user for sessions.
passport.serializeUser(User.serializeUser());

// Deserialize the user from sessions.
passport.deserializeUser(User.deserializeUser());

// ... (other routes)
```

```javascript
// Import required modules for the 'user.js' model.
const mongoose = require("mongoose"); // Import Mongoose for MongoDB interactions.
const Schema = mongoose.Schema; // Define a schema for the user model.
const passportLocalMongoose = require('passport-local-mongoose'); // Import 'passport-local-mongoose' for Passport.js integration.

// Define the schema for the User model, including required fields like 'email'.
const userSchema = new Schema({
    email: {
        type: String,
        required: true
    },
});

// Apply the 'passport-local-mongoose' plugin to the user schema for secure authentication.
userSchema.plugin(passportLocalMongoose);

// Export the User model, which is created using the schema.
module.exports = mongoose.model('User', userSchema);
```

```javascript
// Import required modules for the 'user.js' route.
const express = require("express"); // Import the 'express' framework.
const router = express.Router({ mergeParams: true }); // Create an express router with optional parameters.

const User = require("../models/user.js"); // Import the User model for user data.
const passport = require("passport"); // Import Passport.js for authentication.

// Define a route for user signup.
router.post("/signup", async (req, res) => {
    try {
        // Extract 'username', 'email', and 'password' from the request body.
        let { username, email, password } = req.body;

        // Create a new User instance with 'email' and 'username'.
        const newUser = new User({ email, username });

        // Register the user using Passport's 'User.register' method with the provided 'password'.
        const registeredUser = await User.register(newUser, password);

        // Log the registered user.
        console.log(registeredUser);
    } catch (e) {
        // In case of an error during registration, flash an error message and redirect to the signup page.
        req.flash("error", e.message);
        res.redirect("/signup");
    }
});

// ... (other routes)
```

These detailed comments explain each part of the code in our `app.js`, `user.js` model, and `user.js` route, including the purpose of each line or section.

These detailed notes cover the concepts of authentication, authorization, password storage, hashing, and salting, as well as the use of Passport.js for authentication and user registration. Always prioritize security by following best practices and using secure libraries like Passport.js and `passport-local-mongoose`.

Note: You should always handle errors gracefully and provide appropriate error messages to users. Never expose sensitive error details to the client.

### Login User

`passport.authenticate("local", { failureRedirect: "/login", failureFlash: true })`

The code is a route handler for user login. It utilizes Passport to authenticate users with a local strategy, which typically involves checking username and password. It includes a failure redirect and flash messages for user feedback.

```javascript
// In user.js

// Handle user login using Passport's local strategy
router.post("/login", saveRedirectUrl, passport.authenticate("local", {
    failureRedirect: "/login", // Redirect to the login page in case of authentication failure
    failureFlash: true // Enable flash messages for failure feedback
}), async (req, res) => {
    req.flash("success", "Welcome back to Wanderlust");
    let redirectUrl = res.locals.redirectUrl || "/listings"; // Determine the redirection URL after login
    res.redirect(redirectUrl);
});
```

- The route is a POST request for handling user login.

- `passport.authenticate("local", ...)` checks the user's credentials using the local strategy.

- If authentication fails, the user is redirected to the "/login" page and a failure flash message is displayed.

- After a successful login, a success flash message is displayed.

- The user is then redirected to either the original URL they attempted to access or "/listings" if no specific URL was saved.

### Connecting Login Route with Middleware

`req.isAuthenticated()`

This middleware checks if a user is authenticated (logged in) before allowing access to specific routes. It is often used to protect routes that require a user to be logged in.

```javascript
// In middlewares.js



// Middleware to check if the user is authenticated
module.exports.isLoggedIn = (req, res, next) => {
    if (!req.isAuthenticated()) {
        req.session.redirectUrl = req.originalUrl; // Save the original URL for redirection
        req.flash("error", "Please log in to take action");
        res.redirect("/login");
    } else {
        next(); // Proceed to the next middleware or route
    }
};
```

- The `isLoggedIn` middleware checks if the user is authenticated using `req.isAuthenticated()`.

- If not authenticated, the original URL is saved in the session for future redirection.

- A flash message is displayed, and the user is redirected to the "/login" page.

- If authenticated, the user is allowed to proceed to the next middleware or route.

### Logout User

`req.logout()`

This route logs the user out of the system using the `req.logout()` method provided by Passport.

```javascript
// In user.js

// Handle user logout
router.get("/logout", saveRedirectUrl, (req, res, next) => {
    req.logout((err) => {
        if (err) {
            return next(err);
        }
        req.flash("success", "You are logged out");
        let redirectUrl = res.locals.redirectUrl || "/listings"; // Determine the redirection URL after logout
        res.redirect(redirectUrl);
    });
});
```

- This route logs the user out and displays a success flash message.

- The user is redirected to either the original URL they attempted to access or "/listings" if no specific URL was saved.

### Login After Signup

`req.login()`

This code handles user registration and login simultaneously. It registers a new user and immediately logs them in using `req.login()`.

```javascript
// In user.js

// Handle user signup and login
router.post("/signup", async (req, res) => {
    try {
        // Extract user data from the request body
        let { username, email, password } = req.body;
        const newUser = new User({ email, username });

        // Register the new user with Passport
        const registeredUser = await User.register(newUser, password);

        req.login(registeredUser, (err) => {
            if (err) {
                return next(err);
            }
            req.flash("success", "Welcome to Wanderlust");
            res.redirect("/listings");
        });
    } catch (e) {
        req.flash("error", e.message);
        res.redirect("/signup");
    }
});
```

- This route handles user registration and login.

- User data is extracted from the request body.

- A new user is created and registered using Passport's `User.register` method.

- Upon successful registration, the user is immediately logged in using `req.login()`.

- Success or error flash messages are displayed accordingly.

### Post-Login Page Handling

`res.locals.redirectUrl`

This middleware retrieves the saved redirect URL from the session and makes it available in the `res.locals` object for use in subsequent routes.

```javascript
// In middlewares.js

// Middleware to retrieve the saved redirect URL
module.exports.saveRedirectUrl = (req, res, next) => {
    res.locals.redirectUrl = req.session.redirectUrl;
    next();
};
```

- This middleware makes the saved redirect URL accessible via `res.locals.redirectUrl`.

- It is typically used to determine the URL to which the user should be redirected after login or logout.

These detailed notes provide a comprehensive explanation of the user authentication and login system in our Node.js application. Understanding these components is essential for implementing user management and enhancing the user experience in your web application.


---------------------------------------------------------------------------------------


# Authorization in Web Applications

## What is Authorization?

Authorization is a crucial aspect of web application security that governs access control to specific resources or actions within a system. It determines who is allowed to perform certain operations, access particular data, or execute privileged actions based on their identity, role, or permissions.

## Key Concepts of Authorization

### 1. Authentication:

Authentication is the process of verifying the identity of a user or system attempting to access a resource. It ensures that users are who they claim to be, usually by using credentials like usernames and passwords.

### 2. Access Control:

Access control defines the rules and policies that determine what actions users or systems are allowed to perform. It involves defining roles, permissions, and restrictions for different users or groups.

### 3. Authorization Mechanisms:

Authorization mechanisms enforce access control rules. These can be implemented on both the client and server sides.

## Client-side Authorization

Client-side authorization controls access to resources or actions directly within the user's browser. It is often used for enhancing user experience and minimizing unnecessary requests to the server.

### Code Explanation - Client-side Authorization

#### "show.ejs" Template

```ejs
<% layout('/layouts/boilerplate') -%>
<div class="row mt-3" data-scroll-section>
    <!--other template content -->

    <!--Client side Authorization for delete and edit listing -->
    <% if(currUser && currUser._id.equals(list.owner._id)) { %>
        <div class="del-opacity">
            <form class="show-form-ed" method="GET" action="/listings/<%= list._id %>/edit">
                <button class="show-ed disabled-element">Edit
                    <span class="material-symbols-outlined">
                        edit
                    </span>
                </button>
            </form>
            <div class="show-div">
                <button class="del disabled-element">
                    Delete<span class="material-symbols-outlined">delete</span>
                </button>
            </div>
        </div>
    <% } %>
   <!--other template content -->
</div>
```

**In this code:**

- Client-side authorization is implemented using embedded JavaScript (EJS) templating.
- It checks if `currUser` is authenticated and if the authenticated user's `_id` matches the owner's `_id` of the listing.
- If the condition is met, it allows the user to see the "Edit" and "Delete" buttons, effectively controlling access to these actions on the client side.
- This client-side authorization enhances user experience by only displaying the "Edit" and "Delete" buttons to the owner of the listing, ensuring that only authorized users can perform these actions without unnecessary server requests.

## Server-side Authorization

Server-side authorization is the primary layer of security that enforces access control rules on the server. It is responsible for ensuring that only authenticated and authorized users can perform specific actions, such as deleting or editing a listing.

### Code Explanation - Server-side Authorization

#### "listing.js" (Server-side Authorization to Delete Listing)

```javascript
app.delete(isLoggedIn, isOwner, wrapAsync(async (req, res) => {
  let { id } = req.params;
  await listing.findByIdAndDelete(id);
  req.flash("success", "Listing Deleted!")
  res.redirect("/listings")
}))
```

**In this code:**

- The route for deleting a listing is protected by server-side authorization using middleware functions `isLoggedIn` and `isOwner`.
- `isLoggedIn` ensures that the user is authenticated.
- `isOwner` checks if the authenticated user matches the owner of the listing.
- If both conditions are met, the listing is deleted, and a success message is flashed.

#### "middlewares.js" (`isOwner` Middleware)

```javascript
module.exports.isOwner = async (req, res, next) => {
    const { id } = req.params;
    let Listing = await listing.findById(id);
    if (!Listing.owner._id.equals(res.locals.currUser._id)) {
        req.flash("error", "You are not the owner of this listing");
        return res.redirect(`/listings/${id}`);
    }
    next();
};
```

**In this code:**

- The `isOwner` middleware is used to verify if the user requesting the action is the owner of the listing.
- It retrieves the listing by its ID and compares the owner's `_id` with the currently authenticated user's `_id`.
- If the user is not the owner, an error message is flashed, and they are redirected to the listing's page.

## Conclusion

Authorization plays a crucial role in ensuring the security and integrity of web applications. Client-side authorization enhances user experience by controlling access within the user interface, while server-side authorization enforces access control rules on the server to protect sensitive operations. Combining both client and server-side authorization ensures a robust and secure application.

Please note that security practices may vary, and it's essential to continuously update and adapt authorization mechanisms to protect against evolving security threats.


---------------------------------------------------------------------------------------


# MVC (Model-View-Controller) and `router.route` in Node.js Web Application

## Introduction to MVC

MVC (Model-View-Controller) is a software architectural pattern commonly used in web development to organize and structure code in a way that promotes modularity, maintainability, and separation of concerns. MVC divides an application into three interconnected components: Model, View, and Controller.

### Model

**Purpose:** The Model represents the application's data and business logic. It interacts with the database, performs data manipulation, and enforces data integrity.

**In Node.js applications:** A Model is defined using libraries like Mongoose for MongoDB. It specifies the data structure, validation, and interactions with the database.

### View

**Purpose:** The View is responsible for the presentation and user interface. It displays the data to users and handles user input. It should be as passive as possible, without containing business logic.

**Views:** Often created using templating engines like EJS or HTML, which are populated with data from the Model.

### Controller

**Purpose:** The Controller acts as an intermediary between the Model and the View. It receives user input from the View, processes it, and updates the Model or directs the View to render specific content.

**Controllers:** Implemented as JavaScript functions that handle HTTP requests and responses. They orchestrate the flow of data and operations.

## `router.route` in Web Development

In web development, especially in frameworks like Express.js for Node.js applications, `router.route` is a method used to define and manage routes. It simplifies the creation of multiple HTTP methods (e.g., GET, POST, PUT, DELETE) for a particular route, allowing for better code organization and readability.

**Purpose of `router.route`:**

1. **Simplification:** `router.route` simplifies route definition by grouping multiple HTTP methods for the same path, reducing redundant code.

2. **Readability:** It improves code readability by making it clear which HTTP methods are available for a given route.

3. **Structure:** Helps maintain a structured and organized codebase by grouping related routes together.

### Code Example

```javascript
const express = require("express");
const router = express.Router();

// Define routes for a resource using router.route
router.route("/example")
    .get((req, res) => {
        // Handle GET request
    })
    .post((req, res) => {
        // Handle POST request
    })
    .put((req, res) => {
        // Handle PUT request
    })
    .delete((req, res) => {
        // Handle DELETE request
    });

module.exports = router;
```

In this example, `router.route` groups the routes for the "/example" resource and defines handlers for various HTTP methods. This structure enhances code organization and readability in web applications.

## MVC Components in Detail

### Model

#### `models/listing.js`

```javascript
const mongoose = require("mongoose");
const Schema = mongoose.Schema;
const Review = require("./review.js");

const listingSchema = new Schema({
    // ... fields and validations ...
});

listingSchema.post("findOneAndDelete", async (listing) => {
    // Middleware to delete associated reviews when a listing is deleted
    if (listing) {
        await Review.deleteMany({_id: {$in: listing.reviews}});
    }
});

const Listing = mongoose.model("Listing", listingSchema);
module.exports = Listing;
```

- Defines the schema for the 'Listing' model using Mongoose.
- Includes fields, validations, and a post middleware for deleting associated reviews when a listing is deleted.
- Creates the model from the schema and exports it for use in other parts of the application.

### View

#### `views/listings/index.ejs`

```ejs
<% layout('/layouts/boilerplate') -%>
    <!-- HTML and EJS code for rendering the 'All Listings' view -->
```

- An EJS template used for rendering the 'All Listings' view.
- Dynamically inserts data from 'allListings' into the HTML to generate the view displayed to the user.

### Controller

#### `controllers/listings.js`

```javascript
const Listing = require("../models/listing.js");
const ExpressError = require("../utils/ExpressError.js");

module.exports.index = async (req, res) => {
    // Controller function to render the index page with all listings
    try {
        const allListings = await Listing.find({});
        res.render("listings/index.ejs", { allListings });
    } catch (error) {
        console.error(error);
        res.status(500).send("Internal Server Error");
    }
};

module.exports.create = async (req, res, next) => {
    // Controller function to create a new listing
    try {
        // ... handle listing creation ...
        res.redirect("/listings");
    } catch (error) {
        // ... handle errors ...
    }
};
```

- Defines two controller functions for handling listings: 'index' and 'create'.
- 'index' retrieves all listings from the model and renders the 'index.ejs' view.
- 'create' handles the creation of a new listing, including file upload, model creation, and redirection.

### `router.route`

#### `routes/listing.js`

```javascript
const express = require("express");
const router = express.Router();
const wrapAsync = require("../utils/wrapAsync.js");
const { isLoggedIn, currUrl, isOwner, validateListing, isYou } = require("../middleware.js");
const listingController = require("../controllers/listings.js");
const multer = require('multer');
const { storage } = require("../cloudConfig.js");
const upload = multer({ storage });

// Define routes for the 'listing' resource
router.route("/")
    .get(currUrl, wrapAsync(listingController.index

))
    .post(isLoggedIn, upload.single('listing[image]'), validateListing, wrapAsync(listingController.create));

module.exports = router;
```

- Defines routes for the 'listing' resource using the Express.js Router.
- Applies necessary middleware functions and the 'listingController' for route handling.
- Two HTTP methods are defined for the '/listings' route: 'GET' to display listings and 'POST' to create a new listing.
- Middleware functions such as 'isLoggedIn', 'upload', and 'validateListing' are applied to ensure proper request handling.

## Conclusion

MVC and the use of "router.route" are essential concepts in web development, promoting clean code architecture and efficient route management. These practices help developers create scalable, maintainable, and organized web applications. The provided code examples and detailed explanations give a comprehensive understanding of how these concepts are implemented in a Node.js web application.


---------------------------------------------------------------------------------------
---------------------------------------------------------------------------------------
