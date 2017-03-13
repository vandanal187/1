Tone.js has an extensive test suite built on gulp, mocha and chai. For now, Chrome is the target testing browser, but soon this will be expanded to Firefox as well. 

## Running tests

To the run the tests locally, cd into the `gulp` directory and install all of the dependencies

```bash
cd gulp
npm install
```

You can then run all of the tests by running:

```bash
gulp browser-test
```

To test an individual file use the `--file` or `-f` flag:

```bash
gulp collectTests -f Oscillator
```

Or test a group of components:

```bash
gulp collectTests --event
```