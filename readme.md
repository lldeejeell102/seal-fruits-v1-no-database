# Intro to the Backend

Web works via browsers and servers.

- Users type in urls, click on links, submit forms
- The browsers sends a request
- a server receives the request and responds
- may response with html, files, json, etc.

Servers can be written in javascript with a javascript run time, and there are three of them:

- node
- deno
- bun

node is the most popular cause it's been around the longest.

## Backend frameworks

Framework: A system of libraries, practices and conventions that'll make building a particular type of application easier.

Write servers in node from scratch can be tricky and there are several frameworks created in the node ecosystem.

minimalist (basic routing functionality)
- express (most popular)
- koa
- fastify

battery included frameworks
- NestJS
- FoalTS
- Sails

## Setting up an express project

- open a terminal to an empty folder

- confirm you have node `node --version`

- create some files `touch server.js .gitignore .env`

- list the things we want git ignored

```
.env
/node_modules
```

- create a new node project (package.json) create it by running `npm init -y`
    npm: node package manager
    init: to initiatlize a new package.json
    -y: accept all default values

- If not already installed, install nodemon globally (`npm install -g nodemon`)
    - nodemon is a tool that will turn on file watchers when you run a program, if you update a file, it'll restart

- update the scripts in your package.json

```json
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js",
    "dev2": "node --watch server.js"
  },
```

_Note: the --watch flag is for new versions of node_

## Writing basic express server

```js
//*************************** */
// DEPENDENCIES
// Brings things from libraries and other files
//*************************** */
// require('thing'): it will return the exported value of the library or file we specify

//import the express library
const express = require("express")


//*************************** */
// Create Express Application Object
// This is the center of our express universe
//**************************** */
// express(): returns an express application object

const app = express()


//**************************** */
// MIDDLEWARE
// Special Utilities that run before our routes
//****************************+ */


//*****************************
// ROUTES
// Which function should run for differnt (method/url) pairs
// ****************************
// methods: GET, POST, PUT, DELETE
// url: anything after the domain so xyz.com/cheese -> url: /cheese

// a GET request to the ROOT url or "/" xyz.com/ => "/"
// app.get(url, function)
// function: (request, response) => {}
// req (request): an object with details about the request
// res (response): an object with functions to send the response
app.get("/", (req, res) => {
    // res.send(something) will send the response based on the input
    // an html string: will send back as html
    // js array or object: will send back json
    // string: sends back as text
    res.send("<h1>Hello World</h1>")
})



// *****************************
// TURNING ON SERVER LISTENER
// WILL TELL OUR APP TO LISTEN FOR REQUESTS
// ON A CERTAIN PORT
// *****************************
// app.listen(PORT, FUNCTION)
// The function will run after the server turns on
app.listen(3000, () => {console.log("server is listening on port 3000")})
```

boiled down

```js

const express = require("express")


const app = express()


app.get("/", (req, res) => {
    res.send("<h1>Hello World</h1>")
})


app.listen(3000, () => {console.log("server is listening on port 3000")})
```

## properties of req

- `req.query`: object with query params `?key=value&key=value`
- `req.params`: object with url params `/url/:param`
- `req.url`: url of the request
- `req.method`: method of the request
- `req.headers`: object of request headers
- `req.body`: object with request body data

## properties of res

- `res.send()` sends a response as html, json or text depends on what is passed

- `res.render()` will render a view in a "views" folder using a templating library matching the file extension (.ejs). Can send data as a second argument to be used when rendering the view.

- `res.json()` will respond with json

### Tips

- Thunderclient and curl can used to test routes without an internet browser

- If you need to kill a process on a certain port

```
kill $(lsof -t -i :xxxx)
```
*replace xxxx with the port number