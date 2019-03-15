# LintHTML

[![npm version](http://img.shields.io/npm/v/lintHTML.svg?style=flat-square)](https://npmjs.org/package/lintHTML)
[![license](http://img.shields.io/npm/l/lintHTML.svg?style=flat-square)](https://npmjs.org/package/lintHTML)
[![Build Status](https://travis-ci.org/linthtml/lintHTML.svg?branch=develop)](https://travis-ci.org/linthtml/lintHTML)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Flinthtml%2FlintHTML.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Flinthtml%2FlintHTML?ref=badge_shield)

> An unofficial html5 linter and validator.

_LintHTML uses [htmlparser2](https://www.npmjs.com/package/htmlparser2) to parse your html._

## Installation and Usage

Prerequisites: [Node.js](https://nodejs.org/en/) (>=6.14), npm version 3+.

There are two ways to install LintHTML: globally and locally.

### Local Installation and Usage

If you want to include LintHTML as part of your project's build system, we recommend installing it locally. You can do so using npm:

```shell
npm install linthtml --save-dev
```

You should then set up a configuration file:

```shell
./node_modules/.bin/linthtml --init
```

After that, you can run LintHTML on any file or directory like this:

```shell
./node_modules/.bin/linthtml yourfile.html
```

### Global Installation and Usage

If you want to make LintHTML available to tools that run across all of your projects, we recommend installing LintHTML globally. You can do so using npm:

```shell
npm install -g linthtml
```

You should then set up a configuration file:

```shell
linthtml --init
```

After that, you can run LintHTML on any file or directory like this:

```shell
linthtml yourfile.html
```

<!-- Note: `linthtml --init` is intended for setting up and configuring linthtml on a per-project basis and will perform a local installation of ESLint and its plugins in the directory in which it is run. If you prefer using a global installation of ESLint, any plugins used in your configuration must also be installed globally. -->

## Rules

Current list of rules and deprecations can be found in [docs/rules.md](docs/rules.md).

Rules can be configured using e a JavaScript, JSON or YAML file. This can be in the form of an .linthtml.* file or an , `linthtmlConfig` field in a `package.json` file, both of which LintHTML will look for and read automatically, or you can specify a configuration file on the command line using the `--config` option.

### Inline Configuration

Sometimes it is necessary to use different option values for different parts of an html document. Maybe there is an unavoidable break in style at some point, or two different teams wrote different sections of the document, or part of the page is written in an html-like language like svg that has different linting standards. Inline configurations allow a user to turn on or off certain rules (or pull in entire presets) at any line while linting.

### Format of Inline Configurations

Inline configurations are html comments, but are formatted like self-closing html tags:

```html
<!-- linthtml-configure [key]="[value]" -->
```

In order for an inline configuration to be recognized, it must be an html comment enclosed with `<!-- and -->` and begin with the keyword 'linthtml'.

Configurations must also use valid html attribute formatting. An unlimited number of attributes are allowed in an inline configuration and each rules will be applied in order. Inline configurations only apply to the file they are located in, and will not roll over to other files.

Values may be quoted using either double or single quotes, or may be left without quotes if they contain no spaces. In any case, we will refer to the string, ignoring surrounding quotes, as the "value" to be assigned to the option.

To specify an inline configuration for a rule, use one of this two thing :

* A value for the rule, encoded in pretty-much-JSON.
* The string $previous.

### Rule value

To modify a single rule, use an attribute with that rule's name and the value you wish to assign to it.

```html
<!-- turn off rule `tag-bans` -->
<!-- linthtml-configure tag-bans="false" -->

<!-- Specify a config for the  `tag-bans` rule -->
<!-- linthtml-configure tag-bans="['p','style']" -->
```

<!-- 
The attribute name must be an existing rule name, using [a-zA-Z0-9] and/or the characters - and _ (which are treated interchangeably). The attribute value must be a JSON object (for instance ["style", "b", "i"], or false), with two exceptions: single quotes are allowed and will be treated like double quotes, and string values (such as "crlf"), do not need to be quoted. -->

### $previous

Each rule's previous value (if any) is stored, and may be recalled using `$previous`. This is useful if an option should be temporarily disabled or changed, since the value it was at before being changed is not always easy to determine.

```html
<!-- turn off rule `tag-bans` -->
<!-- linthtml-configure tag-bans="false" -->

<!-- turn on rule `tag-bans` -->
<!-- linthtml-configure tag-bans="$previous" -->
```

<!-- As a one-level undo, this option is inherently quite limited. Our team discussed the possibility of a heirarchical undo, and we believe that the feature would be very rarely needed and difficult to use correctly. In particular, a group of people working on a large html document would need to be aware of all of the option resets in the document to ensure that two do not overlap (thus causing unexpected behavior when the settings and resettings are mismatched). The $previous feature is intended only for small sections when there is not very much space between an option value and the reversion. -->

### Other

We have a some other solutions to run linthtml

This module doesn't provide any interface on its own. It is highly recommended that
you use one of the following modules to run the linter:

* [`gulp-linthtml`](https://github.com/linthtml/gulp-linthtml): a gulp interface for lintHTML (Coming soon 🚧)
* [`linthtml-loader`](https://github.com/linthtml/linthtml-loader): lintHTML loader for webpack (Coming soon 🚧)
* [`broccoli-linthtml`](https://github.com/linthtml/broccoli-linthtml): Integrates HTML linting with lintHTML as part of your Broccoli build pipeline. (Coming soon 🚧)

## Contributing

Contribution are welcome, please make sure to use the proper github tag on your issue/PR.

* `cli` : For anything that is related to the cli interface of linthml
* `rule` : For anything that is related the rules (bugs, improvement, docs, new rule...)
* `core` : For anything that is related to the core of linthml (file parsing, plugin system...)

## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Flinthtml%2FlintHTML.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Flinthtml%2FlintHTML?ref=badge_large)
