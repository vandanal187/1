#### [Tone.Oscillator](http://tonejs.org/docs/#Oscillator)

A wrapper around the native OscillatorNode which simplifies starting and stopping and includes additional parameters such as phase rotation.

```javascript
//a square wave at 440hz
var osc = new Tone.Oscillator(440, "square")
	.toMaster() //connected to the master output
	.start(); // start it right away
```

Tone.Oscillator also includes modifiers on the default oscillator types. Set the type to `"square4"` to hear the first 4 partials of the square wave, or `"triangle9"` for the first 9 partials of the triangle wave. 

#### [Tone.Player](http://tonejs.org/docs/#Player)

Tone.Player plays an audio file. 

```javascript
var player = new Tone.Player("./sound.mp3").toMaster();
```

If you need to keep track of individual buffer loading, use the second callback of the constructor. 

```javascript
var player = new Tone.Player("./sound.mp3", function(){
	//the player is now ready	
}).toMaster();
```

If you don't care about individual load events, bind a function to `Tone.Buffer.onload` to receive a callback when all of the buffers are fully loaded for Tone.Player, Tone.Convolver, and Tone.Sampler. 

```javascript
Tone.Buffer.onload = function(){
	//all buffers are loaded.	
};
```

#### [Tone.PulseOscillator](http://tonejs.org/docs/#PulseOscillator)

A pulse wave is like a square wave, but instead of having a duty-cycle which is 50% up and 50% down, the pulse oscillator lets you set the `width` of the oscillator. A width of 10% (`pulse.width.value = 0.1`) would produce a wave which is up 10% of the time and down 90% of the time. A width of 90% would sound identical to a wave at 10%, but be in the opposite phase. 

#### [Tone.PWMOscillator](http://tonejs.org/docs/#PWMOscillator)

The pulse width modulation oscillator varies the width of the PulseOscillator with another wave. It has an additional control over the `modulationWidth`. 

#### [Tone.OmniOscillator](http://tonejs.org/docs/#OmniOscillator)

Tone.OmniOscillator encompasses Tone.Oscillator, Tone.PWMOscillator and Tone.PulseOscillator which allows you to set it to be "sine", "square", "triangle", "sawtooth", "pwm", or "pulse". 

When the type is set to "pwm" it has an additional control over the `modulationFrequency` and when it's set to "pulse" it exposes a `width` attribute. Trying to set these attributes when the oscillator type is not set correctly will cause an error. 
