Tone has multiple types of envelopes for different purposes. Each of the envelopes is an [ADSR](http://en.wikipedia.org/wiki/Synthesizer#ADSR_envelope) and all of the timings use tempo-relative Tone.Time stay synchronized with the tempo even as the bpm changes. 


### Envelope Phases

![ADSR](http://upload.wikimedia.org/wikipedia/commons/e/ea/ADSR_parameter.svg)

The `attack` portion of the envelope makes the output signal transition from 0 to 1 over the duration of the attack time. When the peak value is reached, the envelope will fall to the sustain value. The decay time is given with the `decay` attribute. The envelope will remain at the sustain value, until the release is triggered. The time it takes for the envelope to go from the sustain value back to 0 is given by the `release` time. 

### Types

#### Tone.Envelope

The basic envelope type just outputs a signal in the range of 0-1. This node has only an output and no input. 

`triggerAttack` starts the attack/decay portion of the envelope ending at the sustain value. An optional velocity argument will scale the output value at that number. 

#### Tone.AmplitudeEnvelope

An amplitude envelope is just a Tone.Envelope connect to a GainNode so that audio passed into the input of the envelope will be scaled by the Tone.Envelope.  

#### Tone.ScaledEnvelope

Tone.ScaledEnvelope has a range which starts at `min` and ramps to `max`. The `min` value can be larger than the `max`, it just represents what value the envelope starts at and ramps to. 