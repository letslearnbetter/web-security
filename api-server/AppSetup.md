# App Setup
In this part we will walk through getting the setup up and running

## Scaffolding the project

* Create a new project directory and cd into it.
* `npm init -y` to initialize a new npm project by creating a `package.json` file
* Install the required dependencies `npm install --save express mongoose morgan body-parser`
  * `mongoose` : Interface with mongoDB
  * `morgan` : Application logging framework
  *  `body-parser`: parse the incoming requests as JSON
* create a file `index.js` in the projec root.
* create a file `.gitignore` and add `node_modules` to it.
* Run with `node index.js`

## Import the required modules

Add the following import statements to `index.js`

```javascript
const express = require('express');
const http = require('http');
const bodyParser = require('body-parser');
const morgan = require('morgan);
```
## Server configuration

Next we create a server, assign a port and start listening for request on that port:

```javascript
const port = process.env.PORT || 3090;
const server = http.createServer(app);
server.listen(port);
console.log('Server listening on:', port);
```

**NOTE:** `process.env.PORT` is an environemnt varibale. It can be set by running `set PORT=<port_number>` or `PORT=<port_number>` in Windows and Mac respectively

### Register middlewares

```javascript
app.use(morgan('combined'));
app.use(bodyParser.json({ type: '*/*' }));
```
## Nodemon

Nodemon gets rid of the trouble of manually restarting our app everytime we make a change.

`npm install --save-dev nodemon`

**NOTE:** `--save-dev` is used to create a dev dependency which means that it will only be used in a development environment.

Add the following to the scripts section in `package.json`

`"dev": "nodemon index.js"`

## Next up

[Route handling with express](Part2.md).