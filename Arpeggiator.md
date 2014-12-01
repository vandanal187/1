# Creating an arpeggiator in Tone.js

## The synthesizer

[script](https://raw.githubusercontent.com/TONEnoTONE/Tone.js/master/build/Tone.js), 

Tone.js has a number of instrument, each with the same interface for triggering note attacks and releases. Here we'll use [Tone.MonoSynth]() which is a single [oscillator](Tone.OmniOscillator) run through an [envelope]() and a [filter]() which also has an envelope attached.

To trigger the attack portion of the note, use ```triggerAttack``` with the name of the note. To make the arpeggiator, we'll choose a note from an array of notes and then increment the note position. 

```javascript
var note = notes[position++];
position = position % notes.length;
synth.triggerAttack(note);
```

We can invoke this from within a setTimeout or setInterval, the problem is that the timing would be kind of loose since these timing methods are not very accurate or reliable. Instead we'll use ```Tone.Transport.setInterval``` and the second argument of ```triggerAttack``` to playback the note with sample-accurate timing. Tone's [Transport]() object is the time keeper for events in Tone.js. With it, you can synchronize events along a shared timeline, or schedule single and repeated events. Here we'll use setInterval to schedule a repeated event. 

```javascript
Tone.Transport.setInterval(function(time){
	//...
	synth.triggerAttack(note, time);
	//...
}, 0.25);
```

Unlike the browser's setInterval, Tone's setInterval method takes the time in seconds instead of milliseconds. Alternatively, you can use musical timing to schedule the event. Instead of using 0.25 in the snippet above (which would be the equivalent to an eighth-note at 120 bpm), you could use "8n" and set the Transport's bpm to 120. As an added bonus, the callback timing will stay an eighth-note even as the Transport's bpm changes. 

Now let's make the synth and connect it to the output. Every class in Tone has a ```toMaster``` method which connects the output of the object to the Master output (which is connected to your speakers). 

```javascript
var synth = new Tone.MonoSynth();
synth.toMaster();
```

All that's left is to pick an array of notes and put it all together. 

```javascript
var notes = ["C4", "E4", "G4", "A4"];
var position = 0;

var synth = new Tone.MonoSynth();
synth.toMaster();

Tone.Transport.setInterval(function(time){
	var note = notes[position++];
	position = position % notes.length;
	synth.triggerAttack(note, time);
}, "8n");

//the transport won't start firing events until it's started
Tone.Transport.start();
```

Checkout the working example [here](). 