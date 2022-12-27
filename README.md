
<p align="center"><img width="100" height="100" src="https://i.imgur.com/6QGo4Zn.jpg"/></p>

[![GitHub license](https://img.shields.io/github/license/ineventapp/musjs.svg)](https://github.com/ineventapp/musjs/blob/master/LICENSE)
![Coverage](https://img.shields.io/badge/coverage-100%25-brightgreen.svg)

# mus.js
A simple mouse tracking library to provide insights on how your users are handling your layout / user experience.

This library was created so you don't need an external service to "record" your users mouse events and "play" them in a later moment.

**mus** works with any AMD you wish and its setup is extremely simple - **5.6kb**

## Fork

This fork has made a number of changes to suit my own purposes:

* Removes tracking of input/form elements
* Removes playback speed setting; plays at natural speed
* Track when the mouse is down 
* Able to set target window to track (e.g. iframe on same domain)
* Able to cue playback from a time (in milliseconds)
* Optional callback after frames advance
* Records scroll-offset during clicks to avoid drift during playback
* Add play-only code + example

## Recording
```js
// Instantiate a mus object with optional parameters
// target = window object to track
// onupdate = callback to fire after each frame
var mus = new Mus({
  target: document.querySelector("iframe").contentWindow,
  onupdate: updateTimer
});

// Start recording
mus.record();

// After a while, stops
setTimeout(function() {
  mus.stop();
}, 5000);
```

## Playing
```js
// Starts playing from start
mus.play();

// Starts playing from 1.5 seconds on
mus.cue(1500);
```


## Public methods

### Controls

#### record()
Starts a recording session for current screen. If there is already a session recorded, it appends to it.

#### stop()
Stops a recording or a playback.

#### play(onfinish)
Plays current recording session from the start

#### cue(ms, onfinish)
Plays the current recording session starting at `ms` milliseconds

#### pause()
Pauses current playback.

#### release()
Releases all data recorded or set.


### Getters and setters

#### ms
property to `get` or `set` time timestamp in milliseconds, which in turn sets the current frame. Does not begin playback.

#### getData()
Returns all data collected during recording.

#### setData(data)
Sets custom data for playback. It must be a JSON object collected from `getData`.

#### setFrames(frames)
Same as `setData`, but allows only to set the `frames` array.

#### setWindowSize(width, height)
During recording, all data collected contains window dimensions as well, so if your recorded data comes from a different window dimension, **mus** automatically adapts to current window size. This function allows you to set a custom playback window size if you decide to use `setFrames` instead of `setData` (that already sets windows dimensions).

#### isRecording()
Informs if **mus** is currently recording something.

#### isPlaying()
Informs if **mus** is currently playing something.

#### timeElapsed(in_ms)
Length of entire recording in seconds (or in milliseconds if `in_ms` is `true`); difference in time between when recording started and stopped.

# Version history

## v1.5.0
- Forked and modded;

## v1.1.0
- Added time point recording for precise data;

## v1.0.1
- Added minified file for distribution;

# License
MIT
