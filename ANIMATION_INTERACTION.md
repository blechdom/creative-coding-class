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
#### Pong-Like Animation
```js
let x, y = 0
let down = true
let speed = 3

function setup() {
  createCanvas(windowWidth, windowHeight)
  x = windowWidth / 2
  y = windowHeight / 2
}

function draw() {
  speed = mouseY / 8
  background(220)
  strokeWeight(10)
  line(x, y - 1, x, y + 1)
  if (down) {
    if (x > 0) {
      x -= speed
    } else {
      down = false
    }
  } else {
    if (x < windowWidth){
      x += speed
    }
    else {
      down = true
    }
  }
}
```

```js
let x, y = 0
let down = true
let speed = 3

function setup() {
  createCanvas(windowWidth, windowHeight)
  background(220)
  x = 0
  y = 0
}

function draw() {
  speed = .5
  background(220)
  for(let i=0; i<8; i++){
   backAndForth(i) 
  }
}

function backAndForth(i) {
  //console.log(x)
  let xOffset = ((windowWidth / 8) * i) + (windowWidth/16)
  let yOffset = ((windowHeight / 8) * i) + (windowHeight/16)
  
  ellipse((x+xOffset)%windowWidth, y+yOffset, windowWidth / 8, windowHeight / 8)
  x += speed
  let thisX = (x+xOffset)%windowWidth;
  let goingUp = true;
  if(thisX > (windowWidth - (windowWidth/8))){
    goingUp = false;
  }
  //console.log('goingUp ', goingUp)
  ellipse(thisX, y+yOffset, windowWidth / 8, windowHeight / 8)
  /*if (down) {
    
    if (x > 0) {
      x -= speed
    } else {
      down = false
    }
  } else {
    if (x < windowWidth){
      x += speed
    }
    else {
      down = true
    }
  }
  */
}

```