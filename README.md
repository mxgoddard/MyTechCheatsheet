# My Tech Cheatsheet

Compilation of some notes I've made, for all the tech stuff I want to come back to. Trying to connect all the dots one thing at a time.

## Table of Contents
1. [Terminology](#terminology)
    1. [Minify](#minify)
    2. [Source Maps](#sourcemaps)
    3. [Asynchronous](#async)
2. [Programming Languages](#programminglanguages)
    1. [JavaScript](#javascript)
        1. [Gulp](#gulp)
        2. [Ulify](#uglify)
        3. [Jasmin](#jasmine)
        4. [Modernizr](#modernizr)
    2. [Markdown](#markdown)
3. [Software](#software)
    1. [NVM](#nvm)
    2. [Webpack](#webpack)
4. [Code Snippets](#snippets)
    1. [Remove files in a folder](#rmfilesdir)

# Terminology <a name="terminology"></a>

## Minify <a name="minify"></a>

"Minification is the process of removing all unnecessary characters from the source code of interpreted programming languages or markup languages without changing its functionality."

Typically this will remove all whitespace and change all variable names to single characters where possible. If you had a file called xyz.js and decided to minify it, it would typically be renamed to xyz.min.js.

## Source Maps <a name="sourcemaps"></a>

[This link](https://www.html5rocks.com/en/tutorials/developertools/sourcemaps/) was extremely useful.

A source map is basically a way to map a minfied / compiled file back to its unbuilt state. When you build and get ready to release to production, files are minified and compiled for performance. Using developers tools such as chrome, with source mapping you can view minified files in their original source code form.

## Asynchronous Programming <a name="async"></a>

Async (asynchronous) communication is the transmission of data intermittently rather than in a reliable predictable time frame.

Sources of async:

- Network I/O 
    - Making HTTP requests (e.g. GET or POST methods)
- Disk I/O
    - Reading or writing to a local file on a physical medium (e.g. A .txt file on your C: drive)
- User interaction
    - Waiting for user response
- Interprocess communication
    - Web workers
        - Web workers perform tasks in the background of the browser to avoid the UI freezing running

# Programming Languages <a name="programminglanguages"></a>

## JavaScript <a name="javascript"></a>

### [Gulp.js](https://gulpjs.com/) <a name="gulp"></a>

Gulp.js is a toolkit for JavaScript that allows you to automate repetive workflows into a more efficient build pipeline. I've mainly seen it used to minify code (using [Uglify.js](#uglify)) when the project compiles.

### [Uglify.js](https://www.npmjs.com/package/uglify-js) <a name="uglify"></a>

- A package for minifying code (The names uglify and minify are synonymous).
- Only supports ECMAScript 5 (ES5, 2011). For ES6 (2015) and more recent (up to ES11 in 2020), use [Babel](https://babeljs.io/).

### [Jasmine](https://jasmine.github.io/) <a name="jasmine"></a>

Jasmine is a behaviour driven, open-source testing framework that aims to run on any JavaScript enabled platform non-intrusively.

### [Modernizr](https://modernizr.com/) <a name="modernizr"></a>

When used, Modernizr runs some quick tests when your web page loads to see which features the current users browser can run.

## [Markdown](https://en.wikipedia.org/wiki/Markdown) <a name="markdown"></a>

Markdown (.md) is a markup language mainly used for formatting documentation and README files such as this one.

Remembering HTML stands for Hypertext Markup Language and is used to design (format) documents in a web browser helped connect some dots for me.

Using a block of triple backtick (`) characters we can create a code block where we can specify the language used for syntax highlighting. Rubycoloredglasses has a nice list of the available languages [here](http://www.rubycoloredglasses.com/2013/04/languages-supported-by-github-flavored-markdown/).

``` markdown
``` javascript
let text = 'Hello, World!';
console.log(text);
```

# Software <a name="software"></a>

## [Node Version Manager](https://github.com/coreybutler/nvm-windows) <a name="nvm"></a>

I came across NVM (Node Version Manager) because I couldn't run methods in my gulpfile. We sussed it down my version of NodeJS being too modern for the version of gulp. The actual error was something like 'ReferenceError: primordials is not defined', which when searched on google brought us to [this stack overflow page](https://stackoverflow.com/questions/55921442/how-to-fix-referenceerror-primordials-is-not-defined-in-node). Basically to solve we either had to upgrade gulp or downgrade node.

So NVM is used to manage and switch between multiple installations of node. I needed an older version of node to run my gulpfile method which using this could easily do without losing my current install.

``` javascript
// This is roughly what my gulp method looked like to minify an array of scripts
gulp.task("myGulpMethod", function () {
	return gulp.src(arrayOfJsScripts)
		.pipe(plugins.concat("outputFileName.js"))
		.pipe(plugins.uglify())
		.pipe(gulp.dest("./outputFileDirectory/js"));
});
```

Manually running the gulp task in the directory containing the gulpfile.

``` bash
WORKING_DIRECTORY> gulp myGulpMethod
    ReferenceError: primordials is not defined.
```

This when run in the console gives the error above. So using NVM, this is how I fixed it.

``` bash
# After installing NVM from the GitHub page
> nvm list
> nvm install 8.11.1
> nvm use 8.11.1
# Check we are on the correct version of node now
> nvm list
# Navigate to working directory containing the gulpfile.js
> cd WORKING_DIRECTORY
# Run the gulp method
WORKING_DIRECTORY> gulp myGulpMethod
```

Now the gulp task works completely as expected.

## [Webpack](https://webpack.js.org/) <a name="webpack"></a>

Bundle code modules with dependencies into static assets that can be called from html script tags.

# Code Snippets <a name="snippets"></a>

You can either paste these snippets into raw files or export them as methods and use them that way. Generally, using JavaScript, I'll write the code into the file (e.g. HelloWorld.js) and run it with Node.

``` javascript
/* HelloWorld.js */
console.log('Hello, World!');
```

``` bash
# ls (unix) or dir (windows) to list files in directory 
> ls
    HelloWorld.js

> node HelloWorld.js
    Hello, World!
```

## Remove files in a folder <a name="rmfilesdir"></a>

JavaScript script to programatically remove files in a directory. Can be conditional to specific file types.

``` javascript
const fs = require('fs');
const path = require('path');

// The directory you want to purge
const directory = 'C:/Users/your_name/somewhere';

// Remove all png files
const extension = '.png';

fs.readdir(directory, (err, files) => {
    if (err) {
        console.log(err);
        throw err;
    }

    for (let file of files) {
        if (file.includes(extension)) {
            fs.unlink(path.join(directory, file), err => {
                if (err) {
                    console.log(err);
                    throw err;
                }
            });
        }
    }
});
```

## Checklist for this page

- [x] Make a contents page
- [x] Add Gulp for an intial commit
- [x] Work out how to manage and split out this page (hierarchy)
- [ ] Git
- [x] Source Maps
- [x] Async
