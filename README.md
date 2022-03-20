# Web Api sample with Express.Js
[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Project Goals
- [X] Create a basic web app with Express.js
- [ ] Manage a request lifecycle with Middleware
- [ ] Json Web Token (JWT) usage with Express.js



## Create a basic web app with Express
* Create a file app.js
* Go to terminal, and enter 'npm init -y'. This command creates a default package.json file for your node.Js project.
* In the terminal, enter 'npm install express'. This command installs the Express Framework.
* Open the package.sjon. In the dependencies section, there is an express entry. This entry means that Express Framework is isntalled.

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

