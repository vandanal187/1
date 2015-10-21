# Contributing

Bug fixes, examples, and contributions are welcome!

Please get in touch (yotammann@gmail.com) and tell me what features you'd like to see or contribute to. 

**Please make all Pull Requests to the `dev` branch.**

## Setup

The dependencies required to build and develop the library can be installed using `npm install` from the `grunt` directory.

# Style

Make sure the code is clearly commented with jsdoc style comments and also has no jshint errors or warnings (take a look at the .jshintrc file to see the jshint settings). 

All classes have a dispose method where all their members are disconnected, disposed and nulled. 

#### Nitpicky

* 4 space TAB indentation. 
* 1 empty line between function definitions. 

# Areas

Here are a few areas that I'd love some more help/contributions with. 

### Examples

To contribute examples, please follow the current style of the examples as closely as possible. Add your example's title and file name to `ExampleList.js` file for it to appear in the examples list on index page. 

### Tests 

Tone.js has an extensive test suite using Mocha and Chai. I'd love help getting more of these tests to pass on Safari and Firefox.

I'd also like to eventually setup a CI environment which can automatically test if commits and PRs pass all of the tests. Web Audio won't run headless with PhantomJS, but something like [Karma-Runner](http://karma-runner.github.io/0.12/index.html) on Travis CI could work well. 

Along with more unit tests, I'd also like to have more tests which run in the online context and generate nice music so that we can find bugs by ear that the automated tests might not illuminate. [Audiokit](http://audiokit.io/tests/) for example has a great suite of aural tests.

### Docs

There is always more work that can be done on documentation. Especially adding good examples to methods and members to make the docs more informative and useful for people coming from diverse musical and technical backgrounds. 

Along with this, I'd love to integrate an interactive, nested graph visualization which could be embedded in the docs for each class and show you the exact signal flow for each component. It'd be great if this graph could be automatically extracted from the code. 

### Tutorials

I'd love to see more tutorials for newcomers to Tone.js to help them get up and running or solve a particular issue. If you make a tutorial, please send me a link.

### Synths/Effects

If you'd like to contribute a cool and expressive synth or effect, i'd love to hear it. Please send me an example that i can play with along with the PR. 

# Transfer Notice

I've moved the repo to a new organization devoted entirely to Tone.js. While all of the links will automatically forward to the new repo, if you forked before the change, you'll have to update the remote url in order to pull or make pull requests. 

```bash
git remote set-url origin https://github.com/Tonejs/Tone.js.git
```
or, if you use ssh:
```bash
git remote set-url origin git@github.com:Tonejs/Tone.js.git
```