# SOUND
* Requires P5.sound library

Theramin: https://www.youtube.com/watch?v=pSzTPGlNa5U

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

## Video

## Resources
* https://creative-coding.decontextualize.com/synthesizing-analyzing-sound/

* https://p5js.org/reference/#/libraries/p5.sound

* https://dood.al/pinktrombone/

* https://edisciplinas.usp.br/pluginfile.php/5212278/mod_resource/content/3/undefined/Getting%20Started%20with%20p5.js%20Making%20Interactive%20Graphics%20in%20JavaScript%20and%20Processing%20by%20Lauren%20McCarthy%2C%20Casey%20Reas%2C%20Ben%20Fry%20%28z-lib.org%29.pdf

* https://nathanmelenbrink.github.io/artg2260/09_media/audio.html

* https://therewasaguy.github.io/p5-music-viz/

* https://www.jezzamon.com/fourier/