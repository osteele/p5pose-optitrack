# P5.JS <-> OptiTrack Starter Kit

This repository uses [p5.js](https://p5js.org) to render data from an [OptiTrack
CSV -> WebSocket server](https://github.com/osteele/optitrack-ws-server).

## Installation

1. Clone this repo.

2. Install [Node.js](https://nodejs.org).
   - On macOS, [install HomeBrew](https://brew.sh), and then enter `brew install node` into a terminal window.
   - On Windows, install it from the [Node.js download page](https://nodejs.org/en/).

3. In a terminal window:
   - Change directories (`cd`) into the repository directory.
   - Enter `npm install`

## Running

In a terminal window:

- Change directories (`cd`) into the repository directory.
- Enter `npm start`

This will open PoseNet in a browser window.

## API

The code in `optitrack.js` provides an API that is very similar to the [ml5.js
PoseNet](https://learn.ml5js.org/docs/#/reference/posenet) API. Code that uses
`ml5.poseNet` can be trivially adapted to render (a projection of) OptiTrack
data instead, or more extensively modified to make use of 3D data.

`const poseNet = optitrack.poseNet(?video, ?options, ?callback);`

### Parameters

* *video*: OPTIONAL. Optional HTMLVideoElement. If present, the x and y
  coordinates from the 3D position are scaled to the dimensions of this element,
  to create the 2D position. (This can any object that provides `width` and
  `height` properties.)

* *callback*: OPTIONAL. A function that is called when the WebSocket connection
  is established.

* *options*: OPTIONAL. An object that contains the following properties. `p5` is
  the global `p5` variable. It is required when p5.js is used in [instance
  mode](https://github.com/processing/p5.js/wiki/Global-and-instance-mode).

  ```json
  {
      p5: p5,
      frameRate: 1,
      serverUrl: 'ws://localhost:8765'
  }
  ```

### Methods

`posenet.on('pose', callback)`

An event listener that returns the results when a pose is detected.

This is upwards-compatible with the ML5's [`posenet.on`
method](https://learn.ml5js.org/docs/#/reference/posenet?id=on39pose39-).

Each keypoint in the array includes both a `position: {x, y}` property (the same
as PoseNet), but also a `pos: {x, y, z}` with the 3D OptiTrack data.

## License

MIT License
