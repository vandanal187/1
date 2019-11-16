## Download

* [download](https://tonejs.github.io/build/Tone.js)
* [npm](https://www.npmjs.org/) - `npm install tone`
* dev - `npm install tone@next`

## Usage

### Basic

If Tone.js is included in the page, a global variable named `Tone` will be added to the `window`.

### Module Loaders

Internally, Tone uses `import`/`export` for dependency management. 

#### Tone.js build

You can include the build file (which is available from one of the links above) like any other dependency using either AMD or CommonJS style:

```javascript
require(["Tone"], function(Tone){
    var synth = new Tone.MonoSynth();
    //...etc
```

or with CommonJS:

```javascript
var MonoSynth = require("Tone").MonoSynth;
var synth = new MonoSynth();
```

#### Individual Files

Using individual files with a module loader can bring your package size down significantly since it will only include the modules used in your code. You'll have to familiarize yourself with Tone.js' directory structure since files have to be referenced with their full path.

To use the individual files, you'll need a `require` framework which supports AMD like [RequireJS](http://requirejs.org/), [webpack](https://webpack.github.io/), or [deAMDify](https://github.com/jaredhanson/deamdify) for browserify.

**The path to the root [Tone](https://github.com/Tonejs/Tone.js/tree/master/Tone) folder needs to be in the search path so that internal dependencies can resolve.**

##### RequireJS Paths

```javascript
require.config({
    baseUrl: "./base",
    paths: {
        "Tone" : "path/to/Tone.js/Tone"
    }
});
require(["Tone/core/Transport"], function(Transport){
    //...
```

##### Webpack

```javascript
module.exports = {
	resolve: {
		root: __dirname,
                // for webpack 1:
		modulesDirectories : ["path/to/Tone.js/"],
                // for webpack 2:
                modules : ["path/to/Tone.js/"]
	},
	//...
```

##### ES6 Imports

After Tone.js is added as a module resolve path, individual files can be specified like so

```javascript
import Transport from 'Tone/core/Transport';
import Volume from 'Tone/component/Volume';
```

## Newbie MacOS QuickStart to Get Examples Running
If you have XCode installed on your Mac, you should be able to get the examples running with the following steps:
Download the .zip file from github:
https://github.com/Tonejs/Tone.js/archive/dev.zip

The file should unzip automatically, so then in a Terminal window go into the directory:
```javascript
$ cd Tone.js-dev
```
and run the commands:
```javascript
$ npm install 
...
$ npm run build
```

Then you need to run a webserver in the directory to serve the files
```javascript
$ python -m SimpleHTTPServer 8000
```
(note, you have to be in the Tone.js-dev directory when you run the python command)

Then, from a browser visit the URL:
localhost:8000/examples

and you should see the examples.
