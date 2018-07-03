# 09-intro-to-backend

## Notes

https://stackshare.io/ is a site that shows you different companies' technology stacks.

### Solutions

All solutions code can be found here: https://github.com/nax3t/webdevbootcamp

And all Cloud9 code can be found here: https://ide.c9.io/learnwithcolt/webdevbootcamp

### Command Line

`rm` and filename removes (deletes) that individual file.

`rm -rf` is known as adding a "flag." `rm` is still the command, and `-rf` is the flag. `rf` stands for "recursive force." It deletes an entire directory and all its contents. (Don't use this in the root directory of your computer or you will wipe everything from your machine.)

### Node

`npm install` installs a package.

`require()` includes a package.

### Express

- A *library* is code that someone else wrote, which we can use in our application. (Examples: jQuery, Bootstrap.) *You* are in control of the code that you call from the library.
- A *framework* is also a library, but is typically much larger and is used differently. The difference is *inversion of control*, meaning that it is the opposite of a library in that *the code calls you* instead of you calling the code. All the control flow is already in the framework, with predefined white spots that you can fill in with your own code. You give up some control and must use the framework the way it is designed to be used. This is not to reduce creativity, it's simply to take care of all the basic setup stuff we would have to do manually for every project. This frees you up to focus on the parts of your app that make it unique.
- A *toolkit* is a collection of libraries that are designed specifically to work together. (As opposed to independent libraries that may or may not work well together.)

Express is a *web development framework*. (As opposed to frameworks that help you make video games or mobile apps.)

It is by far the most popular Node framework. This also equates to it having a large support community.

#### Heavy vs. Light

Refers to how much a framework does for you. A heavyweight framework does a lot for you. A lightweight framework would involve you having to write more of your own code.

#### Unopinionated

Express is also "unopinionated," meaning it is flexible and lets you do things the way you want, rather than forcing you into a rigid structure.

#### Setting Up Express

```
var express = require("express"); /*Imports Express for use in this app*/
var app = express(); /*Now we execute Express and save it to a variable called app*/
```

Then use the method `get` for a get request, which takes two different parameters:

1. The path (could be a URL). In this case, it will be a `/`.
2. The code that you want to run. In this case, it will be a callback function that takes two arguments: request, and response. (Can be called whatever you want to call them.)

```
app.get("/", function(req, res) {
  res.send("Hi, there!");
});
```

`req` and `res` are objects. `req` contains all the information about the request that the user made. `res` will contain all the information that our app is going to respond with.

In Express, you have to write code to specifically tell it to listen for different types of requests. In this case, you also provide it with the port to listen on. (If using Cloud9, you must use `process.env.PORT`, which will return the number of Cloud9's server, which we *have* to use.)

`app.listen(process.env.PORT);`

`env` is a variable, called an "environment variable."

We will also pass in `process.env.IP` for Cloud9:

`app.listen(process.env.PORT, process.inv.IP);`

### Package.json

JSON = JavaScript Object Notation

What it is:
https://docs.nodejitsu.com/articles/getting-started/npm/what-is-the-file-package-json/

Includes a list of dependencies that are needed in order for it to work.

NOTE: Don't upload all the dependencies to GitHub. Just list them in the package.json file. People can download them specifically if they want to run your app. It's like sending a recipe to a friend. You don't package up all the ingredients and send them to them; you just include a list of ingredients required with the recipe, and leave it up to them to get them themselves.

#### --save

When you install packages, adding the `--save` flag at the end means the system will automatically take the package name and version and save it into your package.json file.

#### npm init

Running `npm init` creates a package.json file for you. In your console, cd into the folder where you want your application to exist. Then type `npm init`. It will then walk you through all the steps for creating one.

"Entry Point" refers to the file where your application starts. (Typically `app.js`.)

To leave a field blank (or to leave it at the default value), just hit `Enter` to continue on to the next one.

### Star, or Splat

`*`

If the user types a route into the browser that you do not have any code for (`/bird`, etc.), they will get an error message.

For graceful degradation purposes, you can display your own message instead. You do this by using a `*`, which represents any undefined rotues, as follows:

```
app.get("*", function(req, res) {
  res.send("You are a STAR!");
});
```

IMPORTANT: The `*` has to be the last on your list. Otherwise, it will be the first thing the computer reads, and all user entries (including defined routes) will receive the graceful degradation message. *The first route that matches a given request is the ONLY route that will be run.*

### Route Parameters

These are basically variables. (Also known as "path variables.")

These allow you to write *patterns* of routes users may type in, rather than having to think of every single possible route they might type in.

Example:

Instead of typing this exact route:

`app.get("/r/subredditName")`

You can add a colon:

`app.get("/r/:subredditName")`

This tells the computer you don't actually want to match the text `subredditName`, but any *single* word after where the colon is in your pattern.

However, it will *not* work if the user adds another `/` after the location of the `subredditName`. For example, `/r/subredditName/cats` will go to graceful degradation. Of course, you can get around this by continuing to put `/:` entries in the route.

### Req

When you write:

```
app.get("/r/:subredditName", function(req, res) {

});
```

The `req` will contain all the info about the incoming request. So you can use that in your function, like this:

```
app.get("/r/:subredditName", function(req, res) {
  console.log(req);
});
```

The user's entry will be under `params:`. So a more surgical way to get what you want is:

```
app.get("/r/:subredditName", function(req, res) {
  console.log(req.params);
});
```

### Render

You can pass an entire file into the response by using `render`, which is a method attached to `res`. Like so:

`res.render( "index.html" );`

NOTE: You don't send standard HTML files back using Express, you send dynamic HTML files called "templates."

You can also send EJS files, which stand for "Embedded JavaScript," like so:

`res.render( "index.ejs" );`

These files must be stored in a directory called `views`. (This is the directory name Express is going to look for. But you first have to install `npm install ejs --save`.)

Embedded JavaScript files allow you to "embed" "JavaScript" variables, loops, etc. into HTML. You do this by wrapping it inside the following type of brackets:

`<%= %>`

Whatever goes between those two brackets gets treated like JavaScript. Note that you don't want to clutter your code with tons and tons of JavaScript, so later we'll learn how to handle this.