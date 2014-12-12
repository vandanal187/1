# A Basic Arpeggiator

In this example, we'll create an arpeggiator which plays the next note in a series on every beat. 

### The Synthesizer

Tone.js has a number of instrument, each with nearly the same interface for triggering attacks and releases. Here we'll use [Tone.MonoSynth](http://tonenotone.github.io/Tone.js/doc/Tone.MonoSynth.html), but you can easily swap the MonoSynth for a [DuoSynth](http://tonenotone.github.io/Tone.js/doc/Tone.DuoSynth.html), [FMSynth](http://tonenotone.github.io/Tone.js/doc/Tone.FMSynth.html), or [AMSynth](http://tonenotone.github.io/Tone.js/doc/Tone.AMSynth.html) without changing any of the rest of the code. 

```javascript
var synth = new Tone.MonoSynth();
```

We'll also connect our synth to the [master output](http://tonenotone.github.io/Tone.js/doc/Tone.Master.html) so that we can hear it. 

```javascript
synth.toMaster();
```

### Triggering Notes

We can trigger the synth to start the attack portion of the note using `triggerAttack` -- this method takes a note and a time as arguments. To start the release portion of the note, call `triggerRelease`. Check out [this Wikipedia article](http://en.wikipedia.org/wiki/Synthesizer#ADSR_envelope) for more information about synthesizer envelopes.

For example, let's trigger the note `"C4"` then trigger the release a quarter second later (all values are in seconds):

```javascript
synth.triggerAttack("C4", time);
synth.triggerRelease(time + 0.25);
```

These two methods are combined into a single call to `triggerAttackRelease` which takes the note as the first argument, the duration as the second, and the start time as the third argument. 

```javascript
synth.triggerAttackRelease("C4", 0.25, time);
```

### The Arpeggio

Next let's pick a set of notes to arpeggiate over, like a C pentatonic scale. Then we'll set an interval and get the next note from the array on every loop. 

```javascript
var notes = ["C4", "E4", "G4", "A4"];
var position = 0;

setInterval(function(){
	var note = notes[position++];
	position = position % notes.length;
	synth.triggerAttackRelease(note, 0.25, time);
}, 500);
```

### Timing the Notes

One way to make the arpeggiator loop is with `setInterval` as shown above. The problem is that the timing would be kinda loose since native Javascript timing is not very accurate or reliable. Instead we'll use `Tone.Transport.setInterval` which is defined in [Tone.Transport](http://tonenotone.github.io/Tone.js/doc/Tone.Transport.html). Tone's `setInterval` method looks very similar to Javascript's `setInterval`, except that Tone's method passes in the exact time when the event was scheduled to occur (and also takes its interval time in seconds instead of milliseconds). We'll use that `time` argument to schedule our synth's `triggerAttackRelease` function. 

```javascript
Tone.Transport.setInterval(function(time){
	...
	synth.triggerAttackRelease(note, 0.25, time);
}, 0.5);
```

The transport won't start firing events until it's started. 

```javascript
Tone.Transport.start();
```

### Putting It Together

Here's what it looks like all together:


```javascript
var notes = ["C4", "E4", "G4", "A4"];
var position = 0;

var synth = new Tone.MonoSynth();
synth.toMaster();

Tone.Transport.setInterval(function(time){
	var note = notes[position++];
	position = position % notes.length;
	synth.triggerAttackRelease(note, 0.25, time);
}, 0.5);

//the transport won't start firing events until it's started
Tone.Transport.start();
```

In the [next example](ArpeggiatorEffect), we'll add an effect. 