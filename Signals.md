[Tone.Signal](https://tonejs.github.io/docs/#Signal) plays an important role in Tone.js by allowing audio-rate control over many attributes. It is similar, but more flexible than the Web Audio API's native [AudioParam](http://webaudio.github.io/web-audio-api/#the-audioparam-interface) and allows sample-accurate control synchronization of a node's attributes.

## Setting values

Unlike other attributes, to get or set the value of a Tone.Signal, you must access it through the `.value`. 

For example, the frequency attribute of Tone.Oscillator is a Tone.Signal:

```javascript
oscillator.frequency.value; //returns the current frequency value
oscillator.frequency.value = 100; //sets the value immediately
```

`.value` has to be used because Tone.Signal is not merely a number, but an audio-rate signal meaning it outputs a value on every sample and is also capable of sample-accurate automations. 

## Scheduling values

A very important feature of Tone.Signal is that it is sample-accurate. Scheduled changes will occur precisely when they are supposed to. 

Tone.Signal includes all of the same scheduling methods as the `AudioParam`, such as: 

* `setValueAtTime` - to schedule a value change at a precise time.
* `linearRampToValueAtTime` - to ramp to a value starting from the previously scheduled value. 
* `exponentialRampToValueAtTime` - same as the above, but with an exponential curve instead of a linear curve. 
* `setTargetAtTime` - unlike the `RampValueAtTime` methods, in `setTargetAtTime`, the time attribute is when it should start ramping towards the value instead of arrive at the value. It takes a third parameter which is the time constant at which it will change. 
* `setValueCurveAtTime` - sets an array of values which will be evenly invoked over the course of the duration. 
* `cancelScheduledValues` - cancels all values after the specified time. 

Additionally, Tone provides methods for ramping and scheduling values at the current time. These simplify the above methods by canceling all values after the current time and setting an automation point at the current value. 

* `linearRampTo` - set a value and a ramp time and the signal will begin linearly ramping towards that value. 
* `exponentialRampTo` - same as above but exponential ramp. 
* `rampTo` - same interface as the above methods, but will automatically decide to use linear or exponential based on the units of the signal. 
