# Basic Synthesis

We can make a basic synthesizer out of an oscillator and an envelope. 

## Oscillator

As our oscillator source, let's use an [OmniOscillator](https://tonejs.github.io/docs/#OmniOscillator). 

```
var osc = new Tone.OmniOscillator();
```

If we set the frequency of the oscillator to our desired notes, and starting and stopping it, we have a crude synthesizer. 

```
osc.frequency.value = "C4";
osc.start().stop("+8n");
```

We have limited flexibility in terms of the timbre of our synthesizer, and we'll get a harsh click whenever a note is triggered. 

## Envelope

The trick to getting rid of the click is to apply an envelope to amplitude of the oscillator. Tone has a specific envelope type for doing this called [Tone.AmplitudeEnvelope](https://tonejs.github.io/docs/#AmplitudeEnvelope).

Let's connect our oscillator to the envelope and the envelope to the master output. 

```
var env = new Tone.AmplitudeEnvelope();
osc.connect(env);
env.toMaster();
```

Start the oscillator, but there won't be any sound until you trigger the attack of the envelope

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