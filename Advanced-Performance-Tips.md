These are some performance related tips I'm compiling, all learned the hard way, as I build a complex DAW on top of Tone.js:

**Playback:**
* Chaining multiple (say 12) instruments through multiple (say 2-5) effects at the same time is too much, even for modern browsers / computers, and will lead to crackles.
  * reducing to ~8 instruments and a few effects here and there is much better right now.
  * I'm still working on improving this and would love some help!
* Even if an effect is not connected to any instrument but is connected `toMaster()`, it can lead to performance issues during playback.
* The high level `Tone.Sequence` is very performant and it is not worth prematurely optimizing your internal sequence loops unless you experience a problem, and even then, I'd advise to start with an inventory of web audio nodes.
* The [Audion Extension](https://github.com/google/audion) is a cool way to graph your nodes. Even a medium sized number of nodes will bring it to its knees fairly quickly, which should tell you something.
  * Note that this extension will not work at all on older versions of Tone.js.

**Animation**
* You can definitely draw an interactive waveform using an analyzer node, change an instrument property, and see the change in the waveform. This performs fairly well (slight crackles occasionally).
  * What will not graph well is accidentally triggering the instrument's `triggerAttackRelease()` many times per second (as you hold down the space bar, for instance). You might not notice from the sound, but you'll see the analyzer not updating as it should be.
