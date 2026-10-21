# 🪐 Orrery: A Hand-Controlled 3D Solar System

Explore the solar system with nothing but your webcam and your hands. Point at a planet to fly to it, rotate it in 3D, read about it, and even pull it out of the screen to make it float in front of your own camera feed.

**Live demo:** https://yourusername.github.io/orrery-hands/

<!-- Add a screenshot or GIF here: ![Orrery demo](docs/demo.gif) -->

## Features

- **Split-screen layout:** your live camera with a hand-skeleton overlay on the left, the 3D solar system on the right.
- **Full solar system:** the Sun, 8 planets with procedural textures, Saturn's rings, Earth's moon, an asteroid belt, orbit lines and a starfield.
- **Fly to any planet:** the camera glides in, orbits pause, and you can rotate the planet freely.
- **Info panel:** description, diameter, day length, year length, moons, temperature, gravity and a fun fact for every body.
- **Weight calculator:** see what you would weigh on each planet and on the Sun.
- **Float it in your camera:** drag a planet out of the solar system onto your camera view, where it spins and bobs as if it were in your room. Resize it with two hands, and drag it back to put it away.
- **Time controls:** speed up, slow down or pause the orbits.
- **Mouse and touch fallback:** works without a camera too.

## Gesture guide

| Gesture | Action |
|---|---|
| ☝️ Point at a planet and hold (about 0.35 s) | Fly to it |
| 🤏 Pinch empty space and drag | Rotate the view, or the planet when zoomed in |
| 🤏 Pinch a planet and drag it to the left | Float it over your camera |
| 🤏 Drag a floating planet to the right and release | Put it back |
| 🙌 Pinch with both hands, then spread or close | Zoom, or resize a floating planet |
| ✊ Hold a fist | Return to the solar system |
| ✌️ Hold a peace sign | Next planet |
| 🖐 Hold an open palm | Pause or resume time |

## How it works

- **Hand tracking:** [MediaPipe Hand Landmarker](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker) runs fully in your browser (WebAssembly + GPU). No video is uploaded anywhere.
- **3D rendering:** [Three.js](https://threejs.org/) draws the solar system into the right half of the screen using a viewport and scissor, plus a second transparent pass for the floating planet over the camera half.
- **Gestures:** finger-extension and pinch ratios are computed from the 21 hand landmarks and normalised by hand size, with hysteresis and hold timers to avoid false triggers.
- **Textures:** all planet surfaces are generated on the fly with the Canvas API, so there are no image assets.
- **Single file:** the whole app is one `index.html`.

## Run locally

Browsers only allow camera access on `localhost` or HTTPS, so serve the folder instead of double-clicking the file:

```bash
git clone https://github.com/yourusername/orrery-hands.git
cd orrery-hands
python3 -m http.server 8000
```

Then open http://localhost:8000 in Chrome or Edge, click **Start hand control** and allow the camera.

## Deploy

Because it is a static site, GitHub Pages works out of the box: **Settings → Pages → Deploy from a branch → `main` / `(root)`**. Pages serves over HTTPS, so the camera works for everyone who opens the link.

## Project structure

```
orrery-hands/
├── index.html   # the entire app (HTML, CSS, JS)
├── README.md
├── LICENSE
└── .gitignore
```

## Tips for best tracking

- Use good front lighting and keep your hand about 40 to 60 cm from the camera.
- Face your palm toward the camera for fist, peace sign and open palm gestures.
- Chrome or Edge on a laptop or desktop works best.

## Troubleshooting

- **Camera does not start:** use `http://localhost` or an HTTPS link, and check the browser's camera permission.
- **Hand model does not load:** the page needs internet access to fetch the model from Google and the libraries from jsDelivr and cdnjs.
- **Gestures trigger too easily or not enough:** adjust the thresholds and hold times in the `handle()` function.

## Roadmap

- Planet moons and dwarf planets
- Tour mode that visits every planet with narration
- Quiz mode controlled by gestures
- Floating planet that sticks to your palm

## Credits

Built with [Three.js](https://threejs.org/) and [MediaPipe Tasks Vision](https://github.com/google-ai-edge/mediapipe). Planet facts are rounded values from NASA public resources.

## License

MIT. See [LICENSE](LICENSE).
