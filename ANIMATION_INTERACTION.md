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
* Skew - `skewX(angle)` - skews a shape around its x-axis
* Skew - `skewY(angle)` - skews a shape around its y-axis

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


```



