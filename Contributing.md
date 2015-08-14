# Contributing

Bug fixes, examples, and contributions are welcome!

Please get in touch (yotammann@gmail.com) and tell me what features you'd like to see or contribute to. 

And make all pull requests to the `dev` branch. 

## Examples

To contribute examples, please follow the current style of the examples as closely as possible. Add your example to the ExampleList.js file for it to appear in the drop-down and index page. 

## Development dependencies

The dependencies required to build and develop the library can be installed using `npm`

    cd grunt
    npm install

## Testing 

Tone.js has an extensive test suite that can be run in the browser. To run the tests, arrange for the project root directory to be served by your development machine and then visit `<project-root>/test/index.html`.

## Style

Make sure the code is clearly commented with jsdoc style comments and also has no jshint errors or warnings (take a look at the .jshintrc file to see the jshint settings). 

All classes have a dispose method where all their members are disconnected, disposed and nulled. 

#### Nitpicky

* 4 space TAB indentation. 
* 1 empty line between function definitions. 

# Transfer Notice

I've moved the repo to a new organization devoted entirely to Tone.js. While all of the links will automatically forward to the new repo, if you forked before the change, you'll have to update the remote url in order to pull or make pull requests. 

```bash
git remote set-url origin https://github.com/Tonejs/Tone.js.git
```
or, if you use ssh:
```bash
git remote set-url origin git@github.com:Tonejs/Tone.js.git
```