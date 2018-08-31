# Basic Synthesis

We can make a basic synthesizer out of an oscillator and an envelope. 

## Oscillator

As our oscillator source, let's use an [OmniOscillator](https://tonejs.github.io/docs/#OmniOscillator). 

```
var osc = new Tone.OmniOscillator();
```

Once we're able to (a) set the oscillator's frequency to a desired note, and (b) specify start and stop times, we have a crude synthesizer... 

```
osc.frequency.value = "C4";
osc.start().stop("+8n");
```

But without further refinement, our synthesizer would have limited flexibility in terms of timbre and dynamics. Also, in its current state, it would emit an unpleasant "click" each time a note is triggered. 

## Envelope

We can get rid of the "click" (an artifact of the discontinuity resulting from instantaneously jumping from an amplitude of zero to full) by smoothing the onset of the sound.  To do this we apply an envelope to the oscillator's amplitude using [Tone.AmplitudeEnvelope](https://tonejs.github.io/docs/#AmplitudeEnvelope).

Below we connect the oscillator to our newly created envelope, then route the envelope out directly to the master. 

```
var env = new Tone.AmplitudeEnvelope();
osc.connect(env);
env.toMaster();
```

Upon starting the oscillator, no sound will be allowed thru until the envelope's Attack stage is triggered. (Note that the oscillator's signal is immediately made available to the envelope when start()'ed, but is suppressed until the Attack starts, then again after the Release stage completes.)

```
osc.start();
env.triggerAttack();
```

Read more about using envelopes [here](https://github.com/Tonejs/Tone.js/wiki/Envelope).

## Tone.Synth

[Tone.Synth](https://tonejs.github.io/docs/#Synth) combines an OmniOscillator and an AmplitudeEnvelope just like we did above, into a convenient package. 

### Portamento

SimpleSynth also exposes a portamento value. Portamento is the amount of time it takes to slide from one frequency to the next.

Play around with all of SimpleSynth's attributes [here](https://tonejs.github.io/examples/simpleSynth.html).