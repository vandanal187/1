Tone has multiple types of envelopes for different purposes. Each of the envelopes implements an [ADSR](http://en.wikipedia.org/wiki/Synthesizer#ADSR_envelope) and all of the timings use tempo-relative Tone.Time stay synchronized with the tempo even as the bpm changes. 

### Envelope Phases

![ADSR](http://upload.wikimedia.org/wikipedia/commons/e/ea/ADSR_parameter.svg)

#### Attack
The `attack` portion of the envelope makes the output signal transition from 0 (min) to 1 (max) over the duration of the attack time.

#### Decay
When the peak value is reached, the envelope will fall to the sustain value over the duration of the decay time. 

#### Sustain
Unlike the other attributes of an ADSR envelope, sustain is not a time, but a percentage of the maximum value of the signal. It is a number between 0 and 1. The envelope will remain at the sustain value, until the release is triggered.

#### Release
The time it takes for the envelope to return from the sustain value back to the minimum value is defined by the `release` time. 

### Example

Play with the parameters of an AmplitudeEnvelope to hear how each of the phases effects the timbre of the input source. 

[example](https://tonejs.github.io/examples/envelope.html)

### Envelope Types

#### [Tone.Envelope](https://tonejs.github.io/docs/#Envelope)

The basic envelope type just outputs a signal in the range of 0-1. This node has only an output and no input. 

`triggerAttack` starts the attack/decay portion of the envelope ending at the sustain value. An optional velocity argument will scale the output value at that number. 

#### [Tone.AmplitudeEnvelope](https://tonejs.github.io/docs/#AmplitudeEnvelope)

An amplitude envelope is just a Tone.Envelope connect to a GainNode so that audio passed into the input of the envelope will be scaled by the Tone.Envelope.  

#### [Tone.ScaledEnvelope](https://tonejs.github.io/docs/#ScaledEnvelope)

Tone.ScaledEnvelope has a range which starts at `min` and ramps to `max`. The `min` value can be larger than the `max`, it just represents what value the envelope starts at and ramps to. 

# Curves

The curve of the attack and release can be controlled by `attackCurve` and `releaseCurve`. These either take a string like "linear", "exponential", "sine", or an array of values to be used as the curve. Below are the curve names and their shapes. 

![curves](https://docs.google.com/drawings/d/1Lrz75eaAaLcS0SpgYih7cDS9GDiJlhRfStIxXfx8qj0/pub?w=642&h=1579)