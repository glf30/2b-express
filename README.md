# Lesson 2B: Basics of Express

---

## What this lesson covers:
- What is the Express module
- What is a Status Code
- What is an API
---

## Introduction

We are going to be working with our next module, Express.  As we did with our last project, we are going to initialize our project and install the proper dependency.

0. A) In terminal, initialize the project

```
npm init -y
```
0. B) In terminal, install the express module

```
npm install express
```

0. C) Global Nodemon Installation

Nodemon is a tool that allows us to run our node.js projects without having to restart them upon making code changes.  If we install this globally into our machines, we'll gain the `nodemon` command

```
npm install -g nodemon
```

## What is the Express Module

Express is the most popular Node web framework, and is the underlying library for a number of other popular Node web frameworks. It provides mechanisms to:

- Write handlers for requests with different HTTP verbs at different URL paths (routes)
- Integrate with "view" rendering engines in order to generate responses by inserting data into templates.
- Set common web application settings like the port to use for connecting, and the location of templates that are used for rendering the response.
- Add additional request-processing "middleware" at any point within the request handling pipeline

It's time to begin building out our first server file!

Import the Express module, and prepare a variable that immediately invokes the Express function:

1. Import the express module, and prepare a ready-to-use variable for it

```js
const express = require("express"); // Import the module
const app = express(); // Ready-to-use variable
```

Let's set up the port on our local machine that we want to use:

2. Set the Port we want to use

```js
const PORT = 3000; // 3000 and 8080 are commonly used ports for development
```

Now it's time to make sure the server can start up, and listen to requests:

3. Set the application to begin listening / begin spinning the server

```js
app.listen(PORT, () => {
  console.log(`server is listening on port ${PORT}`);
});
```

Now run `node index.js` in your terminal to find out if your server is working so far. You should see "server is listening on port 3000" in your terminal, which means the server can actively listen to requests! Press `ctrl + c` to stop the server.

Next, we will be setting up how to respond to requests at `localhost:3000/` and similar URLs, starting with the base URL:

4. Set up a response to localhost:3000/

```js
app.get("/", (req, res) => {
  console.log("user hit the resource");
  res.status(200).send("Home Page"); // send the client the text "Home Page" with a success status
});
```

Every time we set up a new response:

- Use the command `node index.js` in the terminal to run the server.
- Use your browser to test the response.
- Shut the server down using `ctrl + c`

If we go to `localhost:3000/` in the browser, you'll see "user hit the resource" in your terminal. That tells us that someone made a request! You should also see the words "Home Page" in your browser. If you notice, we're also setting a `status(200)` to the response.

## What is a status code

A status code is a message a website's server sends to the browser to indicate whether or not that request can be fulfilled. Here is a list of status codes, with their meanings:

- `200` - successful request
- `304` - repeated successful request with no changes (ie. refreshed the page)
- `404` - requested resource cannot be found
- `401` - authentication error, attempt to access a protected resource
- `500` - generic error, when no other error is suitable

Next, we will set up a response to `localhost:3000/about` to make sure we can access more than one page:

5. Set up a response to localhost:3000/about

```js
app.get("/about", (req, res) => {
  res.status(200).send("About Page"); // send the client the text "About Page" with a success status
});
```

Finally, it's time to set up for ALL OTHER URL extensions, and return a `404` status code, because there are no other resources to access:

6. Set up a response to localhost:3000/\*

```js
// /{*any} means all, any page that isn't listed so far. So if you reach localhost:3000/* this should be the response
app.all("/{*any}", (req, res) => {
  res.status(404).send("<h1>page not found</h1>"); // send the client "page not found" with a not found status
});
```

An asterisk `*` is commonly used to represent "everything" when it comes to setting up responses to URLs. Make sure to try and visit various URL extensions once the server is up and running.

## What is an API

API is an acronym that stands for "Application Programming Interface", which is a way for two or more computer programs to communicate with each other. A server can host an API. When you create a server that responds to various requests with different forms of data, this is called an API! (This can mean serving HTML vs serving JSON, or it can mean serving all text but the contents of each text is different).

By completing this lesson, you have created an API.
