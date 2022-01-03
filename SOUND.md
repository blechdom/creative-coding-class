# SOUND
* Requires P5.sound library
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
    img = loadSound('assets/img/cat.jpg')
}
```

```js
function draw() {
    image(img, 0, 0)
    // image(img, x, y, width, height)
}
```

* `snd.play()`, `setVolume()`, `snd.loop()`