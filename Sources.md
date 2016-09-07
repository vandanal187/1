#### [Tone.Oscillator](https://tonejs.github.io/docs/#Oscillator)

A wrapper around the native OscillatorNode which simplifies starting and stopping and includes additional parameters such as phase rotation.

```javascript
//a square wave at 440hz
var osc = new Tone.Oscillator(440, "square")
	.toMaster() //connected to the master output
	.start(); // start it right away
```

Tone.Oscillator also includes modifiers on the default oscillator types. Set the type to `"square4"` to hear the first 4 partials of the square wave, or `"triangle9"` for the first 9 partials of the triangle wave. 

#### [Tone.Player](https://tonejs.github.io/docs/#Player)

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

If you don't care about individual load events, bind a function to `Tone.Buffer.on('load', callback)` to receive a callback when all of the buffers are fully loaded for Tone.Player, Tone.Convolver, and Tone.Sampler, etc. 

```javascript
Tone.Buffer.on('load', function(){
	//all buffers are loaded.	
})
```

#### [Tone.PulseOscillator](https://tonejs.github.io/docs/#PulseOscillator)

A pulse wave is like a square wave, but instead of having a duty-cycle which is 50% up and 50% down, the pulse oscillator lets you set the `width` of the oscillator. A width of 10% (`pulse.width.value = 0.1`) would produce a wave which is up 10% of the time and down 90% of the time. A width of 90% would sound identical to a wave at 10%, but be in the opposite phase. 

#### [Tone.PWMOscillator](https://tonejs.github.io/docs/#PWMOscillator)

The pulse width modulation oscillator varies the width of the PulseOscillator with another wave. It has an additional control over the `modulationWidth`. 

#### [Tone.FMOscillator](https://tonejs.github.io/docs/#FMOscillator)

Composed of one oscillator modulating the frequency of a second oscillator. This technique can give you many interesting harmonics.

#### [Tone.AMOscillator](https://tonejs.github.io/docs/#AMOscillator)

Composed of one oscillator modulating the amplitude of a second oscillator. 

#### [Tone.FatOscillator](https://tonejs.github.io/docs/#FatOscillator)

A fat oscillator is an abstraction around multiple, slightly detuned oscillators. 

#### [Tone.Noise](https://tonejs.github.io/docs/#Noise)

Noise outputs a looped random buffer with 3 different noise colors: white, pink, and brown. See [this](https://tonejs.github.io/examples/noises.html) example for what those different types of noise sound like. 

#### [Tone.OmniOscillator](https://tonejs.github.io/docs/#OmniOscillator)

Tone.OmniOscillator encompasses Tone.Oscillator, Tone.PWMOscillator and Tone.PulseOscillator which allows you to set it to be "sine", "square", "triangle", "sawtooth", "pwm", or "pulse". 

When the type is set to "pwm" it has an additional control over the `modulationFrequency` and when it's set to "pulse" it exposes a `width` attribute. Trying to set these attributes when the oscillator type is not set correctly will cause an error. 
