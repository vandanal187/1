The goal is to convert all of Tone.js' modules to Typescript. These are some pointers and guidelines for contributing. 

This is a major undertaking and refactor. These are some notes to get everyone on the same page. 

[Here's a short video of me converting Tone.Reverb](https://www.youtube.com/watch?v=5wo98hOKR5k)

# Up and Running

Hopefully it's as easy as `npm install` to add all of the dependencies and `npm run watch` to start typescript watch

To help with the typescript conversion, i usually use [lebab](https://github.com/lebab/lebab) to speed up getting started. You'll have to edit the file a little before lebab can parse it. This usually includes changing `Tone.ClassName = function` to `const ClassName = function` and all references of `Tone.ClassName` to `ClassName`. I find it is also not able to parse the `defaults` static member and `Tone.extend(ClassName)` so i usually comment those out as well. 

# Guidelines

## 1) Branch

**Please make all Pull Requests on the [typescript branch](https://github.com/Tonejs/Tone.js/tree/typescript).**

Please make the PRs as self contained as possible, so each PR should ideally contain the typescript'ified class and its corresponding typescript test file. 

## 2) Tests

I'm moving tests from the 'test' directory to the same directory as the source files. Tests should end with `.test.ts`. For example, `Noise.ts` should have a test file in the same directory name `Noise.test.ts`. 

Try and get all tests to pass, if a test can't pass because of a changed API or something else, don't comment it out, but instead just mark it as 'skip'. 

For example: 

```javascript
it.skip("does not work yet", () => {
  // can't get this test to work
})
```

## 3) `getDefaults()`

The way that defaults are handled are slightly different with this typescript update. 

Defaults used to look like this:
```javascript
Tone.Noise.defaults = {
	"type" : "white",
	"playbackRate" : 1
};
```

The updated way is to create a static function which returns the default values mixed with the parent object's defaults: 

```typescript
type NoiseType = "white" | "brown" | "pink";

interface NoiseOptions extends SourceOptions {
	type: NoiseType;
	playbackRate: Positive;
}

// ... in the Noise Class
static getDefaults(): NoiseOptions {
	return Object.assign(Source.getDefaults(), {
		playbackRate: 1,
		type: "white" as NoiseType,
	});
}
```

## 4) Context

Part of this update is also making it easier to handle multiple simultaneous AudioContexts. 

For this to work, make sure any internal instances which are created, use the class's `this.context`. 

```typescript
private _volume: Volume = new Volume({
	context: this.context,
});
```

One of the tests in [BasicTests](https://github.com/Tonejs/Tone.js/blob/typescript/test/helper/Basic.js) tries to ensure and enforce this. 

## 5) Naming and Namespace

Previously all classes were added to the `Tone` object which was used as a namespace. In this typescript conversion, all of the modules have their own name and the bundling under one namespace will be handled in a later step to ensure backwards compatibility. 

old:
```javascript
Tone.Noise = function(){
	var options = Tone.defaults(arguments, ["type"], Tone.Noise);
	// ...etc
```

update:
```typescript
export class Noise extends Source {

	name = "Noise";
	// ...etc
```

Also make sure that the class has a "name" property like in the example above. 

The new naming scheme means that some module names need to change. For example `Tone.Buffer` has been renamed to `ToneAudioBuffer` and `Tone.AudioNode` has been changed to `ToneAudioNode`. This is done to avoid any ambiguity with javascript native classes.

## 6) Linting

The typescript update is using [tslint](https://palantir.github.io/tslint/) for linting. You can see the config in `tslint.json`. 

## 7) Constructor

A typical constructor looks something like this. It takes either a list of parameters, or an options object which includes all of the parameters described by `getDefaults()`

```typescript

/**
 * @param frequency The starting frequency of the oscillator.
 * @param type The type of the carrier oscillator.
 * @param modulationType The type of the modulator oscillator.
 */
constructor(frequency?: Frequency, type?: ToneOscillatorType, modulationType?: ToneOscillatorType);
constructor(options?: Partial<AMConstructorOptions>);
constructor() {

	super(optionsFromArguments(AMOscillator.getDefaults(), arguments, ["frequency", "type", "modulationType"]));
	const options = optionsFromArguments(AMOscillator.getDefaults(), arguments, ["frequency", "type", "modulationType"]);
	...
```

A couple of things to note about this: The enumerated arguments are the first overloaded constructor, the options object is the second one, and the overloaded constructor with no arguments is the last one. The `optionsFromArguments` function needs to be used twice here since `options` can't be defined before `super()` is called. Make sure to also add parameter documentation to at least the first constructor description.


# Tooling and Building

This is still in early development, so not all of the tooling and building are completed yet. If you'd like to contribute to this as well, that's also helpful! The goal is to keep it as backwards compatibility in terms of how the library is imported and used. 

## Build Output 

It should build es5 compatible modules as well as a single minified file which exports a single object that all the modules are nested within. 

## Docs

Separately, the documentation pipeline will also need to be worked on. i will start a separate repo for that. 