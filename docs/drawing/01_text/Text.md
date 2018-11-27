
# Drawing Text
OPENRNDR comes with two text drawing modes: vector based and image based.
The vector based mode is advised for large font sizes while the bitmap based mode is advised for smaller font sizes.

## Relevant apis
TODO it would be great to generate links of these to the dokka API doc
```kotlin
Drawer.fontMap
Drawer.text(text:String, x:Double, y:Double)
FontImageMap.fromUrl(url:String, size:Double)
```

## Drawing bitmap based text

```kotlin
extend {
    drawer.background(ColorRGBa.PINK)
    drawer.fill = ColorRGBa.WHITE
    drawer.circle(drawer.bounds.center, Math.abs(Math.cos(seconds)) * 300)
}
```

[Link to the full example](https://github.com/openrndr/openrndr-examples/blob/master/examples/drawing/01_text/Text000.kt)

<video controls>
    <source src="media/text-001.mp4" type="video/mp4"></source>
</video>


## Advanced text drawing
OPENRNDR comes with a Writer class that allows for basic typesetting. The Writer tool is based on the concept of text box and a cursor.
Its use is easiest demonstrated through an example:

```kotlin
extend {
    drawer.background(ColorRGBa.PINK)
    val writer = Writer(drawer)
    drawer.fontMap = FontImageMap.fromUrl("file:fonts/iosevka-custom-medium.ttf", 20.0)
    drawer.stroke = null
    drawer.fill = ColorRGBa.WHITE
    writer.box = Rectangle(Vector2(100.0, 100.0), 400.0, 400.0)
    writer.text("Some text")
    writer.newLine()
    writer.text("Some more text")
}
```

[Link to the full example](https://github.com/openrndr/openrndr-examples/blob/master/examples/drawing/01_text/Text001.kt)

<video controls>
    <source src="media/text-002.mp4" type="video/mp4"></source>
</video>


## Specifying the text area

<img src="media/text-003.png"/>

The writer has a box property that determines the area in which it can place text.

```kotlin
writer.box = Rectangle(Vector2(100.0, 100.0), 400.0, 400.0)
```

[Link to the full example](https://github.com/openrndr/openrndr-examples/blob/master/examples/drawing/01_text/Text002.kt)

In some cases you may want to have a an infinitely large box, this avoids line breaks altogether.

```kotlin
writer.box = Rectangle(Vector2(100.0, 100.0), Double.`POSITIVE_INFINITY`, Double.`POSITIVE_INFINITY`)
```

[Link to the full example](https://github.com/openrndr/openrndr-examples/blob/master/examples/drawing/01_text/Text002.kt)

A quick way to set the box to equate the bounds of the screen:

```kotlin
writer.box = drawer.bounds
writer.box = drawer.bounds.offsetEdges(-50.0)
```

[Link to the full example](https://github.com/openrndr/openrndr-examples/blob/master/examples/drawing/01_text/Text002.kt)

### Text properties
The `Writer` has several properties that affect the appearance of text.

| Property name      | Description |
|---------------------|-------------|
| `tracking` | additional space between the characters |
| `leading`   | additional space between lines of text |
| `ellipsis`   | the character to display when text does not fit the designated space|
