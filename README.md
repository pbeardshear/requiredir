requiredir
==========

Require all JavaScript files in a directory.  Supports recursive loading and argument passing to loaded files.

## How to use

requiredir is a function that takes three arguments: path to the folder, recursive search, and an optional array of arguments to supply to each file that is required.  Note that
the arguments will be supplied only if the module that the file exposes is a function (module.exports = function () { ... }).
```js

```

```js
var requiredir = require('requiredir'),
	models = requiredir('models'),
	controllers = requiredir('controllers', true);
```

Assuming you have a directory structure of the form:

```js
- Controllers
-- home
--- homeController.js
-- admin
--- adminController.js
--- adminOtherController.js
-- appController.js
```

Then the resulting output would be:

```js
controllers = {
	home: { homeController: [Function] },
	admin: { adminController: [Function], adminOtherController: [Function] },
	appController: [Function]
};
```
