Tone.js has a 7 pre-built synthesizers.

* [Tone.AMSynth](http://tonejs.org/docs/Tone.AMSynth.html)
* [Tone.DuoSynth](http://tonejs.org/docs/Tone.DuoSynth.html)
* [Tone.FMSynth](http://tonejs.org/docs/Tone.FMSynth.html)
* [Tone.MonoSynth](http://tonejs.org/docs/Tone.MonoSynth.html)
* [Tone.NoiseSynth](http://tonejs.org/docs/Tone.NoiseSynth.html)
* [Tone.PluckSynth](http://tonejs.org/docs/Tone.PluckSynth.html)
* [Tone.Sampler](http://tonejs.org/docs/Tone.Sampler.html)

### Methods

All instruments have the same basic methods for triggering the attack and release of the envelopes. 

#### triggerAttack

`triggerAttack` takes the note value as the first argument. If no time value is passed in for the second argument, the attack will be triggered immediately. The third argument is the velocity of the attack. 

```javascript
//trigger the start of a note.
synth.triggerAttack("C4");
```

#### triggerRelease

After the attack, the note will stay at the `sustain` level until `triggerRelease` is called. 

#### triggerAttackRelease

To schedule an attack and release together, use `triggerAttackRelease`. 

### Presets

Each of the instruments also has a number of presets which can be found in the Tone/instrument/presets folder. These named synthesizer configurations are a starting point for exploring the features of each synthesizer. 

### Tone.PolySynth

Each of these synthesizers' constructors can be fed to the second argument of [Tone.PolySynth](http://tonejs.org/docs/Tone.PolySynth.html) to turn the monophonic voice into a polyphonic synthesizer. 

```javascript
//to make a 4 voice MonoSynth
var synth = new Tone.PolySynth(4, Tone.MonoSynth);
```

To set attributes of all the voices, use the `set` method. 

```javascript
synth.set({
	"envelope" : {
		"attack" : 0.1
	}
});
```

Unlike the rest of the synthesizers, for the PolySynth, the `triggerRelease` method needs to be called with the note you want to release. 