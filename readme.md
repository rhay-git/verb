# verb [![NPM version](https://img.shields.io/npm/v/verb.svg)](https://www.npmjs.com/package/verb) [![Build Status](https://img.shields.io/travis/jonschlinkert/verb.svg)](https://travis-ci.org/jonschlinkert/verb)

> Documentation generator

## Install
Install with [npm](https://www.npmjs.com/)

```sh
$ npm i verb --save
```

## Usage

<!-- toc -->


**TODO**

- [x] publish a fast, composable, highly extendable project app with a user-friendly and expressive API
- [x] support sub-apps (to any level of nesting)
- [x] support streams, tasks, and plugins compatible with both [gulp][] and [assemble][assemble-core]
- [x] make it super easy to run specific tasks from any app or sub-app, programmatically or via CLI 
- [x] support _instance plugins_ that allow you to easily add functionality and features to verb
- [x] support any template engine
- [x] support using any number of template engines at once, so that different file types can simultaneously be handled by the engine that was registered for that file type
- [x] support templates as [vinyl][] files, simple to use template collections and lists (for pagination, sorting, groups etc)
- [x] support middleware that can be run on all files or specific files, and at specific points during the _build process_ (like `onLoad`, `preRender`, `postRender`, etc) 
- [x] 820+ unit tests
- [ ] create and publish apps (we created a handful of apps that we've been using locally, these will be published shortly)
- [ ] CLI docs (started)
- [ ] User help (e.g. when the user does `verb help` or just `verb`)
- [ ] API docs
- [ ] App guidelines and conventions

## Install
To get started, you'll first need to install `verb` globally using [npm][], along with any apps you'd like to run.

**Install verb**
Install globally with [npm](https://www.npmjs.com/)

```sh
$ npm i -g verb
```

**Install a "verb app"**

If you aren't familiar with verb, just take the `node` app for a test drive:

```sh
$ npm i -g verb-node
```

**Run a "verb app"**

If everything installed correctly, you should now be able to verb a new project with the following command (make sure you run the command from an empty directory!):

```sh
$ verb node
```

***

## Usage

```sh
$ verb <command> [args]
```

## CLI

_(WIP)_

### help

_(TODO)_

Get started with Verb. 

```js
$ verb help
```

### init

_(TODO)_

Get started with Verb. 

```js
$ verb init
```

Upon running `init`, verb will prompt you for answers to the following questions:


### Run apps

```sh
$ verb <app name> [options]
```

**Example**

Run app `abc`

```sh
$ verb abc
```

### Run tasks

To run a task on the `base` app, just pass the name of the task to run.

```sh
$ verb <task name> [options]
```

Unless overridden by the user, the `base` app is the default app that ships with Verb. This app doesn't really "verb" anything, but it will prompt you for a few answers (if you choose), to store data that's commonly needed by templates, like `author.name`, GitHub `username`, etc. 

**Example**

Run task `bar`:

```sh
$ verb bar
```

### Run sub-apps

> Sub-apps are normal apps that are called from (or registered by) other apps.

Dot-notation is used for getting and runing sub-apps. 

```sh
$ verb <app name>.<sub-app name> [options]
```

**Examples**

Run sub-app `b` on app `a`:

```sh
$ verb a.b [options]
```

Run sub-app `c`:

```sh
$ verb a.b.c [options]
```

And so on...


### Run a app's tasks

```sh
$ verb <app name>:<task name> [options]
```

**Example**

Run task `bar` on app `foo`.

```sh
$ verb foo:bar 
```

### Run a sub-app's tasks

```sh
$ verb <app name>.<sub-app name>:<task name> [options]
```

**Example**

Run task `foo` on sub.app `a.b.c`.

```sh
$ verb a.b.c:foo 
```

## API


### .getConfig

Static method that first tries to get the `verbfile.js` in the root of the current project, then if not found, falls back to the default `verbfile.js` in this project. 

Once resolved, the verbfile will be loaded and used to create the "base" instance of verb. All other instances will be stored on the base instance's `apps` object.

**Params**

* `filename` **{String}**: Then name of the config file to lookup.
* `returns` **{Object}**: Returns the "base" instance.

**Example**

```js
var verb = Verb.getConfig('verbfile.js');
```

### .getTask

Get task `name` from the `verb.tasks` object.

**Params**

* `name` **{String}**
* `returns` **{Object}**

**Example**

```js
verb.getTask('abc');

// get a task from app `foo`
verb.getTask('foo:abc');

// get a task from sub-app `foo.bar`
verb.getTask('foo.bar:abc');
```

### .addApp

Alias for `register`. Adds a `app` with the given `name` to the `verb.apps` object.

**Params**

* `name` **{String}**: The name of the config object to register
* `config` **{Object|Function}**: The config object or function

**Example**

```js
base.addApp('foo', function(app, base, env) {
  // `app` is a `Verb` instance created for the app
  // `base` is a "shared" instance that provides access to all loaded apps
  // `env` is a configuration/environment object with details about the app,
  // user cwd, etc
});
```

### .hasApp

Return true if app `name` is registered. Dot-notation may be used to check for [sub-apps](#sub-apps).

**Params**

* `name` **{String}**
* `returns` **{Boolean}**

**Example**

```js
base.hasApp('foo.bar.baz');
```

### .getApp

Return app `name` is registered. Dot-notation may be used to get [sub-apps](#sub-apps).

**Params**

* `name` **{String}**
* `returns` **{Boolean}**

**Example**

```js
base.getApp('foo');
// or
base.getApp('foo.bar.baz');
```

### .extendApp

Extend an app.

**Params**

* `app` **{Object}**
* `returns` **{Object}**: Returns the instance for chaining.

**Example**

```js
var foo = base.getApp('foo');
foo.extendApp(app);
```

### .invoke

Invoke app `fn` with the given `base` instance.

**Params**

* `fn` **{Function}**: The app function.
* `app` **{Object}**: The "base" instance to use with the app.
* `returns` **{Object}**

**Example**

```js
verb.invoke(app.fn, app);
```

## Authoring apps

_(TODO)_

### App naming conventions

Use `verb-` as the prefix, followed by any words of your choosing to describe the purpose of the app.



## Related projects
* [assemble-core](https://www.npmjs.com/package/assemble-core): The core assemble application with no presets or defaults. All configuration is left to the… [more](https://www.npmjs.com/package/assemble-core) | [homepage](https://github.com/assemble/assemble-core)
* [base-methods](https://www.npmjs.com/package/base-methods): Starter for creating a node.js application with a handful of common methods, like `set`, `get`,… [more](https://www.npmjs.com/package/base-methods) | [homepage](https://github.com/jonschlinkert/base-methods)
* [base-resolver](https://www.npmjs.com/package/base-resolver): 'base-methods' plugin for resolving and loading globally installed npm modules. | [homepage](https://github.com/jonschlinkert/base-resolver)
* [base-runner](https://www.npmjs.com/package/base-runner): Orchestrate multiple instances of base-methods at once. | [homepage](https://github.com/jonschlinkert/base-runner)
* [resolve-modules](https://www.npmjs.com/package/resolve-modules): Resolves local and global npm modules that match specified patterns, and returns a configuration object… [more](https://www.npmjs.com/package/resolve-modules) | [homepage](https://github.com/jonschlinkert/resolve-modules)  

## Running tests
Install dev dependencies:

```sh
$ npm i -d && npm test
```

## Contributing
Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/verb/issues/new).

## Author
**Jon Schlinkert**

+ [github/jonschlinkert](https://github.com/jonschlinkert)
+ [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License
Copyright © 2015 [Jon Schlinkert](https://github.com/jonschlinkert)
Released under the MIT license.

***

_This file was generated by [verb](https://github.com/verbose/verb) on December 07, 2015._



[assemble]: http://assemble.io
[assemble-core]: https://github.com/assemble/assemble-core
[base-methods]: https://github.com/jonschlinkert/base-methods
[gulp]: http://gulpjs.com
[scaffold]: https://github.com/jonschlinkert/scaffold
[verb]: https://github.com/verbose/verb
[vinyl]: http://github.com/gulpjs/vinyl

