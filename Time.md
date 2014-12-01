# Tone.Time

Tone.Time is a representation of time which all time-related methods accept. Below are some examples of the various forms Tone.Time can take. 

### Numbers

A number will be evaluated as the time (in seconds). 

* `1.2` = 1.2 seconds
* `"3"` = 3 seconds

### Notation

Describes time in BPM and time signature relative values. 

* `"4n"` = quarter note
* `"8t"` = eighth note triplet
* `"2m"` = two measures

### Transport Time

Tempo and time signature relative time in the form BARS:QUARTERS:SIXTEENTHS.

* `"32:0:0"` = start of the 32nd measure. 
* `"4:3:2"` = 4 bars + 3 quarter notes + 2 sixteenth notes. 
* `"1:2"` =  1 bar + 2 quarter notes (sixteenth notes can be omitted)

### Frequency

Seconds can also be described in Hz. 

* `"1hz"` = 1 second
* `"5hz"` = 0.2 seconds

### Now-Relative 

Prefix any of the above with "+" and it will be interpreted as "the current time plus whatever expression follows"

* `"+1m"` = 1 measure from now
* `"+0.5"` = half a second from now

### Expressions

Any of the above can also be combined into a mathematical expression which will be evaluated to compute the desired time.

* `"3:0 + 2 - (1m / 7)"` = 3 measures + 2 seconds - a 7th note
* `"+1m + 0.002"` = the current time + 1 measure and 2 milliseconds. 

### No Argument

Methods which accept time, no argument (`undefined`) will be interpreted as "now" (i.e. the `audioContext.currentTime`). 

For example, Tone.MonoSynth's `triggerAttack` method will accept a time as the second argument, or if a time is ommitted, the it will default to "now".

```javascript
synth.triggerAttack();//context.currentTime
synth.triggerRelease("+4n"); //a quarter-note from now
```

