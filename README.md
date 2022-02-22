# Intro to Express

<img src="https://i.imgur.com/HMLwV1V.png" />

## Lesson Objectives

1. Describe what is a `back end`
1. Install `Node packages`
1. Set up a basic `Express` server
1. Set up a basic `GET route`
1. Use `nodemon` to restart your sever when your code changes

## Framing

So far, you've been working on the `front end`, you've been building things with HTML, CSS and JavaScript that appear in a browser.

Now we'll start learning about the `back end` and how that is tied to the `front end`.

<img src="https://i.imgur.com/7HqKH1x.png" />

In this unit, we'll be building our own web applications with `Node.js` and the `Express` web server, along with `Mongo` as our database and `Mongoose` as the NPM package to interface with `Mongo`.


A backend typically consists of the following:

- a server (takes client requests and sends responses) 
- an application (the logic of what to do with the request - get flight information/get directions to somewhere/ etc.)
- a database (store, retrieve, update information/data etc.) 

Let's take a moment to think about `Amazon`, Amazon has 300 million products and counting. Each item has its own web page.

Amazon does not have thousands of web developers carefully handcrafting each web page for each item by hand and updating them as needed. Rather, the pages are built dynamically. The developers build an HTML template and then work with the data of the products to create individualized web pages based on the data. 

Things like price, images of the item, description of the item etc. are stored in a database, this data is retrieved and interpolated with the HTML. This requires the use of a server and a database.

## Install Node packages

Node.js is an application that lets us run JavaScript outside of the browser and in the terminal. We'll use node.js to build simple servers that will respond to browser requests.

Built into Node.js is something called `npm`, which stands for `Node Package Manager`, which will manage Node Packages and if you have worked with React then you should already be familiar with `npm`. 

