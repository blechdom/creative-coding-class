# ANIMATION & INTERACTION
## Animation
### setup() 
* runs once at the beginning of the program
### draw() 
* runs 60 times per second
## Interaction
### Built-in Variables and functions
#### https://processing.org/reference
* mouseX, mouseY, pmouseX, pmouseY (p is for previous), mouseIsPressed, keyIsPressed, keyCode
```js
    if(mouseIsPressed) {
        line(mouseX, mouseY, pmouseX, pmouseY)
    }
```

* `map(inputVal, inputMin, inputMax, outputMin, outputMax)` - maps a value from one range to another)
* `dist(x1, y1, x2, y2)` - distance between two points

### P5.js Events
#### https://p5js.org/reference/#group-Events

* setup() and draw() are events
* `mousePressed` event
```js
function mousePressed(event) {
    console.log(event)
}
```

### JavaScript Events
### p5.js Constants
https://p5js.org/reference/#group-Constants
* PI, HALF_PI, QUARTER_PI, TWO_PI, TAU, DEGREES, RADIANS 
### Example Code
#### Drawing with Mirrors
```js
let strokeColor = 0;

function setup() {
  createCanvas(400, 400);
  background(220);
}

function draw() {
  noStroke();
  fill(255, 0, 0);
  rect(0, 0, 25, 25);
  
  if (mouseX < 25 && mouseY < 25) {
    fill(0, 255, 0);
    rect(0, 0, 25, 25);
  } else {
    fill(255, 0, 0);
    rect(0, 0, 25, 25);
  }

  stroke(strokeColor);
  if (mouseIsPressed == true) {
    line(mouseX, mouseY, pmouseX, pmouseY);
    line(width - mouseX, mouseY, width - pmouseX, pmouseY);
    line(mouseX, height - mouseY, pmouseX, height - pmouseY);
    line(width - mouseX, height - mouseY, width - pmouseX, height - pmouseY);
  }
  //console.log("mouseX: ", mouseX);
}

function mousePressed(event) {
  if (event.shiftKey) {
    strokeWeight(10);
  } else {
    strokeWeight(1);
  }
  if (mouseX < 25 && mouseY < 25) {
      if(strokeColor== 0) {
        strokeColor = 220
      } else{
        strokeColor = 0
      }
      console.log("stroke color ", strokeColor)
    }
    console.log('color', strokeColor)
}

```
#### Mouse-Controlled Animations
```js
let i = 0;
let backgroundColor = 255

function setup() {
  createCanvas(400, 400);
  
}

function draw() {
  background(backgroundColor);
  noStroke();
  
  let mappedColor = map(mouseX, 0,400, 0, 255)
  
  fill(mappedColor,mouseX%255,mouseY%255)
  circle(width/2, height/2, mouseX)
  
  
  fill(255, 0, 0);
  rect(i%width, height/2, 25, 25);
  i += mouseY/25
  
  

}

function keyPressed() {
backgroundColor = keyCode*2
}

```

### Easing

#### example code
##### Follow the mouse
```js
  function draw() {
    background(255)
    line(x, 0, x, height)

    let easing = 0.5
    let diff = mouseX - x
    x += diff * easing
  }

```

##### Send a shape to the target
```js
let x, y, targetX, targetY = 0

function draw() {
  background(255)
  circle(x, y, 50)

  let easing = 0.125
  let diffX = targetX - x
  let diffY = targetY - y
  x += diffX * easing
  y += diffY * easing
}

function mousePressed(){
  targetX = mouseX
  targetY = mouseY
}

```

### Transformations
* Translate - `translate(x, y)` - redefines the origin point
```js
translate(mouseX, mouseY)
circle(0, 0, 50) // will move the circle to the mouse position
```

* Rotate - `rotate(angle)` - rotates a shape around its _origin point_, default is radians
```js
  rotate(radians(45))
  rect(0, 0, 50, 50) // will rotate the rect 45 degrees
```
* Scale - `scale(x, y)` - scales a shape around its origin point, parameters are percentage values
* Shear - `shearX(angle)` - shears a shape around its x-axis
* Shear - `shearY(angle)` - shears a shape around its y-axis


* `push()` and `pop()` are used to save and restore the current drawing state

