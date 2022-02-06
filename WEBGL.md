# WEBGL
* https://github.com/processing/p5.js/wiki/Getting-started-with-WebGL-in-p5

* `createCanvas(400, 400, WEBGL)`
* `createGraphics(400, 400, WEBGL)`
* OpenGL, hardware accelerated graphics library, three.js, etc...

```js
function setup() {
  createCanvas(400, 400, WEBGL);
}
function draw() {
  background(50);
  rotateX(frameCount * 0.01);
  rotateY(frameCount * 0.01);
  box(100);
}
```

```js
function setup() {
  createCanvas(400, 400, WEBGL);
}
function draw() {
  background(50);
  translate(mouseX - width/2, mouseY - height/2)
  rotateX(frameCount * 0.01);
  rotateY(frameCount * 0.01);
  box(100);
}
```
## 3D GEOMETRIES
* https://p5js.org/examples/3d-geometries.html
* loadModel() - (.obj, etc...)
* https://free3d.com/3d-models/obj

```js
function setup() {
  createCanvas(710, 400, WEBGL);
}

function draw() {
  background(250);
  rotateY(frameCount * 0.01);

  for (let j = 0; j < 5; j++) {
    push();
    for (let i = 0; i < 80; i++) {
      translate(
        sin(frameCount * 0.001 + j) * 100,
        sin(frameCount * 0.001 + j) * 100,
        i * 0.1
      );
      rotateZ(frameCount * 0.002);
      push();
      sphere(8, 6, 4);
      pop();
    }
    pop();
  }
}
```

## MATERIALS

* basicMaterial() - like a fill()
* normalMaterial() - good for debugging
* ambientMaterial(0, 0, 255) - reflects light - can only reflect the color of the light
* specularMaterial(255) - white specular highlight
## LIGHTING

* ambientLight(0, 0, 255) - shines from/in all directions
* pointLight(0, 255, 0, -200, 0, 0) - shines at a position - R, B, G, X, Y, Z (x y z are pixels)
* directionalLight(0, 255, 0, -200, 0, 0) - shines from/in a direction - R, B, G, X, Y, Z (x y z are -1 to 1)
* mix lights together

## CAMERAS
* camera() - default
* ortho() - orthographic projection
* perspective() - perspective projection
* createCamera() - create a camera
* setCamera() - set the camera
* getCamera() - get the camera
## TEXTURES
* https://p5js.org/reference/#/p5/texture
## SHADERS
* A shader is a small program that runs on the GPU (Graphics Processing Unit), not the CPU (Central Processing Unit). 
* GPUs are faster than CPUs and use parallel processing.
* NVIDIA Video: https://www.youtube.com/watch?v=-P28LKWTzrI
* Shader library https://www.geeks3d.com/shader-library/
### WRITING A SHADER
* Shaders are written in GLSL (OpenGL Shading Language)
* 2 files: `shader.vert` and `shader.frag`
* `.vert` is the vertex shader - the shapes and their positions. This file runs first and passes the vertex positions to the fragment shader.
* `.frag` is the fragment shader - the colors and the pixels
### READING
* https://itp-xstory.github.io/p5js-shaders/#/
* https://thebookofshaders.com/
### CODE

* DEMO: https://editor.p5js.org/louiselessel/sketches/xCPxmXGVE

```js
let theShader;

function preload() {
    theShader = loadShader('shader.vert', 'shader.frag');   
}

function setup() {
    createCanvas(200,200,WEBGL);
    noStroke();
}

function draw() {
  shader(theShader);
  rect(0,0,width,height);
}
```

## 3D
