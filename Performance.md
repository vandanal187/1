This article provides some resources and best practices for working with Web Audio and Tone.js

## Audio Node Performance

Audio failures result in pops, crackles, silence and other unwanted artifacts. Paul Adenot (the author of Firefox's Web Audio implementation) has [a great article](http://padenot.github.io/web-audio-perf/) on the CPU, memory usage and incurred latency of most of the Web Audio nodes. It can be a helpful resource for pinpointing performance bottlenecks. The most processor intensive nodes are the ConvolverNode (Tone.Convolver) and PannerNode using HRTF (Tone.Panner3D). Other than the amount and types of nodes used, Web Audio does not currently offer much in the way of performance configuration and tuning.

## context.latencyHint

If you're using the Transport to schedule events, the amount of time in advance events are scheduled is adjustable. Scheduling events farther in advance is easier on for the audio thread to process and may improve performance.

`Tone.context.latencyHint` can be set to `"interactive"` (_default_, prioritizes low latency), `"playback"` (prioritizes sustained playback), `"balanced"` (balances latency and performance), and `"fastest"` (lowest latency, might glitch more often). Or set it to the number of seconds which events should be scheduled in advance. 

```javascript
Tone.context.latencyHint = 'playback'
```

## Scheduling in advance

As mentioned, it's best to schedule audio events as in advance as possible. For this reason, it's good to invoke `Tone.Transport.start` a little bit in the future. `Tone.Transport.start("+0.1")` will start the Transport 100 milliseconds in the future which is not very perceptible, but can help avoid scheduling errors.

Scheduling further in advance works for triggering playback of sources and synths as well. For example, if you are hearing performance issues when triggering a synth from a `mousedown` callback, try scheduling the sound a little in advance. Values under 0.1 seconds won't be very noticeable, but could help reduce pops. 

```javascript
element.addEventListener('mousedown', function(){
	//instead of scheduling the synth immediately,
	//try scheduling 50ms in the future to avoid performance-related pops
	synth.triggerAttack('C4', '+0.05')
})
```

## Syncing Visuals

If you're using Tone.Transport, it is important that you **do not** make draw calls or DOM manipulations inside of the callback provided by Tone.Transport or any of the classes that extend Tone.Event (Part, Sequence, Pattern, Loop). The callback for Tone.Transport uses a WebWorker, it is not synced to the animation frame. Also, Transport callbacks can occur many more times a second than animation frame callbacks and can be invoked in a background tab. Additionally, Transport events can be invoked well in advance of when the event is heard, so visuals triggered inside of one of these callbacks might not align with the audio event they are triggered with. 

A solution to synchronizing visuals and audio is to use [Tone.Draw](https://tonejs.github.io/docs/#Draw). You can schedule a draw callback from within a Transport callback using the AudioContext time that the event is supposed to occur. Tone.Draw will invoke the callback on the nearest animation frame to the given time. 

```javascript
var loop = new Tone.Loop(function(time){
	//instead of scheduling visuals inside of here
	//schedule a deferred callback with Tone.Draw

	Tone.Draw.schedule(function(){
		//this callback is invoked from a requestAnimationFrame
		//and will be invoked close to AudioContext time

	}, time) //use AudioContext time of the event

}, "8n")
```


## Loading and Decoding AudioBuffers

On memory constrained devices like mobile phones, loading many and/or large audio files can cause the browser to crash during the buffer decoding.

## StartAudioContext

Some browsers require (and it usually makes for a good user experience) to allow the user to initiate starting the audio. [StartAudioContext](https://github.com/tambien/StartAudioContext) plays a silent sound on a user action to ensures that the AudioContext is started. 

To use it with Tone.js, just pass in the Tone.context as the first argument
```javascript
StartAudioContext(Tone.context, 'buttonElement').then(function(){
	//callback is invoked when the AudioContext.state is 'running'
})
```