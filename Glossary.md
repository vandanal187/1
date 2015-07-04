# Glossary of Terminology

#### Amplitude

Amplitude is the highest value of a wave. 

#### Audio-Rate

Values that can be automated and scheduled on a single sample level.

see [Sampling Rate](#sampling-rate).

#### Beat

The beat is the basic unit of time, the pulse. A regularly repeating event. 

#### Bar

see [Measure](#measure). 

#### Buffer

A buffer is an array of audio data. Typically values are in the range of +1 to -1. 

#### Bus

A bus is an audio pathway that allows you to move a sound from one part of the mixer to another. [[link](http://audiogeekzine.com/2008/09/understanding-sends-auxes-and-buses/)]. 

#### Callback

A callback is a function that is passed as an argument to other code, which is expected to call back (execute) the argument at some convenient time. [[link](http://en.wikipedia.org/wiki/Callback_%28computer_programming%29)]

#### Compressor

Dynamic range compression or simply compression reduces the volume of loud sounds or amplifies quiet sounds by narrowing or "compressing" an audio signal's dynamic range. 

#### Convolution

Convolution is a process used for simulating the reverberation or effects. It is based on the mathematical convolution operation, and uses a pre-recorded audio sample of the impulse response of the space being modeled. [[link](http://en.wikipedia.org/wiki/Convolution_reverb)]

#### Decibel

A Decibel is a logarithmic ratio between two values. Since we perceive loudness on a logarithmic scale, decibels are a useful quantifier for volume. [[link](http://www.soundonsound.com/sos/1994_articles/feb94/decibels.html)]

#### Dry/Wet Control

"Dry" signal is the unprocessed, "clean" signal, while "wet" signal has effects or processes applied to it. the Dry/Wet knob cross-fades between the two signals. 

#### Envelope

Temporal control over the loudness and spectral content of a sound. [[link](http://en.wikipedia.org/wiki/Synthesizer#ADSR_envelope)]

#### Feedback

Feeding the signal back into itself. For audio effects this is only effective if there is a delay signal in the mix, otherwise it leads to uncontrolled positive feedback. 

#### Filter

Audio Filters amplify or attenuate an incoming signal based on its frequency. Common types are "lowpass" which only let frequencies below the "cutoff" pass through, and highpass which only lets high frequencies pass through. [[link](http://en.wikipedia.org/wiki/Audio_filter)]

#### Gain

Gain is the ratio between the input and the output value of a signal. Volume and gain are related in that gain controls the volume, but volume is about the loudness of an acoustic signal as it's coming out of a speaker, gain a multiplication of any signal. 

#### LFO

An Low Frequency Oscillator (LFO) is any oscillator with a frequency of less than 20 or 30hz. These are often used as control signals to modulate synthesis or effects parameters to produce effects such as vibrato, tremolo and phasing. [[link](http://en.wikipedia.org/wiki/Low-frequency_oscillation)]

#### Mid/Side

Mid/Side processing separates the the 'mid' signal (which comes out of both the left and the right channel) and the 'side' (which only comes out of the the side channels) and effects them separately before being recombined. 

#### Measure

A segment of time corresponding to a specific number of beats (the number of beats is determined by the [time signature](#time-signature). Dividing music into bars provides regular reference points to pinpoint locations within a piece of music.

#### Monophonic

A monophonic synthesizer plays only one note at a time. see [Polyphonic](#polyphonic). 

#### Polyphonic

A polyphonic synthesizer can play multiple notes at once. see [Monophonic](#monophonic). 

#### Ramp

Like an animation tween for audio, a ramp is a smooth interpolation of value over a duration of time. 

#### Sampling Rate

Sampling is the reduction of a continuous analog audio signal to a discrete signal. Typically audio is sampled at over 40,000 times per second as a consequence of the Nyquist Theorem. [[link](http://en.wikipedia.org/wiki/Sampling_%28signal_processing%29#Audio_sampling)]

#### Signal

A signal is an [audio-rate](#audio-rate) value which can be used to carry sound waves or [sample-rate](#sampling-rate) control data. 

#### ScriptProcessorNode

The ScriptProcessorNode (now deprecated) was a Web Audio API standard for doing DSP in Javascript. While extremely powerful, the ScriptProcessorNode incurs a large performance and latency penalty. 

#### Synthesis

Electrical or digital signals which represent sound. 

#### Time Signature

Specifies how many [beats](#beat) are to be contained in each bar. 

#### Transport

The transport refers to the controls over play/pause/stop/rewind in a [Digital Audio Workstation](http://en.wikipedia.org/wiki/Digital_audio_workstation). 