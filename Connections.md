`connect` is how we move audio data from one node to the next. It's analogous to running a cable from the output of one node to the input of another. You will see the method used all over Tone.js and the Web Audio API, so it's important to know what it does and how to use it. 

#### Connections are directional

Signal flows from the output of the connect-er node to the input of the connect-ee. So if you had code that looks like this: `source.connect(sink)`. You can visualize this by drawing a line with an arrow from source to sink: `source->sink`. 

#### Connections are invisible

The connection is made in the underlying API and NOT "remembered" by Tone.js or the Web Audio API in any place. So you can't later query "is A connected to B?". If they are connected, there is no way to tell. It's up to your application to remember it. 

#### `disconnect` disconnects all connected nodes

You can't selectively disconnect a node. If you did something like this: 

```
source.connect(filter); 
source.connect(distortion);
``` 

Then `source.disconnect()` would disconnect both `filter` and `distortion`.

#### You can connect different inputs and outputs

For nodes that have multiple inputs or outputs, `connect` can accept two additional arguments: the output number of the connect-er and the input number of the connect-ee. 

To connect the left (0th) output of a splitter node to the right (1st) output of a merger node: `split.connect(merge, 0, 1)`.  

### Convenience methods

Tone.js gives you a few convenience methods for connecting up nodes. 

#### `chain`

Use `chain` to connect a group of nodes in series.

```
source.chain(filter, pan, volume, Tone.Master);
// source->filter->pan->volume-Tone.Master
```

#### `fan`
`fan` connects the output of a node to the inputs of all of the arguments:

```
source.fan(reverb, chorus);
//source->reverb
//source->chorus
```
