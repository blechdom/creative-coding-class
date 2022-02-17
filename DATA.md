# DATA, LIBRARIES, and APIs

## Google Fonts
* https://editor.p5js.org/allison.parrish/sketches/ByyxP7Gbe

* textToPoints()
```js
let font;
function preload() {
  font = loadFont('assets/inconsolata.otf');
}

let points;
let bounds;
function setup() {
  createCanvas(100, 100);
  stroke(0);
  fill(255, 104, 204);

  points = font.textToPoints('p5', 0, 0, 10, {
    sampleFactor: 5,
    simplifyThreshold: 0
  });
  bounds = font.textBounds(' p5 ', 0, 0, 10);
}

function draw() {
  background(255);
  beginShape();
  translate(-bounds.x * width / bounds.w, -bounds.y * height / bounds.h);
  for (let i = 0; i < points.length; i++) {
    let p = points[i];
    vertex(
      p.x * width / bounds.w +
        sin(20 * p.y / bounds.h + millis() / 1000) * width / 30,
      p.y * height / bounds.h
    );
  }
  endShape(CLOSE);
}
```
* particle text: https://editor.p5js.org/creativecoding/sketches/ryBpNdjeN

* WEBGL TEXT
WEBGL: Only opentype/truetype fonts are supported. You must load a font using the loadFont() method (see the example above). stroke() currently has no effect in webgl mode. Learn more about working with text in webgl mode on the wiki.

```js
let inconsolata;
function preload() {
  inconsolata = loadFont('assets/inconsolata.otf');
}
function setup() {
  createCanvas(100, 100, WEBGL);
  textFont(inconsolata);
  textSize(width / 3);
  textAlign(CENTER, CENTER);
}
function draw() {
  background(0);
  let time = millis();
  rotateX(time / 1000); // mouseX
  rotateZ(time / 1234); // mouseY
  text('p5.js', 0, 0);
}
```


## Libraries
* https://p5js.org/libraries/
* https://idmnyu.github.io/p5.js-speech/
* https://rednoise.org/rita/
* https://github.com/FreddieRa/p5.3D

### SPEECH RECOGNITION
* `<script src="https://cdn.jsdelivr.net/gh/IDMNYU/p5.js-speech@0.0.3/lib/p5.speech.js"></script>`


## Data
* https://shiffman.net/a2z/data-apis/
* https://editor.p5js.org/blechdom/sketches/WOkPsXmsk

## get the weather
```js
// Loading Weather Data from Open Weather Map
// https://www.youtube.com/watch?v=ecT42O6I_WI&list=PLRqwX-V7Uu6a-SQiI4RtIwuOrLJGnel0r&index=6&t=0s


// We're going to store the temperature
let temperature = 0;
// We're going to store text about the weather
let weather = "";

let json;

function preload() {
  // The URL for the JSON data (replace "imperial" with "metric" for celsius)
  let url = "https://api.openweathermap.org/data/2.5/weather?q=New%20York&units=imperial&APPID=e812164ca05ed9e0344b89ebe273c141";
  json = loadJSON(url);

}

function setup() {
  createCanvas(200, 200);

  // Get the temperature
  temperature = json.main.temp;

  // Grab the description, look how we can "chain" calls.
  weather = json.weather[0].description;
}

function draw() {
  background(255);
  fill(0);

  // Display all the stuff we want to display
  text("City: New York", 10, 50);
  text("Current temperature: " + temperature, 10, 70);
  text("Forecast: " + weather, 10, 90);
}
```

## APIS
* https://apilist.fun/
* https://public-apis.xyz/page/3

### RAPID API for GOOGLE TRANSLATE
* https://rapidapi.com
* https://rapidapi.com/googlecloud/api/google-translate1/
* Click Subscribe to Test (Careful, if it's not free)
* Test Endpoint with 'translate' call
* Choose `(JavaScript)XMLHttpRequest` Code Snippet to avoid CORS issues
* Copy into p5.js, preload or async...



### TWITTER with CodeBird
* https://editor.p5js.org/brysonian/sketches/rJZ1BCd1f

### EXAMPLES

* https://nervousdata.com/pfum-p5.html

#### work in progress
```js

var myRec = new p5.SpeechRec();

function preload() {
const data = "q=Hello%2C%20world!&target=es&source=en";

const xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
	if (this.readyState === this.DONE) {
		console.log(this.responseText);
	}
});

xhr.open("POST", "https://google-translate1.p.rapidapi.com/language/translate/v2");
xhr.setRequestHeader("content-type", "application/x-www-form-urlencoded");
xhr.setRequestHeader("accept-encoding", "application/gzip");
xhr.setRequestHeader("x-rapidapi-host", "google-translate1.p.rapidapi.com");
xhr.setRequestHeader("x-rapidapi-key", "e25cd8892cmsh0133c9b968ad2c4p1be3fejsn75573dfc61c2");

xhr.send(data);
}

function setup() {
  createCanvas(400, 400);
  var foo = new p5.Speech(); // speech synthesis object
foo.speak('hi there'); // say something
  textSize(32);
		textAlign(CENTER);
		text("say something", width/2, height/2);
		myRec.onResult = showResult;
		myRec.start();
}

function draw() {
  
}
function showResult()
	{
		if(myRec.resultValue==true) {
			background(192, 255, 192);
			text(myRec.resultString, width/2, height/2);
			console.log(myRec.resultString);
          
		}
	}
```