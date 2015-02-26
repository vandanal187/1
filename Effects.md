Tone.js also has a few stereo and mono effects some of which also have their own presets. 

* [Tone.AutoPanner](http://tonenotone.github.io/Tone.js/doc/Tone.AutoPanner.html)
* [Tone.AutoWah](http://tonenotone.github.io/Tone.js/doc/Tone.AutoWah.html)
* [Tone.BitCrusher](http://tonenotone.github.io/Tone.js/doc/Tone.BitCrusher.html)
* [Tone.Chebyshev](http://tonenotone.github.io/Tone.js/doc/Tone.Chebyshev.html)
* [Tone.Chorus](http://tonenotone.github.io/Tone.js/doc/Tone.Chorus.html)
* [Tone.Convolver](http://tonenotone.github.io/Tone.js/doc/Tone.Convolver.html)
* [Tone.Distortion](http://tonenotone.github.io/Tone.js/doc/Tone.Distortion.html)
* [Tone.FeedbackDelay](http://tonenotone.github.io/Tone.js/doc/Tone.FeedbackDelay.html)
* [Tone.Freeverb](http://tonenotone.github.io/Tone.js/doc/Tone.Freeverb.html)
* [Tone.JCReverb](http://tonenotone.github.io/Tone.js/doc/Tone.JCReverb.html)
* [Tone.Phaser](http://tonenotone.github.io/Tone.js/doc/Tone.Phaser.html)
* [Tone.PingPongDelay](http://tonenotone.github.io/Tone.js/doc/Tone.PingPongDelay.html)
* [Tone.StereoWidener](http://tonenotone.github.io/Tone.js/doc/Tone.StereoWidener.html)

### dry/wet

All Effects have a dry/wet control called `wet` which controls how much of the effected ("wet") signal is output compared to the uneffected ("dry") signal. The default value for the effects is 100% wet. 

```javascript
// 50/50 mix
effect.wet.value = 0.5;
//fade to 100% wet over 3 seconds.
effect.wet.rampTo(1, 3);
```