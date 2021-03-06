![CI Status](https://travis-ci.org/revelrylabs/sassy-npm-importer.svg?branch=master)

# sassy-npm-importer

Import SASS from npm via a customizable prefix, like:

```
@import "npm://reset-scss/";
```

&nbsp;

## Installation

```
npm install --save sassy-npm-importer
```

In practice, you would probably be using a task runner (like Gulp). This is an
example of how to provide the importer directly to `node-sass`:

```
var sass = require('node-sass');
var importer = require('sassy-npm-importer').importer;

var result = sass.renderSync({
  file: __dirname + '/styles.scss',
  importer: importer() // No options passed, uses defaults.
});
```

&nbsp;

## Quick Start

Once you've installed the package, you can follow these instructions to test
the importer. This example shows you how to import the
`foundation-sites` package.

```
npm install --save node-sass                # for this example
npm install --save foundation-sites         # example package
```

## Usage

In practice you would probably be using something like a Gulp task here, but this is how to provide the importer directly to `node-sass`:

### node: `index.js`

```
var sass = require('node-sass');
var importer = require('sassy-npm-importer').importer;

var result = sass.renderSync({
  file: __dirname + '/styles.scss',
  importer: importer() // No options passed, uses defaults.
});
```

Create a SASS file that `@import`s from a package manager.

### npm: `styles.scss`
```
@import 'npm://foundation-sites/scss/foundation';
@include foundation-everything;
```

&nbsp;

## Command Line

You can also use sassy-npm-importer via the command line.

```
node-sass --importer ./node_modules/sassy-npm-importer stylesheet.scss
```

&nbsp;

## Importing packages

Some node packages contain a `main` property which points to a SASS file.
Instead of having to enter the long path to a file, you can simply use the
package name and this main file is included.

For example, if a dependency had a `package.json` file which was similar to:

```
{
  "name": "my-sass-dependency",
  "main": "reset.scss"
}
```

Then you have the option of how to import the dependency, all are valid:

```
# This long form with the extension
@import "npm://my-sass-dependency/reset.scss";

# This long form without the extension
# Matches one of: _reset.scss, reset.scss, _reset.css and reset.css
@import "npm://my-sass-dependency/reset";

# The short form, will include whatever `main` refers to
# In this example: reset.scss
@import "npm://my-sass-dependency/";

# The final slash is optional
@import "npm://my-sass-dependency";
```

&nbsp;

## Options

### options.debug

More verbose output.

* Since: 1.0.0

```
importer({ debug: true })
```

&nbsp;

### options.prefix

Attaches a prefix that rewrites to `npm://` to node modules.

* Since: 1.0.0

```
importer({ prefix: '~/' })
```

```
@import '~/foundation-sites/scss/foundation'
# is now the same as
@import 'npm://foundation-sites/scss/foundation'
```

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/revelrylabs/sassy-npm-importer. Check out [CONTRIBUTING.md](https://github.com/revelrylabs/sassy-npm-importer/blob/master/CONTRIBUTING.md) for more info.

Everyone is welcome to participate in the project. We expect contributors to
adhere the Contributor Covenant Code of Conduct (see [CODE_OF_CONDUCT.md](https://github.com/revelrylabs/sassy-npm-importer/blob/master/CODE_OF_CONDUCT.md)).
