---
layout: presentation
title: Express.js
permalink: /slides/express/
---

class: center, middle

# Express.js

Throw together a quick Javascript-based web server.

---

# Agenda

1. [Overview](#overview)
1. [Routing Requests](#routes)
1. [Middleware](#middleware)
1. [Debugging Express](#debugging)
1. [Handling HTTP POST Requests](#post)
1. [Handling File Uploads](#uploads)
1. [Proxying Requests](#proxying)
1. [Environmental Variables](#environment)
1. [Parameters](#parameters)
1. [Template Engines](#template-engines)
1. [Authentication](#authentication)
1. [Database Integration](#databases)
1. [Conclusions](#conclusions)

---

name: overview

# Overview

---

template: overview
name: concept

## Concept

[Express.js](https://expressjs.com/) is a web server framework that runs in the Node.js Javascript environment.

--

- Recall that a **web server** responds to incoming HTTP(S) requests from a **web browser**, or other client app

--

- The server sends an **HTTP response** to each request, including some content if the request is successful, or an HTTP error message if it fails.

--

![HTTP request and response](../images/client_server_multiplicity.png)

---

template: overview

## Setting up an NPM project

Using **express** assumes you have initialized a Node project with the Node Package Manager (NPM).

--

- The `npm init` command will ask for some project details and auto-generate the NPM project's settings file, `package.json`.

--

```bash
cd back-end # or whichever directory you want to house the web server code
npm init # enter `server.js` as the entry point, when asked.
```

--

- Now you can install express and automatically add it into the list of dependencies outlined in the project's `package.json` file.

--

```bash
npm install express --save
```

---

template: overview
name: app-setup

## Set up a placeholder Express app

Place the following into a file named `app.js` - this creates an express web server app that serves no purpose... for now.

```javascript
// import and instantiate express
const express = require("express") // CommonJS import style!
const app = express() // instantiate an Express object

// we will put some server logic here later...

// export the express app we created to make it available to other modules
module.exports = app
```

--

- Do not fear, we will add some code to this file later to tell it how to handle incoming HTTP(S) requests.

---

template: overview

## Create code to launch the express app

Put the following into a file named `server.js`, and enure the `package.json` settings file mentions this as the project's `main` entry point.

```javascript
#!/usr/bin/env node

const server = require("./app") // load up the web server

const port = 3000 // the port to listen to for incoming requests

// call express's listen function to start listening to the port
const listener = server.listen(port, function () {
  console.log(`Server running on port: ${port}`)
})

// a function to stop listening to the port
const close = () => {
  listener.close()
}

module.exports = {
  close: close,
}
```

---

template: overview

## Launch it!

You are now ready to run the express app.

--

- Use `npm start`, the default script to run an NPM project.

--

- `npm start` is really just an alias for `node server`, assuming your `package.json` has `server.js` listed as the main script.

--

- Every time you change the code, you must stop (`Control-C`) and restart the server. This can be tedious.

--

- A popular 3rd-party module called `nodemon` can do this for you. Install it and have it automatically saved into your `package.json` file's list of development-specific dependencies.

```bash
npm install nodemon --save-dev
```

--

- Run `nodemon server` to let nodemon handle stopping and restarting the server with each code change.... the luxury of automation!

---

template: overview

## What now?

You now presumably have an Express server up-and-running on your local machine at port 3000. What to do with it?

--

- Our goal is to be able to **make HTTP(S) requests** to this back-end from a front-end client, be that a web browser or a desktop or mobile native app of some kind.

--

- To do that, we must instruct our app **what to do when an HTTP(S) request is made** at the port we're listening to.

--

- Doing such setup is called creating **routes**.

---

template: overview

## Follow along

The Express.js code examples in this slide deck are available on GitHub - the code is already set up and ready to run.

--

- Fork and clone [the companion git repository](https://github.com/nyu-software-engineering/express-js-starter-app).

--

- Install all dependencies by running `npm install`.

--

- Launch the app by running `nodemon server`.

---

name: routes

# Routing Requests

--

## Concept

Routes instruct express what to do in response to incoming HTTP(S) requests.

--

- Each route listens for requests to a particular URL, e.g. `/`, `/animals`, `/animals/narwhal`, etc.

--

- Each route can be set to listen for a specific type of HTTP request, most commonly **GET** or **POST**.

--

- Each route then responds with an **error message** or **some content**.

--

- Content in the response sent to the client is most commonly formatted as **HTML** or **JSON**.

--

- For requests for images, videos, or other **static files** - express can simply send those static files in the response.

---

template: routes

## Example 1

A route that listens for any **HTTP GET** request for the `/` path, and responds with the **plain text**, 'Hello!'.

```javascript
app.get("/", (req, res) => {
  res.send("Hello!")
})
```

--

- This could be placed in the middle of the [app.js file](#app-setup).

---

template: routes

## Example 2

A route that listens for any **HTTP GET** request for the `/html` path, and responds with a **static HTML file**.

```javascript
// respond to any GET requests for /html-example with an HTML document named some-page.html
app.get("/html-example", (req, res) => {
  res.sendFile("/public/some-page.html", { root: __dirname })
})
```

--

- A request for `/html-example` will simply respond with the contents of the HTML file located at `public/some-page.html`.

--

- This is an example of serving up a _static_ file - the content of the file does not change from one request to the next.

---

template: routes

## Example 3

Inform express that the `public` directory contains all static files that it should just blindly serve up when requested under the `/static` route.

```javascript
// tell express that any requests for '/static' will map out to the 'public' directory, where we place static content
app.use("/static", express.static("public"))
```

--

- A request for `/static/html-example.html` would serve up the file located at `public/html-example.html`.

--

- A request for `/static/css/main.css` would serve up the file located at `public/css/main.css`.

--

- A request for `/static/images/donkey.jpg` would serve up the file located at `public/images/donkey.jpg`.

--

- This is useful for serving any static HTML, CSS, image, audio, video or other content.

---

template: routes

## Example 4

JSON is a common format for sending data between client and server in apps.

```javascript
// route for HTTP GET requests to /json-example
app.get("/json-example", (req, res) => {
  // assemble an object containing the data we want to send
  const body = {
    title: "Hello!",
    heading: "Hello!",
    message: "Welcome to this JSON document, served up by Express",
    imagePath: "/static/images/donkey.jpg",
  }

  // send the response as JSON text to the client
  res.json(body)
})
```

--

- A request for `/json-example` would receive this object in JSON format in response.

--

- Client-side code would presumably use this data in some way.

---

name: middleware

# Middleware

--

## Concept

As you have seen, when a request is made, a route function executes that determines how to respond.

--

- These route functions are automatically passed two objects by express, `req` and `res`, representing the HTTP request and the HTTP response.

```javascript
app.get("/", (req, res) => {
  //...
})
```

--

- Sometimes, it is useful to modify the content of one or both of those objects prior to calling the route functions.

--

- Other times, it's useful to perform 'side-effects', such as maintain log files of all requests.

--

- Middleware are functions executed prior to the routes functions that can handle these two sorts of tasks with any request.

---

template: middleware

## Setting up a middleware function

We call express's `use` function and pass it our middleware function as an argument.

```javascript
app.use((req, res, next) => {
  //...
})
```

--

- Like routes, middleware functions are passed `req` and `res` objects, representing the HTTP request and response.

--

- Middleware functions receive third argument, `next`, which is a callback function to trigger the next middleware function to be run.

--

- Middleware functions can thus be chained together, with each one calling the next. Once they have all been called, any relevant route function is executed.

---

template: middleware

## Example 1

Imagine two middleware functions ...

First:

```javascript
// custom middleware - first
app.use((req, res, next) => {
  // make a modification to either the req or res objects
  res.addedStuff = "First middleware function run!"
  // run the next middleware function, if any
  next()
})
```

Second:

```javascript
// custom middleware - second
app.use((req, res, next) => {
  // make a modification to either the req or res objects
  res.addedStuff += " Second middleware function run!"
  // run the next middleware function, if any
  next()
})
```

---

template: middleware

## Example 1 (continued)

... followed by a route:

```javascript
// route for HTTP GET requests to /middleware-example
app.get("/middleware-example", (req, res) => {
  // grab data passed along by the middleware, if available
  const message = res.addedStuff
    ? res.addedStuff
    : "Sorry, the middleware did not work!"
  // use the data added by the middleware in some way
  res.send(message)
})
```

--

- When express detects an incoming request, it will automatically call the first middleware function.

--

- The first middleware function adds a custom property named `addedStuff` to the `res` object and then passes control to the next middleware function, which appends more text to this property.

--

- The route is then automatically called and detects the custom property and sends it blindly to the client, for simplicity of the example.

---

name: debugging

# Debugging

--

## Concept

As you work on your express-enabled web servers, you will inevitably want to be aware of a few useful debugging tools.

--

- [morgan](https://github.com/expressjs/morgan) - 3rd-party middleware for logging all incoming HTTP requests

--

- [Postman](https://www.postman.com/) - a desktop app for making HTTP requests to a web server without requiring any front-end code.

--

- [mocha](https://mochajs.org/) and [chai](https://www.chaijs.com/) - popular 3rd-party modules for unit testing code, i.e. making sure all functions behave as they are expected to in all circumstances.

--

- [ngrok](https://ngrok.io) - a tool to provide public HTTPS access to a server running on your local machine

---

template: debugging

## Morgan

[Morgan](https://github.com/expressjs/morgan) will log a bit of info about each incoming request to the server's command shell output.

--

- Install the morgan module and save it to your project's list of dependencies in the `package.json` settings file.

```bash
npm install morgan --save
```

--

- Import it into any code file where you define routes that handle incoming requests.

```javascript
const morgan = require("morgan") // middleware for nice logging of incoming HTTP requests
```

--

- Set it as express middleware and specify which style of logs you desire - there are several output styles specified in their documentation.

```javascript
app.use(morgan("dev")) // dev style gives a concise color-coded style of log output
```

---

template: debugging

## Postman

[Postman](https://www.postman.com/) is a desktop app that allows you to trigger custom HTTP requests to your local development web server.

--

- This relieves you from having to write (and debug) front-end code while your focus is on perfecting the back-end.

--

- Once installed, get started by clicking the `Create a request` link on the Launchpad screen. Enter a route you have set up in express, such as `http://localhost:3000/`, and click the `Send` button.

--

- It is possible to tweak request settings to simulate any kind of request a front-end could make.

--

- It is possible to save requests you want to run frequently so you can quickly test them as you work on the code.

--

- The git repository accompanying these slides includes a file named `express-js-starter-app.postman_collection.json` that can be imported into Postman to easiy try out all these routes.

---

template: debugging

## Mocha and chai

[Mocha](https://mochajs.org/) and [chai](https://www.chaijs.com/) are two 3rd-party Node.js modules often used together to perform unit testing of code.

--

- a **unit test** is a test that can be written to validate a function and make sure it always works correctly regardless of context.

--

- We are not concerned with unit testing for now, but will return to it in detail later. It never hurts to try it out now.

---

template: debugging

## ngrok

[ngrok](https://ngrok.io/) is a tool that will provide a publically-accessible web address that forwards requests to a server you run on your local machine.

--

- Install ngrok and make sure it is in your system's PATH variable.

--

- Start your server, for example by running `nodemon server` to launch an express.js server locally.

--

- Expose the port at which your server is running locally to the public, with `ngrok http 3000`, where `3000` is the port your express server is running on.

--

- ngrok will output a public URL (both `http` and `https`) that you and others can use to reach the web server running locally on your own machine.

--

- requests made to that ngrok URL will be forwarded to your local server via a secure tunneling connection.

---

name: post

# Handling HTTP POST Requests

--

## Concept

Many web sites and apps allow users to submit data to a server via forms. Usually these requests are submitted via HTTP POST, with data in the body (i.e. payload) of the request.

--

- Express now includes middleware (formerly a separate project called `body-parser`) that is useful in parsing data in incoming HTTP POST request body.

--

- Tell express to `use` this request body parser middleware.

```javascript
app.use(express.json()) // decode JSON-formatted incoming POST data
app.use(express.urlencoded({ extended: true })) // decode url-encoded incoming POST data
```

---

template: post

## Example

Imagine an HTML form that sends data to the server via HTTP POST...

```html
<form action="/post-example" method="POST">
  <input type="text" name="your_name" placeholder="Your name" /> <br />
  <input type="text" name="your_email" placeholder="Your email" /> <br />
  <input type="checkbox" name="agree" /><label
    >I agree to your onerous conditions</label
  >
  <br />
  <input type="submit" value="Submit!!!" />
</form>
```

--

... and an Express route receives that data after the middleware has kindly added it to the `req` object's `body` property.

```javascript
app.post("/post-example", (req, res) => {
  const name = req.body.your_name
  const email = req.body.your_email
  const agree = req.body.agree
  // now do something amazing with this data...
  // ... then send a response of some kind
})
```

---

name: uploads

# Handling File Uploads

---

template: uploads

## Concept

Clients can upload files to the server as part of their HTTP POST requests.

--

- There exist 3rd-party middlewares, such as [multer](https://github.com/expressjs/multer), that make extracting the files from the request easy.

--

- Install it into your express app and save as a dependency to the `package.json` config file:

```bash
npm install multer --save
```

--

- Import it into the file that handles the upload routes:

```bash
const multer = require('multer')
```

---

template: uploads

## Setup

`multer` can save uploaded files to a number of different destinations. Here, we tell `multer` to save uploaded files into a directory named `public/uploads`, with a filename based on the current time.

```javascript
// enable file uploads saved to disk in a directory named 'public/uploads'
const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, "public/uploads")
  },
  filename: function (req, file, cb) {
    cb(
      null,
      `${file.fieldname}-${Date.now()}${path.extname(file.originalname)}`
    )
  },
})
```

Then instantiate a `multer` object.

```javascript
const upload = multer({ storage: storage })
```

---

template: uploads

## Client-side code

Take the following HTML form that allows users to upload files to the server as part of the POST request.

```html
<form action="/upload-example" method="POST" enctype="multipart/form-data">
  <input name="my_files" type="file" multiple />
  <input type="submit" value="Submit!!!" />
</form>
```

--

- Note that the `form` tag has an addition attribute, `enctype` that must be included for forms with file uploads.

--

- Note also the optional `multiple` attribute that allows the user to upload multiple files, if desired.

---

template: uploads

## Server-side code

`multer` middleware will automatically save any uploaded files in the request into the specified directory, rename them as instructed, and make a field named `req.files` containing the paths to the files on the server.

```javascript
// route for HTTP POST requests for /upload-example
app.post("/upload-example", upload.array("my_files", 3), (req, res, next) => {
  // check whether anything was uploaded
  if (req.files) {
    // success! send data back to the client, e.g. some JSON data
    const data = {
      status: "all good",
      message: "yup, the files were uploaded!!!",
      files: req.files,
    }
    res.json(data) // send respose
  }
})
```

--

- Note the code, `upload.array('my_files', 3)`, instructs `multer` to store no more than 3 files, coming from an HTML element named `my_files`.

---

name: proxying

# Proxying Requests

--

## Concept

We often use our web server as a sort of proxy, relaying requests from the client to some other service, such as an external API or database, and relaying the responses from these other services back to the client.

--

- For example, for an animal-relate app, the client might request data about one or more animals.

--

- A route function on the web server will handle this request and make a request to a database or external API for the animal data.

--

- The API or database will send the list of animals back to the express route function.

--

- The express route function will pass the list of animals to the client as the web server response.

---

template: proxying

## Example

Let's see how to have an express route proxy a request from the client to an API and back, with no modification of the data.

--

- The 3rd-party middleware, [axios](https://www.npmjs.com/package/axios), is useful for issuing requests to APIs. Install it and save it to the `package.json` list of dependencies:

```bash
npm install axios --save
```

--

name: api-call

- Create a route that issues a request to an API and forwards the results to the client

```javascript
// proxy requests to/from an API
app.get("/proxy-example", (req, res, next) => {
  // use axios to make a request to an API for animal data
  axios
    .get("https://my.api.mockaroo.com/animals.json?key=d9ddfc40&num=10")
    .then(apiResponse => res.json(apiResponse.data)) // pass data along directly to client
    .catch(err => next(err)) // pass any errors to express
})
```

---

name: environment

# Environmental Variables

--

## Concept

Hard-coding values like credentials for APIs and databases directly into production code is considered bad practice.

--

- If the code is checked into a version control system, you may inadvertently disclose private credentials to the public.

--

- If those credential settings are hard-coded in multiple places, code maintenance becomes an issue.

---

template: environment

## Setup

A 3rd-party middleware named, [dotenv](https://www.npmjs.com/package/dotenv), makes it easy to store such values as environmental variables that are then imported into the app.

--

- Install it and save it to the `package.json` list of dependencies:

```bash
npm install dotenv --save
```

--

- Import it into any file where you have a need for the credentials or other private data.

```javascript
require("dotenv").config({ silent: true })
```

--

- Now, environmental variables declared in a hidden file named `.env` will be available in your code as `process.env.MY_VARIABLE_NAME`.

---

template: environment

## Usage

Let's place the credentials for the API we used [earlier](#api-call) into a file named `.env`:

```bash
API_BASE_URL=https://my.api.mockaroo.com/animals.json
API_SECRET_KEY=d9ddfc40
```

--

- And use those variables in a route to fetch from the API:

```javascript
// same route as above, but using environmental variables for secret credentials
app.get("/dotenv-example", (req, res, next) => {
  // insert the environmental variable into the URL we're requesting
  axios
    .get(`${process.env.API_BASE_URL}?key=${process.env.API_SECRET_KEY}&num=10`)
    .then(apiResponse => res.json(apiResponse.data)) // pass data along directly to client
    .catch(err => next(err)) // pass any errors to express
})
```

---

name: parameters

# Parameters

--

## Concept

Express routes can have parameters.

--

- This means that routes can have variables passed to them by the client.

--

- E.g., a route named `/parameter-example:animalId` contains a parameter named `animalId`.

--

- If a client makes a request for `/parameter-example/22`, that `22` value (or any other value in this spot in the URL) will be put into a variable named `animalId` within the route function.

---

template: parameters

## Example

The following example route accepts an ID into a parameter, makes a request to an API for a record with that ID, and returns the results to the client.

```javascript
// this route is very similar to the dotenv-example route, but using async/await syntax for a change
app.get("/parameter-example/:animalId", async (req, res) => {
  // use axios to make a request to an API to fetch a single animal's data
  // we use a Mock API here, but imagine we passed the animalId to a real API and received back data about that animal
  const apiResponse = await axios
    .get(
      `${process.env.API_BASE_URL}?key=${process.env.API_SECRET_KEY}&num=1&id=${req.params.animalId}`
    )
    .catch(err => next(err)) // pass any errors to express

  // express places parameters into the req.params object
  const responseData = {
    status: "wonderful",
    message: `Imagine we got the data from the API for animal #${req.params.animalId}`,
    animalId: req.params.animalId,
    animal: apiResponse.data,
  }

  // send the data in the response
  res.json(responseData)
})
```

---

name: template-engines

# Template Engines

--

## Concept

Sometimes, it is desireable to respond to incoming requests with content that is formatted in a way that is ready to be displayed by a web browser.

--

- This usually meanse sending back HTML code to the web browser and the web browser then blindly renders this HTML content on the page.

--

- In many cases, you will find that you will want to send the same basic HTML code in response to many different requests, with just a few bits of the content changed each time.

--

- This is where a template engine can help - responding to requests with standardized templates of content where dynamic values are inserted into it as needed.

--

- There are several popular template engines for use with Express - e.g. [Pug](https://pugjs.org/api/getting-started.html), [Mustache](https://www.npmjs.com/package/mustache), and [EJS](https://www.npmjs.com/package/ejs).

---

template: template-engines

## Creating a Pug Template

For example let's install and use the **Pug** template engine.

```bash
npm install pug --save
```

--

- It is now possible to set Express to use Pug as its template engine:

```javascript
app.set("view engine", "pug")
```

--

- To create a template for your site's home page, create a file named `index.pug` with two bits of dynamic content, `title` and `content`:

```yaml
html
head
title= title
body
h1= content
```

---

template: template-engines

## Using a Pug Template

To use a Pug template, simply create a route that instructs Express to respond with the contents of the template by using the `render` function.

--

- For example, to create a route for a site's home page that points to the `index.pug` template we previously made and supplies the values to plug into `title` and `content` fields:

```javascript
app.get("/", function (req, res) {
  res.render("index", {
    title: "My First Templated Site",
    message: "Welcome to your first dynamic templated page!!",
  })
})
```

--

- Simply repeat this process for all the different sorts of routes and templates that your site might need.

--

- The full set of template options are available in the [official Pug language reference](https://pugjs.org/language/attributes.html).

---

template: template-engines

## Single Page Applications

Template engines are less useful for web apps that are set up as **single page applications**.

--

- In a single page application, an initial set of static HTML, CSS, and Javascript code is requested by and loaded into the web browser.

--

- The static browser-based Javascript code then issues new requests to the server as necessary. The server responds to any subsequent requests with JSON data, not HTML documents, e.g.:

```javascript
{
    'title': 'My First Templated Site',
    'message': 'Welcome to your first dynamic templated page!!'
}
```

--

- The static Javascript code initially loaded by the browser when the page was first loaded then updates relevant parts of the page in response to this JSON data.

---

template: template-engines

## Front-Ends Built With React.js

React.js-based front-ends are built as **single page applications**.

--

- An initial set of HTML, CSS, and Javascript code is loaded into the browser.

--

- The browser-based Javascript then makes requests to the server, as necessary.

--

- The server responds with JSON data.

--

- Browser-based Javascript code automatically then updates the components on the page based on this JSON data, as necessary.

--

- Thus, there is no big need for a template engine to help generate repetitious HTML documents.

---

name: authentication

# Authentication

--

## Concept

Many web apps require users to **sign up** and **log in**.

--

- Handling user account creation and authentication can be simple... or complicated.

--

- Fortunately, there's middleware to steamline this!

--

- [passport](http://www.passportjs.org/) is a popular and very flexible authentication middleware solution.

--

- We recommend you wait until you have learned to integrate a database into your project before using it.

---

name: databases

# Database Integration

--

## Concept

Most classic technology stacks that rely on Express.js for the back-end use [MongoDb](https://mongodb.com) as the database.

--

- Most software relies on **relational databases**, such as Oracle, MS SQL, SQLite, MySQL, etc, which store data in a way similar to spreadsheets, with records stored in rows containing columns for each piece of data.

--

- MongoDB is a **document-oriented database** that lends itself well to many common data needs of Javascript-based web and mobile apps, such as native support for geolocation, data stored internally as JSON objects, and easy scalability should your app take off to the moon.

--

- The 3rd-party module named [mongoose](https://mongoosejs.com/) makes it easy to integrate express.js-based apps with MongoDB. Similar modules exist for most other database integrations as well.

--

- We recommend you wait until you have mastered back-end development without a database before adding one into the mix.

---

name: conclusions

# Conclusions

---

# Conclusions

You now have an baseline understanding of what express.js is, how it works, some useful middlewares, and various route patterns.

--

- A [simple Express.js project](https://github.com/nyu-software-engineering/express-js-starter-app) is available for you to fork, clone, and try out for yourself. Remember to run `npm install` to install all dependencies before running it.

--

- Thank you. Bye.
