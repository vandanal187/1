Tone has multiple types of envelopes for different purposes. Each of the envelopes is an [ADSR](http://en.wikipedia.org/wiki/Synthesizer#ADSR_envelope) and all of the timings can be set as tempo-relative values which will stay synchronized with the tempo even as the bpm changes. 

#### Tone.Envelope

The basic envelope type just outputs a signal in the range of 0-1. This node has only an output and no input. 

`triggerAttack` starts the attack/decay portion of the envelope ending at the sustain value. An optional velocity argument will scale the output value at that number. 

#### Tone.AmplitudeEnvelope

An amplitude envelope is just a Tone.Envelope connect to a GainNode so that audio passed into the input of the envelope will be scaled by the Tone.Envelope.  

#### Tone.ScaledEnvelope

Tone.ScaledEnvelope has a range which starts at `min` and ramps to `max`. The `min` value can be larger than the `max`, it just represents what value the envelope starts at and ramps to. 