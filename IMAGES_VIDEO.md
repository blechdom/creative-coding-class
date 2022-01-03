# IMAGES AND VIDEO
* Make sure you are logged-in to the editor
* Open the `Sketch Files` tab (the arrow above the top left corner of the coding window)
* Select `Upload file`
* Drag/Drop media files
## Images
* Image Formats: JPG, GIF, PNG, SVG
* Images can load in the background
* `preload()` event
* `loadImage()` function
```js
function preload() {
    img = loadImage('assets/img/cat.jpg')
}
```

```js
function draw() {
    image(img, 0, 0)
    // image(img, x, y, width, height)
}
```

* `img.width` and `img.height`

## Typography
* accepts `.ttf` and `.otf` files
* dowload from web or use https://fonts.google.com/
* `textFont()`, `loadFont()` and `textSize()`
```js
text('Hello World', x, y, width, height)
```