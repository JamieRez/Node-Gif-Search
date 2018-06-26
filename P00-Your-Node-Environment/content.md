---
title: "Setting up your NodeJS environment"
slug: your-node-environment
---

NodeJS or node.js or just node is a web server built with JavaScript. But... JavaScript is for the client!? What's going on!?

JavaScript only ran in the browser until Google invented the V8 Engine and Ryan Dahl used the V8 Engine to create a JavaScript based server in 2009.

Now Node is a fast growing and popular web server. And now you get to learn how to use it to build a simple gif search engine using the Giphy API.

If you haven't been to [Giphy](https://giphy.com) before, head over to their website now to see how it works.

# Setting Up Your Node Environment with Package Managers

We're going to use NodeJS as our **web server** for this project. We could write just plain JavaScript to use NodeJS, but that would mean writing a lot of **boilerplate**. Instead, we will use the **web framework** ExpressJS, which uses NodeJS.

**Package managers** are pieces of software that manage the versions of various libraries so they can work together without errors on your computer. We'll use [Homebrew](https://brew.sh/), the MacOS **package manager**, to install [NodeJS](https://nodejs.org/en/). When we install NodeJS, the Node Package Manager (npm) will be installed as well, so we can then install node packages (like ExpressJS!).

Open your computer's terminal and then...

If you don't already have Homebrew installed, install that first and then NodeJS & npm.


#### Mac Instructions:

```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
$ brew install node
```

> [info]
> Whenever you see the `$` in a command, that means it should be called in your computer's terminal. Remember: Don't include the `$` in your command.`

#### Windows Instructions

Choose the proper installer at the [Node.js download](https://nodejs.org/en/download/) page.

Now open your Command Prompt program and type `npm -v` to check if npm is installed. This should print out a version number, e.g. `4.10.0`.

# Starting a Node Project

> [info]
> If you do not already have a text editor, download and install the [Atom Text Editor](https://atom.io/).


Use npm to initialize a Node project from the commandline.

```bash
$ mkdir gif-search
$ cd gif-search
$ npm init
# (hit enter for each option it asks for to select the default choice)
$ atom . # to open your project in the Atom text editor
```

Now that you initialized your node project with `npm init`, you will see that you have a `package.json` file in your folder.

# Add Express Package and Start Node

Now we need to add ExpressJS to this project. We will use npm to install ExpressJS and npm will add a line to our `package.json` file to track the libraries that our project uses. It will also add ExpressJS and its dependences to a `node_modules` folder inside our project. You won't ever need to touch any of the files inside the `node_modules` folder during this tutorial.

Install ExpressJS to your project

```
$ npm install express --save
```

# Adding `app.js`

Add a file named `app.js` to your project. This is a more conventional name for the root file of an ExpressJS project.

Mac:

```
$ touch app.js
```

Windows:

```
> app.js
```

Now add this code that add express to the file, then uses it to start a web server.

```js
const express = require('express');
const app = express();

app.listen(3000, () => {
  console.log('Gif Search listening on port localhost:3000!');
});
```

Finally, open up your `package.json` file and set your `main` file to "app.js"

```json
{
  ...
  "main": "app.js",
  ...
}
```

Once this is in place, run your server from your terminal with this command:

```bash
$ node app.js
```

You should see "Gif Search listening on port 3000!" output in your terminal. And if you enter `localhost:3000` into your browser's address bar, you should see `Cannot GET /`. This is because we haven't defined a **root route**, a route for the path: `/`.

> [info]
> Using the `$ node` method to start your server is kinda annoying because you'll have to stop and restart your server every time you make a change. Instead let's start our node server with a program called `nodemon`.
> Install `nodemon` by typing this into your terminal `$ npm install nodemon -g`. Now begin your server by typing `$ nodemon`. Now your server will restart anytime you make any changes to your code.

# Your First Route in an Express Project

Now that we have Node and npm installed we're going to start an Express project and make it say "hello world".

Web servers are built to receive requests to various predefined **URL endpoints** or **routes**. These routes or endpoints are defined as unique **URL paths**. Let's look at some examples of a path. To get to your public facebook profile, you must go to facebook.com + your facebook user name:

`https://www.facebook.com/YOUR_USER_NAME`

In express this would be defined like this:

```js
app.get('/:username', (req, res) => {
  // Here you would look up the user from the database
  // Then render the template to display the users's info
})
```

This is an example of an endpoint or route. It is called a **GET** route because we are "getting" information to read, not saving or changing information in the database. Hence, the function name we call is `app.get()`. Remember that `app()` is an instance of Express, and that means that the `get()` function is a native Express function (not middleware that we added).

Using the code below as a model, create a route that goes to 'hello-squirrel' that prints 'Hello Squirrel' in the web browser.

```js
// app.js
const express = require('express');
const app = express();

app.get('/hello-world', (req, res) => {
  res.send('Hello World');
});

app.listen(3000, () => {
  console.log('Example app listening on port 3000!');
});
```

For reference you can look at [ExpressJS's Getting Started](https://expressjs.com/en/starter/installing.html) docs
