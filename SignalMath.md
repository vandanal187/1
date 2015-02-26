Signal-rate math operators:

* [Tone.Abs](http://tonenotone.github.io/Tone.js/doc/Tone.Abs.html)
* [Tone.Add](http://tonenotone.github.io/Tone.js/doc/Tone.Add.html)
* [Tone.AudioToGain](http://tonenotone.github.io/Tone.js/doc/Tone.AudioToGain.html)
* [Tone.Clip](http://tonenotone.github.io/Tone.js/doc/Tone.Clip.html)
* [Tone.EqualPowerGain](http://tonenotone.github.io/Tone.js/doc/Tone.EqualPowerGain.html)
* [Tone.Max](http://tonenotone.github.io/Tone.js/doc/Tone.Max.html)
* [Tone.Min](http://tonenotone.github.io/Tone.js/doc/Tone.Min.html)
* [Tone.Modulo](http://tonenotone.github.io/Tone.js/doc/Tone.Modulo.html)
* [Tone.Multiply](http://tonenotone.github.io/Tone.js/doc/Tone.Multiply.html)
* [Tone.Negate](http://tonenotone.github.io/Tone.js/doc/Tone.Negate.html)
* [Tone.Normalize](http://tonenotone.github.io/Tone.js/doc/Tone.Normalize.html)
* [Tone.Pow](http://tonenotone.github.io/Tone.js/doc/Tone.Pow.html)
* [Tone.Scale](http://tonenotone.github.io/Tone.js/doc/Tone.Scale.html)
* [Tone.ScaleExp](http://tonenotone.github.io/Tone.js/doc/Tone.ScaleExp.html)
* [Tone.Subtract](http://tonenotone.github.io/Tone.js/doc/Tone.Subtract.html)
* [Tone.WaveShaper](http://tonenotone.github.io/Tone.js/doc/Tone.WaveShaper.html)

Each of these functions is performed at audio-rate and many also inherit Tone.Signal's scheduling and automation methods to allow value switching with sample-accurate timing. 

#### Tone.Add

Tone.Add can either add together a signal and a number or two signals depending on how it's connected. If instantiated with a number in the constructor, Tone.Add sums together a number and the incoming signal. 

```javascript
var sig = new Tone.Signal(1);
var add = new Tone.Add(1);
sig.connect(add); //the output of add equals 2
```

If Add is constructed with no argument, it will sum the first and second input. 

```javascript
var sig0 = new Tone.Signal(2);
var sig1 = new Tone.Signal(2);
var add = new Tone.Add();
sig0.connect(add, 0, 0);
sig1.connect(add, 0, 1);
//output of add equals 4
```

#### Tone.Multiply

Like Tone.Add, Tone.Multiply accepts either an argument as a number or multiplies the two inputs. If the value is a number, Tone.Multiply can be scheduled just like Tone.Signal. 

```javascript
var sig = new Tone.Signal(3);
var mult = new Tone.Multiply(3);
sig.connect(mult); // output of mult is 9
mult.setValueAtTime(4, "+0.5"); //output is 12 in 0.5 seconds from now
```

