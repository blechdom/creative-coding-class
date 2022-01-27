# SOUND
* Requires P5.sound library

Theramin: https://www.youtube.com/watch?v=pSzTPGlNa5U

Ableton: https://learningsynths.ableton.com/

## Sound Files
* Make sure you are logged-in to the editor
* Open the `Sketch Files` tab (the arrow above the top left corner of the coding window)
* Select `Upload file`
* Drag/Drop sound files

* Sound Formats: mp3, ogg, wav and m4a/aac (based on browser support)
* Sounds can load in the background
* `preload()` event
* `loadSound()` function
```js
function preload() {
    snd = loadSound('assets/img/cat.jpg')
}
```
* `snd.play()`, `setVolume()`, `snd.loop()`
```js
function draw() {
    snd.play()
}
```
## Synthesis

## Sound Manipulation
https://editor.p5js.org/p5/sketches/Sound:_Manipulate_Sound

```js
let song;

function preload() {
  // Load a sound file
  song = loadSound('assets/Damscray_DancingTiger.mp3');
}

function setup() {
  createCanvas(710, 400);

  // Loop the sound forever
  // (well, at least until stop() is called)
  song.loop();
}

function draw() {
  background(200);

  // Set the volume to a range between 0 and 1.0
  let volume = map(mouseX, 0, width, 0, 1);
  volume = constrain(volume, 0, 1);
  song.amp(volume);

  // Set the rate to a range between 0.1 and 4
  // Changing the rate alters the pitch
  let speed = map(mouseY, 0.1, height, 0, 2);
  speed = constrain(speed, 0.01, 4);
  song.rate(speed);

  // Draw some circles to show what is going on
  stroke(0);
  fill(51, 100);
  ellipse(mouseX, 100, 48, 48);
  stroke(0);
  fill(51, 100);
  ellipse(100, mouseY, 48, 48);
}
```

## Resources
* https://creative-coding.decontextualize.com/synthesizing-analyzing-sound/

* https://p5js.org/reference/#/libraries/p5.sound

* https://dood.al/pinktrombone/

* https://edisciplinas.usp.br/pluginfile.php/5212278/mod_resource/content/3/undefined/Getting%20Started%20with%20p5.js%20Making%20Interactive%20Graphics%20in%20JavaScript%20and%20Processing%20by%20Lauren%20McCarthy%2C%20Casey%20Reas%2C%20Ben%20Fry%20%28z-lib.org%29.pdf

* https://nathanmelenbrink.github.io/artg2260/09_media/audio.html

* https://therewasaguy.github.io/p5-music-viz/

* https://www.jezzamon.com/fourier/


* Sountfont: https://b2renger.github.io/Introduction_p5js/07_audio_01_soundfont/index.html

* https://compform.net/sound/

## Audio Recording

```js
// uses the p5 SoundRecorder and SoundFile classes to record the audio output.
// begins recording when called. records for _length_ time in milliseconds.
function record(length) {
  var soundRecorder = new p5.SoundRecorder();
  var soundFile = new p5.SoundFile();
  soundRecorder.record(soundFile);
  setTimeout(function () {
    console.log("Recording Complete");
    soundRecorder.stop();
    save(soundFile, "output.wav");
  }, length);
}
```

### filters
### audio routing 
* p5.AudioIn, soundOut, 
.jump()
### recording

```js
var mic, recorder, soundFile;

var state = 0; // mousePress will increment from Record, to Stop, to Play

function setup() {
  createCanvas(400,400);
  background(200);
  fill(0);
  text('Enable mic and click the mouse to begin recording', 20, 20);

  // create an audio in
  mic = new p5.AudioIn();

  // users must manually enable their browser microphone for recording to work properly!
  mic.start();

  // create a sound recorder
  recorder = new p5.SoundRecorder();

  // connect the mic to the recorder
  recorder.setInput(mic);

  // create an empty sound file that we will use to playback the recording
  soundFile = new p5.SoundFile();
}

function mousePressed() {
  // use the '.enabled' boolean to make sure user enabled the mic (otherwise we'd record silence)
  if (state === 0 && mic.enabled) {

    // Tell recorder to record to a p5.SoundFile which we will use for playback
    recorder.record(soundFile);

    background(255,0,0);
    text('Recording now! Click to stop.', 20, 20);
    state++;
  }

  else if (state === 1) {
    recorder.stop(); // stop recorder, and send the result to soundFile

    background(0,255,0);
    text('Recording stopped. Click to play & save', 20, 20);
    state++;
  }

  else if (state === 2) {
    soundFile.play(); // play the result!
    saveSound(soundFile, 'mySound.wav'); // save file
    state++;
  }
}
```
### Looper

https://editor.p5js.org/cassie/sketches/sPljTnaPI
### microphone processing

### distortion

https://editor.p5js.org/cassie/sketches/BiOzrHdCQ

### filter
https://editor.p5js.org/cassie/sketches/g4TH5QBlj

### Granular
https://editor.p5js.org/cassie/sketches/TFX7S1UOS

### drum machine
https://editor.p5js.org/cassie/sketches/L_ZBnqCwG

scribble audio
http://scribble.audio/


* https://github.com/CodingTrain/website/tree/main/Tutorials/P5JS/p5.js_sound

If you can't come up with a creative sound project, try to add sounds to this visual project:

```js
// require https://cdn.jsdelivr.net/npm/p5@1.4.0/lib/p5.js
// require https://cdnjs.cloudflare.com/ajax/libs/p5.js/0.6.0/addons/p5.sound.js

let x;
let y;
let dX;
let dY;

function setup() {
  createCanvas(400, 200);
  fill(255);
  noStroke();

  x = 200;
  y = 100;
  dX = 6;
  dY = 5;
}

function draw() {
  background(50);
  x += dX;
  y += dY;

  if (x > 395) {
    dX = -abs(dX);
  }
  if (y > 195) {
    dY = -abs(dY);
  }
  if (x < 5) {
    dX = abs(dX);
  }
  if (y < 5) {
    dY = abs(dY);
  }

  ellipse(x, y, 10, 10);
}
```