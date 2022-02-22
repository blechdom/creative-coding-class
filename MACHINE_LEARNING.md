# ML5.js
* ML5 is a javaScript library for machine learning in p5.js.
* Built on TensorFlow.js, which is build on TensorFlow (open source from Google) 
* TensorFlow.js is javaScript library, while TensorFlow is a python library, but c++ under the hood
## Anatomy
* Algorithms: Neural Networks
* Models: pre-trained
  * MobileNet - Image Classification
  * prediction
* data sets
* ml5.js library include script:

`<script src="https://unpkg.com/ml5@latest/dist/ml5.min.js"></script>`

### Image Classification
```js
// Initialize the Image Classifier method with MobileNet. A callback needs to be passed.
let classifier;

// A variable to hold the image we want to classify
let img;

function preload() {
  classifier = ml5.imageClassifier('MobileNet');
  img = loadImage('images/bird.jpg');
}

function setup() {
  createCanvas(400, 400);
  classifier.classify(img, gotResult);
  image(img, 0, 0);
}

// A function to run when we get any errors and the results
function gotResult(error, results) {
  // Display error in the console
  if (error) {
    console.error(error);
  }
  // The results are in an array ordered by confidence.
  console.log(results);
  createDiv(`Label: ${results[0].label}`);
  createDiv(`Confidence: ${nf(results[0].confidence, 0, 2)}`);
}
```

* https://editor.p5js.org/blechdom/sketches/Py-Gded5mP

```js
let classifier;
let imageCounter = 0

let imagePaths = [
  'https://res.cloudinary.com/dk-find-out/image/upload/q_80,c_limit,h_840,w_1240,f_auto/GettyImages_150644751_qknq07.png',
  'images/bigbird.png',
  'images/car.png',
  'https://res.cloudinary.com/dk-find-out/image/upload/q_80,w_960,f_auto/DCTM_Penguin_UK_DK_AL502808_sqrep1.png',
  'https://res.cloudinary.com/dk-find-out/image/upload/q_80,w_960,f_auto/A-dreamstime_xxl_13809428_fwsxfo.png', 'https://www.google.com/search/static/gs/animal/cover_images/m03k3r_cover.png',
  'images/tree.png',
  'images/carrots.png',
  'images/supercat.png'
]

let images = []

function preload() {
  classifier = ml5.imageClassifier('MobileNet');
  for (let i=0; i<imagePaths.length; i++){
     images[i] = loadImage(imagePaths[i]);
  }
 
}

function setup() {
  createCanvas(400, 400);
  classifyImage()
}

function classifyImage(){
  classifier.classify(images[imageCounter], gotResult);
}

function gotResult(error, results) {
  images[imageCounter].resize(width, 0);
  image(images[imageCounter], 0, 0);
  if (error) {
    console.error(error);
  }
  console.log(`Label: ${results[0].label}`);
  console.log(`Confidence: ${nf(results[0].confidence, 0, 2)}`);
  setTimeout(function(){
    strokeWeight(3)
    stroke(random(255), random(255), random(255))
    fill(random(255), random(255), random(255))
    textSize(50)
    text(results[0].label.split(',')[0], random(width/2) + 0, random(height/2) + 70)
  }, 2000)
  setTimeout(function(){
    imageCounter = imageCounter < imagePaths.length-1 ? imageCounter+1 : 0
    classifyImage()
  }, 5000)
}
```
## Examples
* https://examples.ml5js.org/
* FACE-API https://editor.p5js.org/ml5/sketches/FaceApi_Video_Landmarks
* DOODLENET - https://editor.p5js.org/ml5/sketches/ImageClassification_DoodleNet_Canvas
* VIDEO CLASSIFICATION WITH SPEECH - https://editor.p5js.org/ml5/sketches/ImageClassification_VideoSound
* UNET - AUTO SEGMENTATION - https://editor.p5js.org/ml5/sketches/UNET_webcam
* FACEMESH-WEBCAM https://editor.p5js.org/ml5/sketches/Facemesh_Webcam
* HANDPOSE-WEBCAM https://editor.p5js.org/ml5/sketches/Handpose_Webcam
* PIX2PIX https://editor.p5js.org/ml5/sketches/Pix2Pix_callback