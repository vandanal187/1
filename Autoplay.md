Autoplay is the source of a lot of weird Tone.js bugs, but luckily the fix is quite simple

## Solution

Make sure that you don't start the Transport or play any sounds until the page receives a user gesture (e.g. a button click). Tone.js has a `start` method which will kick off the audio for your page. 

```javascript
document.querySelector('button').addEventListener('click', async () => {
    await Tone.start()
    // your page is ready to play sounds
})
```

## Problem

Pretty much all browsers won't play any sound on page load anymore. This is known as _autoplay_. There's a little more background [here](https://developers.google.com/web/updates/2017/09/autoplay-policy-changes). Basically the AudioContext (which is responsible for rendering audio in the Web Audio API), starts out as `"suspended"`. 

You can check verify this for your page:

```javascript
// before a user gesture
Tone.context.state === "suspended"
```

Only after a user gesture in which the user creates a sound or invokes `Tone.start()` will the AudioContext change its state to `"running"`. 

```javascript
// after Tone.start() is invoked from a user gesture
Tone.context.state === "running"
```

The way that autoplay is handled can be pretty inconsistent and what counts as a user gesture might be different for different platforms or situations. The most reliable solution is to invoke `Tone.start()` after a button click.

## Background

The purpose of the Autoplay policy is to stop pages from making a sound as soon as it loads. The intention is to give users greater playback control and a good user experience where pages aren't making unwanted sounds at them before they give permission. This has been the case for mobile browsers for quite a while. And in the past few years, desktop browsers have adopted stricter autoplay as well. 

