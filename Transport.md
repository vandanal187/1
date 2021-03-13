Tone.Transport is the master timekeeper, allowing for application-wide synchronization of sources, signals and events along a shared timeline. Callbacks scheduled with Tone.Transport will be invoked just before the scheduled time with the **exact** time of the event passed in as the first parameter to the callback. 

Tone.Transport's callbacks pass `time` into the callback because, without the Web Audio API, Javascript timing can be quite imprecise. For example, `setTimeout(callback, 100)` will be invoked _around_ 100 milliseconds later, but many musical applications require sub-millisecond accuracy. The Web Audio API provides sample-accurate scheduling for methods like `start`, `stop` and `setValueAtTime`, so we have to use the precise `time` parameter passed into the callback to schedule methods within the callback. 

Additionally, by abstracting away the Web Audio clock, Tone.Transport lets you think in terms of musical timing. In the Web Audio API, all time values are in terms of the AudioContext's time, which starts at 0 when the page is loaded and counts upward in seconds. With Tone.Transport, you can schedule events in bars and beats without having to convert everything to seconds.


## Basics

```javascript
Tone.Transport.schedule(function(time){
	//time = sample accurate time of the event
}, "1m");
```

The above callback will be invoked each time the Transport reaches the first measure. If the Transport is set to loop, or stopped and restarted, the callback will fire each time it reaches the scheduled position along the timeline. 

The callback won't fire until the Transport is started. 

```
Tone.Transport.start();
```

## Scheduling API

There are three basic methods for timing events with Tone.Transport; `schedule`, `scheduleRepeat` and `scheduleOnce`. All three of these methods return a unique ID which can be used to cancel the callback using `clear`. 

#### `schedule(callback, time)`

`Tone.Transport.schedule` will add a callback event to a specific position along the Transport which will be invoked each time the Transport reaches that position.

```javascript
Tone.Transport.schedule(function(time){
	//invoked when the Transport starts
}, 0);
```

#### `scheduleRepeat(callback, interval, startTime, duration)`

Schedule an event to be invoked at the given interval, starting at `startTime` and for the specified `duration`. If no `startTime` is passed in, the interval will start at the current tick if the Transport is started, or at 0 if the Transport is stopped. If no `duration` is given, 
the callback will repeat infinitely. 

```javascript
//play a note every eighth note starting from the first measure
Tone.Transport.scheduleRepeat(function(time){
	note.triggerAttack(time);
}, "8n", "1m");
```

#### `scheduleOnce(callback, time)`

Schedule an event which will only be invoked once. After the event is invoked, it will be removed. If the given `time` is before the current Transport's position, the event will be invoked immediately. 


#### `clear(eventID)`

Each of the scheduling methods returns a unique ID. This ID can be used to cancel the event using `clear`. 

### Attributes

#### `bpm`

Tempo-relative values (like `"1m"`) are evaluated against the Transport's bpm (beats per minute) value. `Tone.Transport.bpm` is a signal-rate value, which means that it's capable of smooth tempo-curves and automation. All callbacks scheduled with the Transport will adjust their timing to match the new tempo. 

```javascript
//smoothly ramp the tempo to 240 bpm over 4 seconds
Tone.Transport.bpm.rampTo(240, 4);
```


#### `loop`

When `loop` is set to `true`, the Transport will loop between `loopStart` and `loopEnd`. 

#### `timeSignature`

The transport is capable of any time signature, but the value will be reduced to a number over 4. So for example, 4/4 time would be set as just 4, and 6/8 time would be set as 3. 

If an array is given, it will be reduced to just the numerator value over 4 (`[7, 8]` becomes just `3.5`).

#### `swing`

The transport has a `swing` attribute which is a number between 0-1. It controls how laid back the `swingSubdivision`. 

#### `swingSubdivision`

The `swingSubdivision` sets which subdivision to apply the swing to. The default value is `"16n"`. The subdivision can be set to anything less than a quarter note. The downbeat will never be swung. 

# References

[Chris Wilson's great explanation of Web Audio scheduling.](http://www.html5rocks.com/en/tutorials/audio/scheduling/)