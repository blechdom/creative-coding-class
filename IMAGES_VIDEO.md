# IMAGES AND VIDEO
* Make sure you are logged-in to the editor
* Open the `Sketch Files` tab (the arrow above the top left corner of the coding window)
* Select `Upload file`
* Drag/Drop media files
## Images
* Image Formats: JPG, GIF, PNG, SVG
* Images can load in the background
* `preload()` event
* `loadImage()` function
```js
function preload() {
    img = loadImage('assets/img/cat.jpg')
}
```

```js
function draw() {
    image(img, 0, 0)
    // image(img, x, y, width, height)
}
```

* `img.width` and `img.height`

## Typography
* accepts `.ttf` and `.otf` files
* dowload from web or use https://fonts.google.com/
* `textFont()`, `loadFont()` and `textSize()`
```js
text('Hello World', x, y, width, height)
```

## More P5.js Concepts
* `push()` and `pop()` are used to save and restore the current drawing state
* `rotate()`, `translate()`, `scale()`, and `shear()` are used to change the current transformation matrix
* `bezier()`, `quadraticVertex()`, and `curveVertex()` are used to draw Bézier curves
* `noLoop()` and `loop()` are used to control whether the `draw()` function continuously executes

## Pixels

* `pixels[]` is an array of the values in the image data
* `loadPixels()` is used to load the pixel data for the image into the `pixels` array
* `updatePixels()` is used to update the image with the data in the `pixels` array
* `get()` and `set()` are used to access and set the individual pixels in the `pixels` array
* `set()` is used to set the color of a single pixel


## live camera

* `video = createCapture(VIDEO)`
* https://editor.p5js.org/codingtrain/sketches/B1L5j8uk4
```js
// Daniel Shiffman
// https://thecodingtrain.com
// https://youtu.be/WCJM9WIoudI
// https://youtu.be/YqVbuMPIRwY
let video;

let x = 0;

function setup() {
  createCanvas(800, 240);
  pixelDensity(1);
  video = createCapture(VIDEO);
  video.size(320, 240);
  background(51);
}

function draw() {
  video.loadPixels();
  let w = video.width;
  let h = video.height;
  copy(video, w/2, 0, 1, h, x, 0, 1, h);
  x = x + 1;
  if (x > width) {
    x = 0;
  }
}
```
### WebCam ASCII

```js
let webCam;

function setup() {
  createCanvas(480, 240);
  pixelDensity(1);
  webCam = createCapture(VIDEO);
  webCam.size(width, height);
  webCam.hide();
  noStroke();
  fill(0);
}

function draw() {
  background(255);
  webCam.loadPixels();
  stepSize = 4
  for (let y = 0; y < height; y+=stepSize) {
    for (let x = 0; x < width; x+=stepSize) {
      const i = (y * width + x) * 4;
      fill(webCam.pixels[i], webCam.pixels[i+1], webCam.pixels[i+2], webCam.pixels[i+3], webCam.pixels[i+4])
      textSize(stepSize*2)
      text(char(webCam.pixels[i]%128), x, y);
    }
  }
}
```