Tone.js also has a few stereo and mono effects some of which also have their own presets. 

* [Tone.AutoPanner](http://tonejs.org/docs/Tone.AutoPanner.html)
* [Tone.AutoWah](http://tonejs.org/docs/Tone.AutoWah.html)
* [Tone.BitCrusher](http://tonejs.org/docs/Tone.BitCrusher.html)
* [Tone.Chebyshev](http://tonejs.org/docs/Tone.Chebyshev.html)
* [Tone.Chorus](http://tonejs.org/docs/Tone.Chorus.html)
* [Tone.Convolver](http://tonejs.org/docs/Tone.Convolver.html)
* [Tone.Distortion](http://tonejs.org/docs/Tone.Distortion.html)
* [Tone.FeedbackDelay](http://tonejs.org/docs/Tone.FeedbackDelay.html)
* [Tone.Freeverb](http://tonejs.org/docs/Tone.Freeverb.html)
* [Tone.JCReverb](http://tonejs.org/docs/Tone.JCReverb.html)
* [Tone.Phaser](http://tonejs.org/docs/Tone.Phaser.html)
* [Tone.PingPongDelay](http://tonejs.org/docs/Tone.PingPongDelay.html)
* [Tone.StereoWidener](http://tonejs.org/docs/Tone.StereoWidener.html)

### dry/wet

All Effects have a dry/wet control called `wet` which controls how much of the effected ("wet") signal is output compared to the uneffected ("dry") signal. The default value for the effects is 100% wet. 

```javascript
// 50/50 mix
effect.wet.value = 0.5;
//fade to 100% wet over 3 seconds.
effect.wet.rampTo(1, 3);
```