# SOUND
* Requires P5.sound library

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

## Resources
* https://creative-coding.decontextualize.com/synthesizing-analyzing-sound/

* https://p5js.org/reference/#/libraries/p5.sound

* https://dood.al/pinktrombone/

* https://nathanmelenbrink.github.io/artg2260/09_media/audio.html

* https://therewasaguy.github.io/p5-music-viz/

* https://www.jezzamon.com/fourier/