### Motion
* sin(angle) - returns the sine of an angle
* cos(angle) - returns the cosine of an angle
* tan(angle) - returns the tangent of an angle
* degrees(angle) - converts an angle from radians to degrees
* radians(angle) - converts an angle from degrees to radians
* acos(x) - returns the arccosine of a number (in radians)
* asin(x) - returns the arcsine of a number (in radians)
* atan(x) - returns the arctangent of a number (in radians)

```js
let angle = 0;
let offset = 60;
let scalar = 40;
let speed = 0.1;

function setup() {
  createCanvas(900, 600)
  fill(0)
}

function draw(){
  background(255)
  
  let y1 = offset + sin(angle) * scalar
  let y2 = offset + sin(angle + 0.4) * scalar
  let y3 = offset + sine(angle + 0.8) * scalar

  ellipse(50, y1, 10, 10)
  ellipse(100, y2, 10, 10)
  ellipse(150, y3, 10, 10)

  angle += speed
}

```

### Timers

* millis() - returns the number of milliseconds since the program started
* second() - returns the number of seconds since the program started
* minute() - returns the number of minutes since the program started
* hour() - returns the number of hours since the program started


```js
let timer = 100
let backgroundColor = 0
let nextTime = timer

function setup() {
  createCanvas(400, 400)
  background(0)
}

function draw() {
  background(backgroundColor)
  if (millis() > nextTime) {
    backgroundColor = random(255)
    nextTime = millis() + timer
  }
}
```

### Patterns

#### 10Print
* https://10print.org/

```js
let x = 0;
let y = 0;
let spacing = 15;

function setup() {
  createCanvas(400, 400);
  background(255);
}

function draw() {
  stroke(0);
  strokeWeight(2)
  if (random(1) < 0.5) {
    line(x, y, x + spacing, y + spacing);
  } else {
    line(x, y + spacing, x + spacing, y);
  }
  x = x + spacing;
  if (x > width) {
    x = 0;
    y = y + spacing;
  }
}
```

```js
let angle = 0.0;
let speed = 0.05

function setup() {
  createCanvas(windowWidth, windowHeight);
  fill(0)
  strokeWeight(1)
}

function draw() {
  
  let arm1 = map(mouseX, 0, width, 10, 200)
  let arm2 = map(mouseY, 0, height, 10, 200)
  let arm3 = map(mouseX+mouseY, 0, width+height, 10, 200)
  background(255)
  translate(width/2, height/2)
  rotate(angle)  //radians
  line(0, 0, 0, arm1)

  translate(0, arm1)
  rotate(angle)
  line(0, 0, 0, arm2)

  translate(0, arm2)
  rotate(angle)
  line(0, 0, 0, arm3)

  angle += speed
}
```


```js
let angle = 0.0;

function setup() {
  createCanvas(windowWidth, windowHeight);
  fill(0)
  strokeWeight(1)
  frameRate(25)
}

function draw() {
  let speed = map(mouseY, 0, height, 0, 0.2)
  let arm1 = map(mouseX, 0, width, 10, 400)
  background(255)
  push()
  stroke(random(255),random(255),random(255))
  translate(width/2, height/2)
  for(let i=0; i<100; i++){
    extendArm(arm1, angle)
  }
  pop()
  push()
  stroke(random(255),random(255),random(255))
  translate(width/2, height/2)
  for(let i=0; i<100; i++){
    extendArm(arm1, angle)
  }
  pop()
  push()
  stroke(random(255),random(255),random(255))
  translate(width/2, height/2)
  for(let i=0; i<100; i++){
    extendArm(arm1, angle)
  }
  pop()
  angle += speed
}

function extendArm(armLength, angle) {
  let randomOffset = random(100)
  rotate(angle)  //radians
  line(0, 0, 0, randomOffset)
  translate(0, randomOffset)
}
```

### ELLIPSE PATTERNS

```js
let angle = 0.0;
let speed = 0.05;

function setup() {
  createCanvas(windowWidth, windowHeight);
  noFill()
}

function draw() {
  let speed = map(mouseY, 0, height, -0.2, 0.2)
  let arm = map(mouseX, 0, width, 10, 400)
  
  background(255)

  translate(width/2, height/2)
  rotate(angle)
  for(let i=0; i<10; i++){
    push()
    rotate(i*TWO_PI/10)
    translate(0, arm)
    ellipse(0,0,50,50)
    pop()
  }
  
  angle += speed
}
```

