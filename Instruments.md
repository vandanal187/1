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

`triggerAttack` takes the note value as the first argument. If no time value is passed in for the second argument, the attack will be triggered immediately. The third argument is the velocity of the attack. The velocity is a value between 0 and 1 which will scale the envelope's attack and sustain values. 

```javascript
//trigger the start of a note.
synth.triggerAttack("C4");

//trigger the start of a note at `time`
synth.triggerAttack("C4", time);

//trigger the start of a note at `time` with a velocity of 50%
synth.triggerAttack("C4", time, 0.5);
```

#### triggerRelease

After the attack, the note will stay at the `sustain` level until `triggerRelease` is called. 

```javascript
//trigger the release portion of the envelope immediately
synth.triggerRelease();

//trigger the release at `time`
synth.triggerRelease(time);
```

#### triggerAttackRelease

To schedule an attack and release together, use `triggerAttackRelease`. 

```javascript
//trigger "C4" and then 1 second later trigger the release
synth.triggerAttackRelease("C4", 1);
```

### Presets

Each of the instruments also has a number of presets which can be found in the Tone/instrument/presets folder. These named synthesizer configurations are a starting point for exploring the features of each synthesizer. 

### Polyphony with Tone.PolySynth

Each of the synthesizers is monophonic, meaning it can only produce a single note at a time. [Tone.PolySynth](http://tonejs.org/docs/Tone.PolySynth.html) will turn any of the synthesizers into a polyphonic synthesizer by producing multiple copies of a synth and then handling the triggering of attacks and releases on those synth voices. Tone.PolySynth is not a synth by itself, but just a vessel for constructing multiple voices of any of the other synthesizer types.  

The name of the synth is fed to the second argument of Tone.PolySynth to turn the monophonic voice into a polyphonic synthesizer like so: 

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

Unlike the rest of the synthesizers, PolySynth's `triggerRelease` method needs to be called with the note you want to release. 