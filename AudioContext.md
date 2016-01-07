The Web Audio [AudioContext](https://developer.mozilla.org/en-US/docs/Web/API/AudioContext) is the interface which represents the underlying audio-processing graph built from audio modules linked together. 

In Tone.js, the AudioContext is created for you as soon as Tone.js is loaded; it is accessible as [`Tone.context`](http://tonejs.org/docs/#Tone.context) from the global Tone object or by accessing `.context` from any Tone.js class instance. 

```javascript
var filter = new Tone.Filter();
filter.context; //the shared AudioContext
```

All Tone.js classes share the same AudioContext. Nodes created from different AudioContext's cannot be interconnected. 

### Setting your own AudioContext

In some cases, you might need to explicitly set the AudioContext. 

```javascript
//set another audio context
Tone.setContext(audioContext);
```

You should set the context before creating any nodes since nodes created before the context was set cannot be connected to the nodes created after. 

### Using other Web Audio libraries

Tone.js plays nice with most other Web Audio libraries. 

If the library creates its own instance of the AudioContext, just set Tone's to that one using `Tone.setContext`. If you can pass in an AudioContext to the class constructor, use Tone.context. 

```javascript
//using Tone.js with Tuna.js
var tuna = new Tuna(Tone.context);
```