`connect` is used to specify how audio data should flow from one node to the next. It's analogous to "connecting a cable" from the output of one thing to the input of another. You will see the method used all over Tone.js and the Web Audio API, so it's important to know what it does and how to use it. 

#### Connections are directional

Signal flows from the output of the connect-er node (aka "source") to the input of the connect-ee ("sink"). For example, this code snippet: `source.connect(sink)` could be visualized like so: `source ---> sink`. 

#### Connections are invisible

The connection is made at a low level within underlying API.  Neither Tone.js nor the Web Audio API explicitly retain connectivity data. Specifically, there is no *query* mechanism enabling you to determine, e.g. "Is A connected to B?".  (Perhaps one could think of it as "write only"). Since connectivity cannot be determined programmatically, if such functionality is desired, it's up to the application to maintain connectivity state in whatever way meets your needs.

But fear not -- it's rarely a necessity.  All kinds interesting things can be built without your code becoming too difficult to reason about by direct inspection.  However, if you're really hard core you might find it interesting to know that more than one ambitious developer has wrapped a Nodal Editor around Tone Nodes and connections, creating a fun and useful "boxes and wires" interface with drag-and-drop functionality. Fun stuff.

#### You can connect different inputs and outputs

For nodes that have multiple inputs or outputs, `connect` can accept two additional arguments: the output number of the connect-er and the input number of the connect-ee. 

To connect the left (0th) output of a splitter node to the right (1st) output of a merger node: `split.connect(merge, 0, 1)`.  

### Convenience methods

Tone.js gives you a few convenience methods for connecting up nodes. 

#### `chain`

Use `chain` to connect a group of nodes in series.

```
source.chain(filter, pan, volume, Tone.Master);
// source->filter->pan->volume->Tone.Master
```

#### `fan`
`fan` connects the output of a node to the inputs of all of the arguments:

```
source.fan(reverb, chorus);
//source->reverb
//source->chorus
```
