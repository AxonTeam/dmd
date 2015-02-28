[![view on npm](http://img.shields.io/npm/v/dmd.svg)](https://www.npmjs.org/package/dmd)
[![npm module downloads per month](http://img.shields.io/npm/dm/dmd.svg)](https://www.npmjs.org/package/dmd)
[![Build Status](https://travis-ci.org/75lb/dmd.svg?branch=master)](https://travis-ci.org/75lb/dmd)
[![Dependency Status](https://david-dm.org/75lb/dmd.svg)](https://david-dm.org/75lb/dmd)

# dmd
dmd (document with markdown) is a [handlebars](http://handlebarsjs.com) partial and helper pack for generating markdown API documentation (see [jsdoc-to-markdown](https://github.com/75lb/jsdoc-to-markdown) for example output). It has <code>[one function](#module_dmd)</code> into which you feed [jsdoc-parse](http://handlebarsjs.com) data and a template. 

## Synopsis
With this input file containing [jsdoc-parse](http://handlebarsjs.com) output:
```json
[
    {
        "id": "fatUse",
        "name": "fatUse",
        "kind": "member",
        "description": "I am a global variable",
        "scope": "global"
    }
]
```
this command :
```
$ cat examples/input/doclet.json | dmd
```
produces this output: 
```
<a name="fatUse"></a>
## fatUse
I am a global variable

**Kind**: global member
```

## Templates
The default template simply renders the [main](https://github.com/75lb/dmd/blob/master/partials/main.hbs) partial:
```hbs
{{>main}}
```

This partial outputs all documentation and an index (if there are enough items). If you supply your own template, you can customise the output:
```hbs
# A Module
This is the readme for a module. 

## Install
Install it using the power of thought. 

# API Documentation
{{>main}}
```

## Usage
### As a library
Install:
```sh
$ npm install dmd --save
```
Example:
```js
var dmd = require("dmd");

process.stdin.pipe(dmd()).pipe(process.stdout);
```

### At the command line
Install the `dmd` tool globally: 
```sh
$ npm install -g dmd
```
Example:
```sh
$ cat examples/doclet.json | dmd
```

## Plugins
* [dmd-examples-highlight](https://github.com/75lb/dmd-examples-highlight)
    
# API Reference
<a name="exp_module_dmd--dmd"></a>
### dmd([options]) ⇒ <code>[TransformStream](http://nodejs.org/api/stream.html#stream_class_stream_transform)</code> ⏏
Transforms doclet data into markdown documentation. Returns a transform stream - pipe doclet data in to receive rendered markdown out.

**Kind**: Exported function  
**Params**

- \[options\] <code>object</code> - The render options  
  - \[template =<code>&quot;\{\{&gt;main\}\}&quot;</code>\]  - {string} - A handlebars template to insert your documentation into.  
  - \[heading-depth =<code>2</code>\] <code>number</code> - the heading depth to begin the docs from (e.g. `2` starts from a markdown heading of `##`).  
  - \[example-lang\] <code>string</code> - for syntax highlighting on github  
  - \[partial\] <code>string</code> | <code>Array.&lt;string&gt;</code> - overrides  
  - \[helper\] <code>string</code> | <code>Array.&lt;string&gt;</code> - overrides  
  - \[plugin\] <code>string</code> | <code>Array.&lt;string&gt;</code> - packages containing overrides  
* * *

&copy; 2015 Lloyd Brookes <75pound@gmail.com>. Documented by [jsdoc-to-markdown](https://github.com/75lb/jsdoc-to-markdown).
