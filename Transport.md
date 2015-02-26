A unique feature of the library is the oscillator-based Transport which allows for application-wide synchronization of sources and signals. The Transport allows you to register callbacks at precise moments along the timeline which are invoked right before the event with the exact time of the event. Additionally, because the Transport is implemented with an oscillator, it is capable of elaborate tempo curves and automation. 

### Timing Methods

There are three methods for timing events with Tone.Transport. All three methods have the same interface: they take a function and a time and return the ID of the event which was scheduled. The function is invoked just before the time scheduled. Because the timing of the callback is dependent on many factors and might not be very precise, the sample-accurate timing of the event is passed in as the argument to the callback function.

#### Tone.Transport.setInterval

like the native `setInterval`, `Tone.Transport.setInterval` will schedule a repeating event at the interval specified. These events will only be invoked when the Transport is playing. 

```javascript
//this will start the player on every quarter note
Tone.Transport.setInterval(function(time){
	player.start(time);
}, "4n");
//start the Transport for the events to start
Tone.Transport.start();
```

#### Tone.Transport.setTimeout

Set a single event in the future relative to the current Transport position with ```Tone.Transport.setTimeout```

```javascript
//this will start an oscillator 5 seconds from now
Tone.Transport.setTimeout(function(time){
	osc.start(time);
}, 5);
Tone.Transport.start();
```

#### Tone.Transport.setTimeline

`Tone.Transport.setTimeline` will schedule an event relative to the start of the timeline. These events will start, stop and loop with the Transport. 

### Attributes

#### bpm

`bpm` is a Tone.Signal which allows it to be automated and scheduled like any other Tone.Signal. 

```javascript
//set the bpm to 120 right away
Tone.Transport.bpm.value = 120;
//ramp to a bpm of 240 over 5 seconds
Tone.Transport.bpm.rampTo(240, 5);
```

#### loop

When `loop` is set to `true`, the Transport will loop between `loopStart` and `loopEnd`. This will not affect the `setInterval` and `setTimeout` methods, it will only affect `setTimeline`. 

#### timeSignature

The transport is capable of any time signature, but the value must be reduced to a number over 4. So for example, 4/4 time would be set as just 4, and 6/8 time would be set as 3. 

#### swing

The transport has a `swing` attribute which is a number between 0-1. It controls how laid back the `swingSubdivision`. 

#### swingSubdivision

The `swingSubdivision` sets which subdivision to apply the swing to. The default value is `"16n"`, but can be set to anything less than a quarter note. 