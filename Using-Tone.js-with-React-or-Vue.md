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

## The React component using Hooks ([Demo](https://codesandbox.io/s/tone-sampler-example-3j9tm))
```js
import React, { useState, useRef } from "react";
import ReactDOM from "react-dom";
import { Sampler } from "tone";
import A1 from "../A1.mp3";

export const App = () => {
  const [isLoaded, setLoaded] = useState(false);
  const sampler = useRef(
    new Sampler(
      { A1 },
      {
        onload: () => {
          setLoaded(true);
        }
      }
    ).toMaster()
  );

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

## References

* [React + TypeScript Cheatsheets](https://github.com/typescript-cheatsheets/react-typescript-cheatsheet)