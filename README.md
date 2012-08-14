requiredir
==========

Require all JavaScript files in a directory.  Supports recursive loading and argument passing to loaded files.

## How to use

requiredir is a function that takes three arguments: path to the folder, recursive search, and an optional array of arguments to supply to each file that is required.  Note that
the arguments will be supplied only if the module that the file exposes is a function.
```js
var requiredir = require('requiredir'),
	models = requiredir('models'),
	controllers = requiredir('controllers', true);
```

Assuming you have a directory structure of the form:

```js
- controllers
--- home
----- homeController.js
--- admin
----- adminController.js
----- adminOtherController.js
--- appController.js
```

Then the resulting output would be:

```js
controllers = {
	home: { homeController: [Function] },
	admin: { adminController: [Function], adminOtherController: [Function] },
	appController: [Function]
};
```

## Supplying arguments

You may occasionally want to supply arguments to the files you are including in a directory.  Assume you are using express, and have a directory of routing files that each need a reference to the express app.

```js
// in routes/HomeRoutes.js

module.exports = function (app) {
	app.get('/', ...);
};
```

Using requiredir, you can do the following:

```js
var express = require('express'),
	app = express.createServer(...),
	routes = requiredir('routes', true, [app]);
```
