### Time

Time can be encoded in many ways as a String or a Number. 

* Numbers, which will be taken literally as the time (in Seconds)
* Notation, ("4n", "8t") describes time in BPM and time signature relative values.
* TransportTime, ("4:3:2") will also provide tempo and time signature relative times 
in the form BARS:QUARTERS:SIXTEENTHS.
* Frequency, ("8hz") is converted to the length of the cycle in seconds.
* Now-Relative, ("+1") prefix any of the above with "+" and it will be interpreted as 
"the current time plus whatever expression follows".
* Expressions, ("3:0 + 2 - (1m / 7)") any of the above can also be combined 
into a mathematical expression which will be evaluated to compute the desired time.
* No Argument, for methods which accept time, no argument will be interpreted as 
"now" (i.e. the currentTime).

Read more about [Time](https://github.com/Tonejs/Tone.js/wiki/Time).