Node packages are libraries (or frameworks - see below) of code that provide useful functionality. These packages are published at [www.npmjs.com](https://www.npmjs.com/)


These chunks of code fall into one of two categories:

- Libraries
    - A collection of functions, objects, and even other libraries that you call
    - It has no idea what you're going to build
- Frameworks
    - Is essentially just a library
    - Is also a pre-conceived skeleton for an application
    - It knows what you're going to build and is somewhat opinionated about how you should do it

We'll be working with one package throughout this unit called `express` - which calls itself a framework AND unopinionated  `¯\_(ツ)_/¯`

<hr>

**A bit of review**

**❓ - What is the difference between a library and a framework and when would you choose one over the other?**

<hr>

### Setting Up Our Server

Let's first get things setup.

- cd into `student_examples`
- `mkdir first_server`
- `cd first_server`


First we have to initialize our directory with a `package.json` file. We can create it interactively by typing the following into the terminal.

```sh
npm init
```

We'll get a few prompts for the following:

- the name of our project
- the version
- what our main file is
- ...several more prompts...

To keep the defaults, you can just keep pressing enter on each of these prompts. 

Here is a very minimal `package.json` - it's just a text file with an object written in strict JSON format. 


<img src="https://i.imgur.com/oX88ZQB.png" width=400/>


### Package.json

It's totally ok to edit this file - for example, if I forgot to put myself as the author I could add it as a string. If I didn't like my project name, I could update it too. 

**GOTCHA** be careful to write any additions to the file using proper JSON format or else you will get errors and your code will not run.


<hr>

**❓ - What 2 rules can you think of that define the JSON format?**

<hr>



#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min 

The instructor will demo making a few edits that don't follow the rules of JSON so we can see the error(s) that will be produced. 

<hr>

Let's take a moment and delete both `.json` files.  Now we will run `npm init` again but this time with the following flag:

```sh
npm init -y
```

Running it this way automatically creates the file and accepts all the default values. 

### NodeJS Frameworks 

Express will be our choice for a NodeJS Framework in this unit.  However there are several other popular frameworks out there.  

Let's a take a look at the following articles on the top node frameworks in 2020. 

- [Top 3 Most Popular Frameworks And When To Use Them](https://rapidapi.com/blog/best-nodejs-frameworks/)
- [Top 20 Best NodeJS Frameworks For Devs in 2020](https://www.ubuntupit.com/best-nodejs-frameworks-for-developers/)


### Installing Express

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min 

So let's take a look at the [Express NPM Package](https://www.npmjs.com/package/express) before we install it. 

<hr>

Let's install the `express` npm package :

```
npm i express
```

We can see that we've successfully added because or `package.json` file will have updated (under dependencies)

<img src="https://i.imgur.com/jHWP7bd.png" width=400/>


Additionally, we see that we now have a directory called `node_modules` and a file called `package-lock.json`

![files](https://i.imgur.com/sS4uziE.png)
<img src="" />

We're not going to edit our `package-lock.json` file, it's just a helper file for npm that helps npm do some under the hood stuff.

Inside `node_modules` is all the code that was downloaded so we could use `express`, the code is tucked into folders that are managed by npm. Like `jQuery` or `React`, we don't ever have to look at the source code or modify it in any way, it can just sit there and we'll bring in the code and use it in our own files.  

<hr>

**❓ - What does the node_modules folder contain?**

**❓ - If the folder isn't there how do you go about creating it?**
<hr>

## Set up a basic Express server

In the root of our project, `touch server.js`


<img src="https://i.imgur.com/FlNsHyM.png" />

In `React` we had used the ES6 keyword `import` to import the following:

```js
// 3rd party packages
import React from 'react'
// Components 
import Form from './Form'
// Data
import itemsArr from './data.js'
```

However in node we use the ES5 keyword **require()** to import modules. 

Now that the `Express` library has been installed, we can use it in our code, by using `require()`.

```javascript
const express = require('express');
```

Let's take a minute and add a console log to see what is stored in the `express` variable

```js
console.log('express', express)
```

### Executing The File

In order to see the console log we must run the file at least once. 

```js
node server.js
```

We can see it's a giant object with a ton of properties and functions. 
<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min 

Express has much to offer so it's worth sometime to checkout their docs. 


[Full express documentation](http://expressjs.com/en/api.html)

We will focus on the `Getting Started` section.

<hr>

### Building An Express Server

Let's build out a basic bare bones simple server.

```js
// IMPORT EXPRESS
const express = require('express');
// CREATE A NEW INSTANCE OF EXPRESS
const app = express();
// SET THE DEFAULT PORT NUMBER THE WEB SERVER WILL LISTEN IN ON
const PORT = 3000;
// ACTIVATE THE SERVER TO LISTEN ON THE PORT
app.listen(PORT, () => {
  console.log(`Express server listening on port ${PORT}`);
});
```

<!-- <details><summary>Answer</summary>
<img src="https://i.imgur.com/qlTWMWB.png" />
</details> -->


Start the app by executing `node server.js` in the command line. It'll now run continuously because of the functionality of the `app.listen`

Therefore, it will start and then you won't get your bash prompt back, it'll just hang

Visit http://localhost:3000/ in your browser.  You should see your 'Hello world' text. You've successfully created a basic web server!  This will serve dynamic pages to web browsers.

### Shut down your server

You can't run two servers on the same port and you can get annoying errors if you don't shut your servers down properly. Get in the habit of `control c` to shut your server down when you are done working.

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min 

The instructor will demo terminating the node process via:

-  `Activity Monitor`
- terminal
  - find all running node processes:  `ps -ef | grep node`
  - kill a single node processes: `kill -9 "process id number"`

<hr>

### Hot Reloading Express

An NPM package called `nodemon` allows us to run code just like `node`, but will restart the application whenever code in the application's directory is changed.

This is really handy and gives us a better workflow, much like when working with `React`. 

Let's first take a look at the [nodemon npm](https://www.npmjs.com/package/nodemon)  package and then install it. 

```js
npm i nodemon -g
// -g installs the package globally 

// depending on permissions you may need to use sudo
sudo npm i nodemon -g
``` 


Now we can call `nodemon server.js`, and the server will restart whenever the app's code changes

### Adding A New Script To Package.json
We can also modify the `scripts` section in the `package.json` file to add a new `start` script:

```sh
"scripts": {
  "start": "nodemon server.js"
}
```

If you want to get really fancy, you can go to your `package.json` file then change the value of `main` from `index.js` to `server.js`

```sh
"main": "server.js",
```

Now you can just type  `nodemon` in terminal and it will 'know' you mean to run `server.js`

```sh
nodemon
```

## Adding API Endpoints

The backend web servers we will be building in this unit will be configured as API servers.  

This means they will be configured with `API Endpoint` that will return data based on the `route` used to connect with the server. 

### Our First Route

Let's add our first route.  This will be a GET route which gets data.  Additional verbs we will work with are: `POST`, `PUT` and `DELETE`.  


| **URL** | **HTTP Verb** | 
|------------|-------------|
| /         | GET       |   

Here is how we add the route. Here we are setting a `GET` route that responds to the  `/` route, which is the default route for the server.  That means if a user goes to `localhost:3000/` this is the method that will get triggered.

```js
app.get('/', (req, res)=>{
  res.send('Hello world');
});
```

The function (callback) takes two parameters

- `request`
    - object containing information about the request made (browser, ip, query params, etc)
- `response`
    - object containing methods for sending information back to the user (client)

Both are position dependent as are all function parameters. Inside our callback we can write whatever code we want.

In this case we are using a method on the response object (`res.send()`) - that is saying `send this plain text as the response`


We can build as many routes as we like and customize them to do whatever we want.

<!-- ### Synopsis Of What We Have Done Thus Far

![](https://i.imgur.com/eIN0lrM.png) -->

### Examine the req & res Objects

Let's add a console log and examine whats inside the `req` object. 

```js
app.get('/', (req, res)=>{
  console.log('get - req', req)
  res.send('Hello world');
});
```

And now let's see what's inside the `res` object.
```js
app.get('/', (req, res)=>{
  console.log('get - res', res)
  res.send('Hello world');
});
```

<hr>

**❓ - What does `req` and `res` shorthand represent?**

<hr>

### Adding A Second Route

Let's first update our routing table so we keep track of what routes and associated HTTP verbs our server is responsible for. 

| **URL** | **HTTP Verb** | 
|------------|-------------|
| /         | GET       |  
| /somedata         | GET       |    


And now add the route.
```js
app.get('/somedata', (req, res)=>{
  response.send('here is your information');
});
```

We can even wrap the content in HTML. 

```js
app.get('/somedata', (req, res)=>{
  response.send('<h3>here is your information</h3>');
});
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 10min 

In the Express server in server.js define the following routes:

| **URL** | **HTTP Verb** | Action |
|------------|-------------|-------------|
| /         | GET       |  send "Welcome to my webpage" 
| /somedata         | GET       | send 'Here is your information'  |
| /name        | GET       | send "Your name is..."  |
| /fav-foods         | GET       | send "Your favorite foods are..."  |
| /fav-books        | GET       | send "Your favorite books are..."  |


**BONUS**

Examine the [Express Response](http://expressjs.com/en/4x/api.html#res) documentation and determine how to send `name`, `fav-foods` and `fav-books` as a single json object. You should create a new route for is called `/alldata`.

<details><summary>Solution</summary>

```js
app.get('/alldata', (req, res) => {
    res.json({
        name: "Hannah",
        food: "Food",
        book: "Book"
    })
})
```

</details>


<hr>

## Adding .gitignore File

When we downloaded express it installed a lot of code (inside `node_modules`) - we don't need to track these files and upload/download them to and from github. All the info needed is in the `package.json`

To avoid tracking/uploading/downloading files that don't need to be tracked or shouldn't be tracked (passwords, secrets) you can create a file called `.gitignore`

Add the following line:

```sh
node_modules
```

Here is a collection of `.gitignore` files to reference depending on what your building. Let's do a quick search for node and see what else we might consider adding. 

- [A Collection of useful .gitnore](https://github.com/github/gitignore)


### Resources

- [require-vs-es6-import](http://researchhubs.com/post/computing/javascript/nodejs-require-vs-es6-import-export.html)
- [Top 3 Most Popular Frameworks And When To Use Them](https://rapidapi.com/blog/best-nodejs-frameworks/)
- [Top 20 Best NodeJS Frameworks For Devs in 2020](https://www.ubuntupit.com/best-nodejs-frameworks-for-developers/)
- [Full express documentation](http://expressjs.com/en/api.html)
- [Express NPM Package](https://www.npmjs.com/package/express) 
- [A Collection of useful .gitnore](https://github.com/github/gitignore)
