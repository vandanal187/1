# A Basic Arpeggiator

In this example, we'll create an arpeggiator which plays the next note in a series on every beat. 

## The Synthesizer

Tone.js has a number of instruments, each with nearly the same interface for triggering attacks and releases. Here we'll use [Tone.Synth](https://tonejs.github.io/docs/Synth), but you can easily swap the SimpleSynth for any of the other instruments without changing any other code.

```javascript
var synth = new Tone.Synth();
```

We'll also connect our synth to the [Destination](https://tonejs.github.io/docs/Destination) (formerly known as Master) so that we can hear it.

```javascript
synth.toDestination();
```

## Triggering Notes

We can trigger the synth to start the attack portion of the note using `triggerAttack` -- this method takes a note and a time as arguments. To start the release portion of the note, call `triggerRelease`. Read more about using envelopes [here](https://github.com/Tonejs/Tone.js/wiki/Envelope).

Let's trigger the note `"C4"` then trigger the release a quarter second later (all values are in seconds):

```javascript
synth.triggerAttack("C4", time);
synth.triggerRelease(time + 0.25);
```

These two methods are combined into a single call to `triggerAttackRelease` which takes the note as the first argument, the duration as the second, and the start time as the third argument. 

```javascript
synth.triggerAttackRelease("C4", 0.25, time);
```

## The Arpeggio

Next let's pick a set of notes to arpeggiate over, like a C pentatonic scale. We'll set an interval and get the next note from the array on every loop. If the last argument of `triggerAttackRelease` is omitted, it defaults to the current time.

```javascript
var pattern = new Tone.Pattern(function(time, note){
	synth.triggerAttackRelease(note, 0.25);
}, ["C4", "D4", "E4", "G4", "A4"]);
```

[Tone.Pattern](https://tonejs.github.io/docs/#Pattern) will arpeggiate over the given array in a number of different ways (`"up"`, `"down"`, `"upDown"`, `"downUp"`, `"random"` and more). By default the pattern will iterate upward and then loop back to the beginning. 

As with all [Event classes](https://github.com/Tonejs/Tone.js/wiki/Events), `time` is passed in as the first argument. This is very important because native Javascript timing is pretty loose. Callbacks scheduled with `setInterval` for example, will happen _around_ the given time, but there is no guarantee on precision; that's not good enough for musical events. 

The last thing to do is to start the pattern from the beginning of the Transport timeline. 

```javascript
// begin at the beginning
pattern.start(0);
```

And start the Transport to get the clock going.

```javascript
Tone.Transport.start();
```