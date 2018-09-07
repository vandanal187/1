Tone.js has an extensive test suite built on karma, mocha and chai.

## Installing

To install all testing dependencies: 

```bash
npm install
```

## All tests

To run all tests on Chrome and Firefox using Karma Test Runner:

```bash
npm run test
```

## Testing files

To test an individual file with karma: 

```bash
npm run test --file=Oscillator
```

(replace `Oscillator` with the name of the test file you'd like to run)

## Testing directories

To run all tests in a directory run:

```bash
npm run test --dir=core
```

(replace `core` with the name of the directory you'd like to run)
