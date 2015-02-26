# Arpeggiator + Effect

In the [previous example](Arpeggiator) we created an arpeggiating synthesizer. Now we'll add an auto filter effect to our synthesizer. An auto filter is a filter with an LFO attached to the frequency attribute which gives it a warbly sound. 

### The Filter

To create our effect we'll first create a [Tone.Filter](http://tonejs.org/docs/Tone.Master.html) and then route the synth signal through the filter. In the previous example, we connected the synth to the master output, but in this example, we are going to connect the synth to the filter and the filter to the master output. 

```javascript
var synth = new Tone.MonoSynth();
var filter = new Tone.Filter();

synth.connect(filter);
filter.toMaster();
```

### Low Frequency Oscillator

Next we'll create an [LFO](http://en.wikipedia.org/wiki/Low-frequency_oscillation) -- Low Frequency Oscillator. Here we'll make an LFO which has a rate of a sixteenth note (`"16n"`) and we'll set the output signal of the LFO to modulate between 100 and 1400. 

```javascript
var lfo = new Tone.LFO("16n", 100, 1400);
```

Making the lfo modulate the filter's frequency is as simple as connecting it to the filter's frequency parameter. 

```javascript
lfo.connect(filter.frequency);
```

Lastly, we'll synchronize the LFO to `Tone.Transport` so that when the Transport is started, as will the LFO. Additionally, when the Transport's tempo is changed, the LFO's modulation frequency will also change. 

```javascript
lfo.sync();
```

### Putting It Together

```javascript
var synth = new Tone.MonoSynth();
var filter = new Tone.Filter();

synth.connect(filter);
filter.toMaster();

var lfo = new Tone.LFO("16n", 100, 1400);
lfo.connect(filter.frequency);
lfo.sync();

var notes = ["C4", "E4", "G4", "A4"];
var position = 0;

Tone.Transport.setInterval(function(time){
	var note = notes[position++];
	position = position % notes.length;
	synth.triggerAttackRelease(note, "8n", time);
}, "4n");

Tone.Transport.start();
```