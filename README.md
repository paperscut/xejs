XEJS
====
_By @angrykoala_

[![npm version](https://badge.fury.io/js/xejs.svg)](https://badge.fury.io/js/xejs)
[![Build Status](https://travis-ci.org/angrykoala/xejs.svg?branch=master)](https://travis-ci.org/angrykoala/xejs)
[![codecov](https://codecov.io/gh/angrykoala/xejs/branch/master/graph/badge.svg)](https://codecov.io/gh/angrykoala/xejs)


>**eXtreme EJS**

XEJS allows you to render files with a custom tag-based language using [EJS](https://github.com/mde/ejs)

> Recursive templating, what could go wrong?

## How it works
**xejs** provides a custom renderer utility on top of **ejs**, allowing you to define your own tags of the type `{{ my tag }}` with custom delimiters (`<< my tag >>`).

**xejs** will then match your custom _regex_ rules (e.g. `/[Tt]itle/`) and map it to a string to be rendered by _ejs_.

The original **EJS** tags of the file (`<% %>`) will be escaped and won't be rendered by xejs


## Usage
```js
var xejs=require('xejs');
var fs= require('fs');

var options={
    openTag: "{{",
    closeTag: "}}",
    tokens: [
        [/bold\s(.+)/, "- '<b>$1</b>'"]
    ]
};


var file=xejs("example/test.ejs",options);

fs.writeFileSync('example/prueba.html',file);
```

This code will render all {{ bold [my text] }} into html `<b>` text

### Provided tags
The tag `include` is already implemented, allowing you to load (and render) another file.

### Examples:
Using the tags delimiters `{{ ... }}`

* `/[Tt]itle/` - `"= title"` will translate any tag of the type `{{ title }}` or `{{Title}}` into a valid `<%- title %>` ejs tag which will be rendered by ejs.



>**Warning:** Only simple tags allowed, nested tags and html-based tags not supported
