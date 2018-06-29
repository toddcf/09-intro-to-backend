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