```js
let angle = 0.0;
let speed = 0.05;

function setup() {
  createCanvas(windowWidth, windowHeight);
  noFill()
}

function draw() {
  let speed = map(mouseY, 0, height, -0.1, 0.1)
  let arm = map(mouseX, 0, width, 1, 400)
  let arm2 = map(mouseY+mouseX, 0, height+width, 1, 400)
  
  background(255)

  translate(width/2, height/2)
  rotate(angle)
  for(let i=0; i<10; i++){
    push()
    rotate(i*TWO_PI/10)
    translate(0, arm)
    ellipse(0,0,20,20)
   
    rotate(angle)
    for(let j=0; j<10; j++){
      push()
      rotate(j*TWO_PI/10)
      translate(0, arm2)
      ellipse(0,0,20,20)
      for(let k=0; k<10; k++){
        push()
        rotate(k*TWO_PI/10)
        translate(0, arm2)
        ellipse(0,0,20,20)
        pop()
      }
      pop()
    }
    
    pop()
  }
  
  angle += speed
}

function keyPressed(){
  console.log('keycode', keyCode)
}
```

### with key commands
```js
let angle = 0.0;
let speed = 0.05;
let numThings = 3;
let circSize = 10;

function setup() {
  createCanvas(windowWidth, windowHeight);
  noFill()
}

function draw() {
  let speed = map(mouseY, 0, height, -0.1, 0.1)
  let arm = map(mouseX, 0, width, 1, 400)
  let arm2 = map(mouseY+mouseX, 0, height+width, 1, 400)
  
  background(255)

  translate(width/2, height/2)
  rotate(angle)
  for(let i=0; i<numThings; i++){
    push()
    rotate(i*TWO_PI/numThings)
    translate(0, arm)
    circle(0,0,circSize)
   
    rotate(angle)
    for(let j=0; j<numThings; j++){
      push()
      rotate(j*TWO_PI/numThings)
      translate(0, arm2)
      circle(0,0,circSize)
      for(let k=0; k<numThings; k++){
        push()
        rotate(k*TWO_PI/numThings)
        translate(0, arm2)
        circle(0,0,circSize)
        pop()
      }
      pop()
    }
    
    pop()
  }
  
  angle += speed
}

function keyPressed(){
  if(keyCode===38){
    numThings++;
  }
  if(keyCode===40){
    (numThings > 1) && numThings--;
  }
  if(keyCode===37){
    (circSize > 1) && circSize--;
  }
  if(keyCode===39){
    circSize++;
  }
  console.log('circSize: ', circSize)
  console.log('numThings: ', numThings)
}
```

### Recursize example

```js
let angle = 0.0;
let speed = 0.05;
let numThings = 3;
let maxCircSize = 10;

function setup() {
  createCanvas(windowWidth, windowHeight);
  noFill()
}

function draw() {
  let speed = map(mouseY, 0, height, -0.1, 0.1)
  let maxArm = map(mouseX, 0, width, 1, 400)
  
  background(255)
  
  translate(width/2, height/2)
  rotate(angle)
  drawShapes(maxArm, maxCircSize, 3)

  angle += speed
}
function drawShapes(arm, circSize, level) {
  if (level > 0){
    for(let i=0; i<numThings; i++){
      push()
      rotate(i*TWO_PI/numThings)
      translate(0, arm)
      circle(0,0,circSize)
      rotate(angle)

      drawShapes(arm/2, circSize/2, level-1)
      pop()
    }
  }
}

function keyPressed(){
  if(keyCode===38){
    numThings++;
  }
  if(keyCode===40){
    (numThings > 1) && numThings--;
  }
  if(keyCode===37){
    (maxCircSize > 1) && maxCircSize--;
  }
  if(keyCode===39){
    maxCircSize++;
  }
}
```


### Patterns and Iterative Art links
* https://10print.org/
* http://www.generative-gestaltung.de/2/
* https://digitalideation.github.io/ba_222_gencg_h1801/notebooks/week01.html
* https://store.doverpublications.com/0486469816.html
* https://books.google.com/books/about/Designing_Tessellations.html?id=y984AQAAIAAJ
* https://www.theedkins.co.uk/jo/tess/grids.htm