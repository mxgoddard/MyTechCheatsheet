# My Tech Cheatsheet

Compilation of some notes I've made, for all the tech stuff I want to come back to.

## Table of Contents
1. [Terminology](#terminology)
    1. [Minify](#minify)
2. [Programming Languages](#programminglanguages)
    1. [JavaScript](#javascript)
        1. [Gulp](#gulp)
        2. [Ulify](#uglify)
        3. [Jasmin](#jasmine)
        4. [Modernizr](#modernizr)
3. [Software](#software)
    1. [NVM](#nvm)

# Terminology <a name="terminology"></a>

## Minify <a name="minify"></a>

"Minification is the process of removing all unnecessary characters from the source code of interpreted programming languages or markup languages without changing its functionality."

Typically this will remove all whitespace and change all variable names to single characters where possible. If you had a file called xyz.js and decided to minify it, it would typically be renamed to xyz.min.js. 

# Programming Languages <a name="programminglanguages"></a>

## JavaScript <a name="javascript"></a>

### [Gulp.js](https://gulpjs.com/) <a name="gulp"></a>

Gulp.js is a toolkit for JavaScript that allows you to automate repetive workflows into a more efficient build pipeline. I've mainly seen it used to minify code (using [Uglify.js](#uglify)) when the project compiles.

### [Uglify.js](https://www.npmjs.com/package/uglify-js) <a name="uglify"></a>

- A package for minifying code (The names uglify and minify are synonymous).
- Only supports ECMAScript 5 (ES5, 2011). For ES6 (2015) and more recent (up to ES11 in 2020), use [Babel](https://babeljs.io/).

### [Jasmine Page](https://jasmine.github.io/) <a name="jasmine"></a>

Jasmine is a behaviour driven, open-source testing framework that aims to run on any JavaScript enabled platform non-intrusively.

### [Modernizr Page](https://modernizr.com/) <a name="modernizr"></a>

When used, Modernizr runs some quick tests when your web page loads to see which features the current users browser can run.

# Software <a name="software"></a>

## [Node Version Manager](https://github.com/coreybutler/nvm-windows) <a name="nvm"></a>

I came across NVM (Node Version Manager) because I couldn't run methods in my gulpfile. We sussed it down my version of NodeJS being too modern for the version of gulp. The actual error was something like 'ReferenceError: primordials is not defined', which when searched on google brought us to [this stack overflow page](https://stackoverflow.com/questions/55921442/how-to-fix-referenceerror-primordials-is-not-defined-in-node). Basically to solve we either had to upgrade gulp or downgrade node.

So NVM is used to manage and switch between multiple installations of node. I needed an older version of node to run my gulpfile method which using this could easily do without losing my current install.

```javascript
// This is roughly what my gulp method looked like to minify an array of scripts
gulp.task("myGulpMethod", function () {
	return gulp.src(arrayOfJsScripts)
		.pipe(plugins.concat("outputFileName.js"))
		.pipe(plugins.uglify())
		.pipe(gulp.dest("./outputFileDirectory/js"));
});
```

```bash
# Manually running the gulp task
> gulp myGulpMethod
    ReferenceError: primordials is not defined.
```

This when run in the console gives the error above. So using NVM, this is how I fixed it.

```bash
# After installing NVM from the GitHub page
> nvm list
> nvm install 8.11.1
> nvm use 8.11.1
# Check we are on the correct version of node now
> nmv list
# Navigate to working directory containing the gulpfile.js
> cd WORKING_DIRECTORY
# Run the gulp method
WORKING_DIRECTORY> gulp myGulpMethod
```

Now the gulp task works completely as expected.

## Checklist for this page

- [x] Make a contents page
- [x] Add Gulp for an intial commit
- [x] Work out how to manage and split out this page (hierarchy)
- [x] Dummy point