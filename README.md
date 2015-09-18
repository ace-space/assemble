# assemble [![NPM version](https://badge.fury.io/js/assemble.svg)](http://badge.fury.io/js/assemble)

> Make stuff.

<!-- toc -->

* [Install](#install)
* [Usage](#usage)
* [assemblefile.js](#assemblefilejs)
* [API](#api)
* [Related projects](#related-projects)
* [Running tests](#running-tests)
* [Contributing](#contributing)
* [Author](#author)
* [License](#license)

_(Table of contents generated by [verb])_

<!-- tocstop -->

## Install

Install with [npm](https://www.npmjs.com/)

```sh
$ npm i assemble --save
```

## Usage

```js
var assemble = require('assemble');
var app = assemble();
```

## assemblefile.js

The following example `assemblefile.js` includes tasks for generating `.html` files from templates and `.css` stylesheets from `.less`.

```js
var assemble = require('assemble');
var extname = require('gulp-extname');
var less = require('gulp-less');
var app = assemble();

app.task('html', function() {
  app.src('templates/*.hbs')
    .pipe(extname('.html'))
    .pipe(app.dest('dist/'));
});

app.task('css', function () {
  app.src('styles/*.less')
    .pipe(less())
    .pipe(app.dest('dist/assets/css'));
});

app.task('default', ['html', 'css']);
```

## API

### [Assemble](index.js#L25)

Create an `assemble` application. This is the main function exported by the assemble module.

**Params**

* `options` **{Object}**: Optionally pass default options to use.

**Example**

```js
var assemble = require('assemble');
var app = assemble();
```

### [.process](index.js#L146)

Copy a file from `src` to `dest` and process any templates in
`file.contents`.

**Params**

* `file` **{Object}**: [Vinyl][] file object.
* `options` **{Object}**
* `returns` **{Stream}**: Returns a stream to continue processing if needed.

### [.generate](index.js#L195)

Generate all of the `src`/`dest` definitions in the given
`config` object. Used for generating [boilerplates][] and
[scaffolds][].

**Params**

* `config` **{Object}**: The configuration object to use.
* `cb` **{Function}**: Callback function, exposes `err` on the callback.
* `returns` **{Object}**: Returns the `Assemble` instance for chaining.

### [.src](index.js#L217)

Glob patterns or filepaths to source files.

**Params**

* `glob` **{String|Array}**: Glob patterns or file paths to source files.
* `options` **{Object}**: Options or locals to merge into the context and/or pass to `src` plugins

**Example**

```js
app.src('src/*.hbs', {layout: 'default'});
```

### [.symlink](index.js#L232)

Glob patterns or paths for symlinks.

**Params**

* `glob` **{String|Array}**

**Example**

```js
app.symlink('src/**');
```

### [.dest](index.js#L248)

Specify a destination for processed files.

**Params**

* `dest` **{String|Function}**: File path or rename function.
* `options` **{Object}**: Options and locals to pass to `dest` plugins

**Example**

```js
app.dest('dist/');
```

### [.copy](index.js#L268)

Copy files with the given glob `patterns` to the specified `destDir`.

**Params**

* `patterns` **{String|Array}**: Glob patterns of files to copy.
* `dest` **{String|Function}**: Desination directory.
* `returns` **{Stream}**: Stream, to continue processing if necessary.

**Example**

```js
app.task('assets', function() {
  app.copy('assets/**', 'dist/');
});
```

### [.toStream](index.js#L288)

Push a view collection into a vinyl stream.

**Params**

* `collection` **{String}**: The name of the view collection to push into the stream.
* **{Function}**: Optionally pass a filter function to use for filtering views.
* `returns` **{Stream}**

**Example**

```js
app.toStream('posts', function(file) {
  return file.path !== 'index.hbs';
})
```

### [.renderFile](index.js#L316)

Render a vinyl file.

**Params**

* `locals` **{Object}**: Optionally locals to pass to the template engine for rendering.
* `returns` **{Object}**

**Example**

```js
app.src('*.hbs')
  .pipe(app.renderFile());
```

### [.task](index.js#L352)

Define an Assemble task.

**Params**

* `name` **{String}**: Task name
* `fn` **{Function}**: function that is called when the task is run.

**Example**

```js
app.task('default', function() {
  app.src('templates/*.hbs')
    .pipe(app.dest('dist/'));
});
```

### [.run](index.js#L371)

Run one or more tasks.

**Params**

* `tasks` **{Array|String}**: Task name or array of task names.
* `cb` **{Function}**: callback function that exposes `err`

**Example**

```js
app.run(['foo', 'bar'], function(err) {
  if (err) console.error('ERROR:', err);
});
```

**Params**

* `glob` **{String|Array}**: Filepaths or glob patterns.
* `tasks` **{Array}**: Task(s) to watch.

**Example**

```js
app.task('watch', function() {
  app.watch('docs/*.md', ['docs']);
});
```

## Related projects

Assemble is built on top of these great projects:

* [boilerplate](https://www.npmjs.com/package/boilerplate): Tools and conventions for authoring and publishing boilerplates that can be generated by any build… [more](https://www.npmjs.com/package/boilerplate) | [homepage](http://boilerplates.io)
* [composer](https://www.npmjs.com/package/composer): API-first task runner with three methods: task, run and watch. | [homepage](https://github.com/jonschlinkert/composer)
* [generate](https://www.npmjs.com/package/generate): Project generator, for node.js. | [homepage](https://github.com/generate/generate)
* [scaffold](https://www.npmjs.com/package/scaffold): Conventions and API for creating scaffolds that can by used by any build system or… [more](https://www.npmjs.com/package/scaffold) | [homepage](https://github.com/jonschlinkert/scaffold)
* [templates](https://www.npmjs.com/package/templates): System for creating and managing template collections, and rendering templates with any node.js template engine.… [more](https://www.npmjs.com/package/templates) | [homepage](https://github.com/jonschlinkert/templates)
* [verb](https://www.npmjs.com/package/verb): Documentation generator for GitHub projects. Verb is extremely powerful, easy to use, and is used… [more](https://www.npmjs.com/package/verb) | [homepage](https://github.com/verbose/verb)

## Running tests

Install dev dependencies:

```sh
$ npm i -d && npm test
```

## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/assemble/issues/new).

If Assemble doesn't do what you need, [please let us know][issue].

## Author

**Jon Schlinkert**

+ [github/jonschlinkert](https://github.com/jonschlinkert)
+ [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright © 2015 Jon Schlinkert
Released under the MIT license.

***

_This file was generated by [verb-cli](https://github.com/assemble/verb-cli) on September 17, 2015._

[boilerplate]: http://boilerplates.io
[scaffold]: https://github.com/jonschlinkert/scaffold
[template]: https://github.com/jonschlinkert/template
[template]: https://github.com/jonschlinkert/template
[verb]: https://github.com/verbose/verb
