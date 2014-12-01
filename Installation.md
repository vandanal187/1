# Installation

There are a few ways to download and install Tone.js. 

## Downloading

* Github - [full](https://raw.githubusercontent.com/TONEnoTONE/Tone.js/master/build/Tone.js) | [min](https://raw.githubusercontent.com/TONEnoTONE/Tone.js/master/build/Tone.min.js)
* [Bower](http://bower.io/) - bower install tone
* [npm](https://www.npmjs.org/) - npm install tone

## Using

RequireJS is the recommended way to use Tone.js but it can also be used just as well without it. 

### without RequireJS

Tone.js can be used like any other script or library by dropping the into the <head> of your page. A global called `Tone` will be added to the `window`. 

```html
<script type="text/javascript" src="path/to/Tone.js"></script>
```

To use any of the instrument and effect presets, be sure to grab the [Tone.Presets build](https://raw.githubusercontent.com/TONEnoTONE/Tone.js/master/build/Tone.Preset.js) which is not included in the default build. 

### RequireJS

[RequireJS](http://requirejs.org/) is a JavaScript module loader which Tone.js uses internally for dependency management. It is a powerful tool for development and deploying. Using r.js (RequireJS's optimizer) can bring package size down significantly since it will only include the modules used in your code. 

#### Build

You can use the built file with Require like any other external script.

```javascript
require(["Tone"], function(Tone){
    var synth = new Tone.MonoSynth();
    //...etc
```

#### Directory

For the full RequireJS experience, maintain the directory structure of the library and reference all modules from the root directory "Tone". Add a path to the root directory. This will require familiarizing yourself with the directory structure. 

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