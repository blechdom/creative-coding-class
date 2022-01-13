# WEBGL
## SHADERS
* A shader is a small program that runs on the GPU (Graphics Processing Unit), not the CPU (Central Processing Unit). 
* GPUs are faster than CPUs and use parallel processing.
* NVIDIA Video: https://www.youtube.com/watch?v=-P28LKWTzrI
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
