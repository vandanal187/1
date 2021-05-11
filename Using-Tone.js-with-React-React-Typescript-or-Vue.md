This is a place to add any gotcha's and tips for people combining Tone.js with React or Vue. 

## Basic example in vanilla JS, React, and Vue

### Vanilla Javascript ([demo](https://codesandbox.io/s/tone-sampler-example-4pm72))
```js
import { Sampler } from "tone";

const sampler = new Sampler(
  {
    A1: "A1.mp3"
  },
  {
    onload: () => {
      document.querySelector("button").removeAttribute("disabled");
    }
  }
).toMaster();

document.querySelector("button").addEventListener("click", () => {
  sampler.triggerAttack("A2");
});

```

## The same component in React ([demo](https://codesandbox.io/s/tone-sampler-example-ykd53))
```js
import React from "react";
import ReactDOM from "react-dom";
import { Sampler } from "tone";
import A1 from "../A1.mp3";

export default class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isLoaded: false };
    this.handleClick = this.handleClick.bind(this);

    this.sampler = new Sampler(
      { A1 },
      {
        onload: () => {
          this.setState({ isLoaded: true });
        }
      }
    ).toMaster();
  }

  handleClick() {
    this.sampler.triggerAttack("A1");
  }

  render() {
    const { isLoaded } = this.state;
    return (
      <div>
        <button disabled={!isLoaded} onClick={this.handleClick}>
          start
        </button>
      </div>
    );
  }
}

ReactDOM.render(<App />, document.getElementById("app"));
```

## The React component using Hooks ([Demo](https://codesandbox.io/s/tone-sampler-example-sjohx))
```js
import React, { useState, useRef, useEffect } from "react";
import ReactDOM from "react-dom";
import { Sampler } from "tone";
import A1 from "../A1.mp3";

export const App = () => {
  const [isLoaded, setLoaded] = useState(false);
  const sampler = useRef(null);

  useEffect(() => {
    sampler.current = new Sampler(
      { A1 },
      {
        onload: () => {
          setLoaded(true);
        }
      }
    ).toMaster();
  }, []);

  const handleClick = () => sampler.current.triggerAttack("A1");

  return (
    <div>
      <button disabled={!isLoaded} onClick={handleClick}>
        start
      </button>
    </div>
  );
};

ReactDOM.render(<App />, document.getElementById("app"));
```

## The Same Example Using Vue Components ([Demo](https://codesandbox.io/s/tonejs-vue-example-wo3qr))
```js
import { Sampler } from "tone";
import A1 from "./A1.mp3";
import Vue from "vue";

new Vue({
  el: "#app",
  template: `
  <div id="app">
    <button :disabled="!isLoaded" @click="handleClick">
      start
    </button>
  </div>`,
  data: {
    isLoaded: false
  },
  created() {
    this.sampler = new Sampler(
      { A1 },
      {
        onload: () => {
          this.isLoaded = true;
        }
      }
    ).toMaster();
  },
  methods: {
    handleClick() {
      this.sampler.triggerAttack("A1");
    }
  }
});
```

---

## React + Typescript Caveats (typing hooks or components with Typescript, [Demo](https://codesandbox.io/s/reacttypescripttonejs-b6ibv?file=/src/useOscillator.ts)):

The issue: Sometimes we want to abstract the logic of a ToneJS class in React hooks or React Components, and maybe our intuition tells us to do this:

```typescript
// useOscillator.ts
import { useRef } from "react";
import { Oscillator } from "tone";

export default function useOscillator(
  options
): Oscillator {
  const oscillator = useRef<Oscillator>(
    new Oscillator(options).toDestination()
  );

  return oscillator.current;
}

// Oscillator.tsx
function Oscillator({ options, ...props }) {
  const oscillator = useOscillator(options);
  return (
    /* UI logic here */
  );
}
```

In this case, it's clear that we want to use options as something we pass directly to our `ToneJS` instance. Typescript should infer our types and we will have a nice developer experience.

However, if we check the type of options in this example, we will see that it's inferred to be `any`...

_Why does this happen?_

There {s small caveat regarding the [`Oscillator` class constructor]("https://github.com/Tonejs/Tone.js/blob/053b5d4397b595ea804b5d6baf6108158c8e0696/Tone/source/oscillator/Oscillator.ts#L73") (here's the exact lines copied):

```typescript
constructor(frequency?: Frequency, type?: ToneOscillatorType);
constructor(options?: Partial<ToneOscillatorConstructorOptions>)
constructor()
```

The constructor has 3 overload cases with different types, typescript can't infer the type :cry:. The Typescript handbook doesn't recommend this pattern, but this change would imply a huge change in the codebase of `ToneJS` and retro-compatibility, so that can't be changed.

The question we end up with is: **_How do we type this?_**

First instinct is to try typing it with the type we wish to use (in this case `Partial<ToneOscillatorConstructorOptions>` from "tone/Tone/source/Oscillator/OscillatorInterface"). However this will raise an error, the type clashes with other overload types.

We **need** to type this according to the overload we are using. Typescript has a handy helper for this: `ConstructorParameters<T>`. We simply need to use it: `ConstructorParameters<typeof Oscillator>`. This returns a `Tuple`, with a single element (The only constructor that has a single element as `options`), so we must access it:

```typescript
type Options = ConstructorParameters<typeof Oscillator>[0];
```

Now we can type everything safely in our app :smile: :
```typescript
import { useRef } from "react";contain it
import { Oscillator } from "tone";

type Options = ConstructorParameters<typeof Oscillator>[0];

export default function useOscillator(
  options: Options
): Oscillator {
  const oscillator = useRef<Oscillator>(
    new Oscillator(
      options as Options
    ).toDestination()
  );

  return oscillator.current;
}

// Oscillator.tsx
type Props = {
  options: Options;
  /* Other types */
}

function Oscillator({ options, ...props }) {
  const oscillator = useOscillator(options);
  return (
    /* UI logic here */
  );
}
```

## References

* [React + TypeScript Cheatsheets](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet)