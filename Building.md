# Installing Dependencies

Tone.js uses [gulp](http://gulpjs.com/) and [requirejs](http://requirejs.org/) for building and dependency management. 

Make sure you have both of those installed (as well as [node.js](nodejs.org)). From within the 'gulp' directory, run `npm install` to install all of the dependencies.

## Build

Once all of the dependencies are installed, simply run `gulp` from the command line. The dependency order will be resolved and all of the files will be combined into `Tone.js` and `Tone.min.js` in the 'build' folder. 