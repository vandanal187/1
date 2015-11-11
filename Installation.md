## Download

* CDN by Github pages - [full](http://cdn.tonejs.org/latest/Tone.js) | [min](http://cdn.tonejs.org/latest/Tone.min.js)
* [bower](http://bower.io/) - `bower install tone`
* [npm](https://www.npmjs.org/) - `npm install tone`

## Usage

### Basic

Tone.js can be used like any other script or library by dropping the into the <head> of your page. A global called `Tone` will be added to the `window`. 

```html
<script type="text/javascript" src="path/to/Tone.js"></script>
```

or from the Tone's CDN:

```html
<script type="text/javascript" src="http://cdn.tonejs.org/latest/Tone.min.js"></script>
```

Note: it's always safer to use a specific version rather than "latest"

### Module Loaders

Tone uses AMD internally for dependency management. 

#### Using the Tone.js build

The build of Tone.js is UMD compatible. You can include it like any other dependency:

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

Using individual files with a module loader can bring your package size down significantly since it will only include the modules used in your code. You'll have to familiarize yourself with Tone.js' directory structure since files have to be referenced with their full path. Make sure that the directory `Tone` points to the `Tone` directory of the source code so that internal dependencies can resolve. 


```javascript
//Using 'paths' in RequireJS
require.config({
    baseUrl: "./base",
    paths: {
        "Tone" : "path/to/Tone.js/Tone"
    }
});
require(["Tone/core/Transport"], function(Transport){
    //...
```