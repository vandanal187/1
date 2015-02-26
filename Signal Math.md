Signal-rate math operators:

* [Tone.Abs](http://tonejs.org/docs/Tone.Abs.html)
* [Tone.Add](http://tonejs.org/docs/Tone.Add.html)
* [Tone.AudioToGain](http://tonejs.org/docs/Tone.AudioToGain.html)
* [Tone.Clip](http://tonejs.org/docs/Tone.Clip.html)
* [Tone.EqualPowerGain](http://tonejs.org/docs/Tone.EqualPowerGain.html)
* [Tone.Max](http://tonejs.org/docs/Tone.Max.html)
* [Tone.Min](http://tonejs.org/docs/Tone.Min.html)
* [Tone.Modulo](http://tonejs.org/docs/Tone.Modulo.html)
* [Tone.Multiply](http://tonejs.org/docs/Tone.Multiply.html)
* [Tone.Negate](http://tonejs.org/docs/Tone.Negate.html)
* [Tone.Normalize](http://tonejs.org/docs/Tone.Normalize.html)
* [Tone.Pow](http://tonejs.org/docs/Tone.Pow.html)
* [Tone.Scale](http://tonejs.org/docs/Tone.Scale.html)
* [Tone.ScaleExp](http://tonejs.org/docs/Tone.ScaleExp.html)
* [Tone.Subtract](http://tonejs.org/docs/Tone.Subtract.html)
* [Tone.WaveShaper](http://tonejs.org/docs/Tone.WaveShaper.html)

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

