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

