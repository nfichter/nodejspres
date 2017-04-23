## Node.js

A presentation by Noah Fichter and Chloe Delfau.

### What is Node.js?
```markdown
- Node.js is a **platform** built on Chrome's JavaScript runtime for easily building fast and scalable network applications. 
- It uses an **event-driven, non-blocking I/O model** that makes it **lightweight** and **efficient**, perfect for data-intensive **real-time applications** that run across distributed devices.
- In essence, it is a **backend command line tool** that allows you to use JavaScript on a server
```

### What are the benefits of using Node?
```markdown
Asynchronous
  - Don’t have to wait for one process to end before beginning another (non-blocking model)
  - Very fast and efficient
  - Should not be used for applications heavy on CPU usage
**Event Driven**
  - After initialization, it sets up event listeners and waits for one to occur
  - When one occurs, it triggers the function set to it (callback function)
  - Supports concurrent events
  - We already use it this way when using JS in the browser, so we know how to work with events
**Uses JS on both frontend and backend**
  - Breaks down the barrier between frontend and backend
  - Can replace Python & Flask entirely
  - Allows easy passing of data using JSON
  We don’t have to convert between different data types
```

### What is NPM?
```markdown
**NPM** is the **Node Package Manager**
  - Used to install packages and modules, similar to pip for Python
  - Comes with Node.js, so don’t worry about installing it yourself
  
Example command line usage:
  `$ npm install express  
  (-g to install globally instead of only the application you’re working in)
  (--save to save it in the package.json file)`
```

### What are some popular modules?
```markdown
Frameworks - similar to Flask, Django
  - Express.js
Template Engines - similar to Jinja
  - Pug, EJS, Handlebars
Utilities
  - Path, OS, API Modules, Compilers, nodemon
Database ORM (Object Relational Mappers)
  - Mongoose, MongoJS - used to interact with MongoDB
```

### How do I get started with Node?
```markdown
Windows & Mac	
  - [https://nodejs.org/en/download/](https://nodejs.org/en/download/)
Linux
  - Google it
  `$ sudo apt-get install python-software-properties
  $ curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
  $ sudo apt-get install nodejs`
Check that you correctly installed
  `$ node -v
  $ npm -v`
NOTE: while node uses JS, some functions and objects that are built into browser-based JS like document and window cannot be used
```

### Simple Example Server w/ Node & Express
```markdown
`$ npm init`
  - creates package.json file, necessary for all node.js applications
`$ node <entry file name>
http://<host>:<port>`
2 ways to install express.js:
  1. `$ npm install express --save`
  2. add to package.json then `$ npm install`
```

### Example Code
```markdown
`// Modules required
var http = require("http");
var fs = require("fs");

// Server info
var host = '127.0.0.1';
var port = '3000';

// When you call a module’s method, you attach a “callback function” that runs when the method completes.
// In this case, readFile reads index.html and takes a function(err,html) as its callback
// Once it finishes reading the file, it runs the function which creates a server
fs.readFile("./index.html", function(err,html) {
	if (err) {
		console.log(err);
		return;
	}

	//Here, createServer does not have an initial argument; it only needs a callback function(request,response)
	//Once it finishes creating the server, it sends a response to the user
	var server = http.createServer(function(req, res) {
		res.statusCode = 200;
		res.setHeader("Content-Type","text/html");
		res.write(html);
		res.end();
	})

	//Finally, the server now has a listen function that takes the port and host it should listen on and
  //a callback function once the event is fired off (aka, once someone connects)
	server.listen(port, host, function() {
		console.log("Server running on port "+port);
	});
});

=====================================

<!DOCTYPE html>
<html>
<head>
	<title>Hello World</title>
</head>
<body>
	<h1>Hi there</h1>
</body>
</html>`
```
