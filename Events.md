Tone.js has a few callback-generating classes which simplify the scheduling of complexly-timed events along the Transport. These events can be set to start and stop at specific moments along the Transport, as well as loop and playback at different rates. **Events will not fire unless the Transport is started.**

### Tone.Event

Tone.Event is the base-class for musical events. It creates a callback with a value which will be passed in as the second argument to the callback. 

```javascript
//create a looped note event every half-note
var note = new Tone.Event(function(time, pitch){
	synth.triggerAttackRelease(pitch, "16n", time);
}, "C2");

//set the note to loop every half measure
note.set({
	"loop" : true,
	"loopEnd" : "2n"
});

//start the note at the beginning of the Transport timeline
note.start(0);

//stop the note on the 4th measure
note.stop("4m");
```
#### `probability`

Events have a probability parameter which allows you to adjust the probability of the event firing each time it is scheduled to. 

```javascript
//fire 50% of the time
note.probability = 0.5;
```

#### `humanize`

"Humanization" let's you adjust how rigid the callback timing is. If `humanize` is set to `true`, the passed-in `time` parameter will drift back and forth slightly to make the part feel a little more "human". You can also set `humanize` to a Time value, which will make it drift by that amount. 

```javascript
//drift by +/- a 32nd-note
note.humanize = "32n";
```

#### `playbackRate`

You can also adjust the playback-rate of all Event classes. 

```javascript
//loop the event twice as fast. 
note.playbackRate = 2;
```

### Tone.Loop

Tone.Loop is a simplified Tone.Event. It has many of the same attributes as Tone.Event except instead of a `loopEnd` property, the duration of the loop is defined by the `interval` and it is set to loop by default. The constructor takes an `interval` after the callback

```javascript
//loop the callback every 8th note from the beginning of the Timeline
var loop = new Tone.Loop(callback, "8n").start(0);
```

### Tone.Part

Tone.Part aggregates any number of Tone.Events which can be started, stopped and looped as a combined unit. Parts have all of the same methods as Tone.Events. 

They can be constructed with either an array of `[Time, Value]` pairs, or with an array of objects that contain a `"time"` property. 

```javascript
var part = new Tone.Part(function(time, pitch){
	synth.triggerAttackRelease(pitch, "8n", time);
}, [["0", "C#3"], ["4n", "G3"], ["3 * 8n", "G#3"], ["2n", "C3"]]);

part.start("4m");
```

#### `at`

`at` let's you set or change values of a part at a given time. 

```javascript
//get the value at the given time
part.at("4n"); //returns "G3"
```

```javascript
//change the first note to a G#
part.at("0", "G#2");
```

### Tone.Sequence

Tone.Sequence extends Tone.Part and simplifies the notation of composing sequential events. Pass in an array of evenly-spaced events at a given subdivision like so:

```javascript
//a series of 8th notes
var seq = new Tone.Sequence(callback, ["C3", "Eb3", "F4", "Bb4"], "8n");
```

Nested arrays will subdivide that index by the length of the subarray and `null` is a rest

```javascript
//a dotted quarter-note followed by an 8th note triplet
var seq = new Tone.Sequence(function(time, note){
	//play the note
}, ["C3", [null, "Eb3"], ["F4", "Bb4", "C5"]], "4n");
```

Sequences are set to loop by default at whatever the length of the events array is. 

##### `at`

`at` works similarly to Tone.Part, but takes an index as the time value instead of the time. 

```javascript
seq.at(0); //returns "C3"
seq.at(1); //returns a Tone.Sequence
```

### Tone.Pattern

Tone.Pattern let's you easily create different kinds of arpeggios melodies. It takes a callback, an array of values and a pattern name in the constructor.

```javascript
//cycle up and then down the array of values
var arp = new Tone.Pattern(callback, ["C3", "E3", "G3"], "upDown");
//callback order: "C3", "E3", "G3", "E3", ...repeat

arp.pattern = "downUp";
//callback order: "G3", "E3", "C3", "E3", ...repeat
``` 