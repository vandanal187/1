Tone.js also has a bunch of stereo and mono effects. 

To add an effect to your audio signal, simply connect the effect in between your source and destination. Here is an example which routes a [Tone.SimpleSynth](https://tonejs.github.io/docs/#SimpleSynth) through a [Tone.Distortion](https://tonejs.github.io/docs/#Distortion). 

```javascript
//create an effect and connect it to the master output
var dist = new Tone.Distortion().toMaster();
//create a synth and connect it to the effect
var synth = new Tone.SimpleSynth().connect(dist);
//and play a note to hear the distortion
synth.triggerAttackRelease("C4", "8n");
```

### dry/wet

All effects have a dry/wet control called `wet` which controls how much of the effected ("wet") signal is output compared to the uneffected ("dry") signal. The default value for the effects is 100% wet. 

```javascript
// 50/50 mix
effect.wet.value = 0.5;
//fade to 100% wet over 3 seconds.
effect.wet.rampTo(1, 3);
```