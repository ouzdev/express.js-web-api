# Web Api sample with Express.Js
[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Project Goals
- [X] Create a basic web app with Express.js
- [X] Manage a request lifecycle with Middleware
- [ ] Json Web Token (JWT) usage with Express.js



## Create a basic web app with Express
* Create a file app.js
* Go to terminal, and enter 'npm init -y'. This command creates a default package.json file for your node.Js project.
* In the terminal, enter 'npm install express'. This command installs the Express Framework.
* Open the package.json. In the dependencies section, there is an express entry. This entry means that Express Framework is isntalled.

## Create a web app that return JSON data
Add the following code to app.js
```
app.get("/products",(req,res) => {

    const products = [
    {
        id:1,
        name:"Product 1"
    },
    {
        id:2,
        name:"Product 2"
    }
    ];
    res.json(products);
})
```
Make sure the app.json that files look like this

```
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => res.send('Hello World!'));
app.get("/products",(req,res) => {

    const products = [
    {
        id:1,
        name:"Product 1"
    },
    {
        id:2,
        name:"Product 2"
    }
    ];
    res.json(products);
});
app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```
## Manage a request lifecycle with middleware

The Express Framework has built-in support for handling a request in this way.

Add the following code to app.js

```
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => res.send('Hello World!'))

app.get('/users',(req,res) => {
  res.json([{
    id: 1,
    name: 'User Userson'
  }])
})

app.get('/products', (req, res) => {
  res.json([{
    id: 1,
    name: 'The Bluest Eye'
  }])
})

app.listen(port, () => console.log(`Example app listening on port ${port}!`))
```
Create a new file is client.js. Add the following code to client.js
```
const http = require('http');

http.get({
  port: 3000,
  hostname: 'localhost',
  path: '/users',
  headers: {}
}, (res) => {
  console.log("connected");
  res.on("data", (chunk) => {
    console.log("chunk", "" + chunk);
  });
  res.on("end", () => {
    console.log("No more data");
  });
  res.on("close", () => {
    console.log("Closing connection");
  });
});
```

Run app.js with ``` node app.js ``` command in terminal.

After that command that run command.

Run client.js``` node client.js ``` command in terminal.


The terminal should look like this.

For app.js

```
Example app listening on port 3000!
```
For client.js
```
connected
chunk [{"id":1,"name":"User Userson"}]
No more data
Closing connection
```
That from step later open app.js. After the row ```const app = express()```. Add the following code.

```
function isAuthorized(req,res, next) {
    const auth = req.headers.authorization;
    if (auth === 'secretPassword') {
      next();
    } else {
      res.status(401);
      res.send('Not permitted');
    }
  }
```
Locate that part of the code.
```
app.get('/users', (req,res) => {
  res.json([{
    id: 1,
    name: 'User Userson'
  }])
})
```
Replace part of the code
```
app.get('/users',isAuthorized, (req,res) => {
  res.json([{
    id: 1,
    name: 'User Userson'
  }])
})
```
