## Download

* CDN - [full](https://tonejs.github.io/build/latest/Tone.js) | [min](https://tonejs.github.io/build/latest/Tone.min.js)
* [npm](https://www.npmjs.org/) - `npm install tone`

## Usage

### Basic

Tone.js can be used like any other script or library by dropping the into the `<head>` of your page. A global called `Tone` will be added to the `window`. 

```html
<script type="text/javascript" src="path/to/Tone.js"></script>
```

or from the Tone's CDN:

```html
<script type="text/javascript" src="https://tonejs.github.io/build/latest/Tone.js"></script>
```

Note: it's always safer to use a specific version rather than "latest"

### Module Loaders

Internally, Tone uses AMD for dependency management. But the build process adds a UMD footer to the built file which makes it compatible with both AMD and CommonJS. 

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
		modulesDirectories : ["path/to/Tone.js/"],
	},
	//...
```