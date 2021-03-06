 
 # Drawing text
OPENRNDR comes with support for rendering bitmap text. There are two modes of operation for writing text, a direct
mode that simply writes a string of text at the requested position, and a more advanced mode that can place texts 
in a designated text area. 
 
 ## Simple text rendering

To render simple texts we first make sure a font is loaded and assigned to `drawer.fontMap`, we then use [`drawer.text`](https://api.openrndr.org/org.openrndr.draw/-drawer/text.html) to
draw the text. 
 
 <img src="media/text-001.png"/> 
 
 ```kotlin
program {
    val font = loadFont("data/IBMPlexMono-Bold.ttf", 48.0)
    extend {
        drawer.clear(ColorRGBa.PINK)
        drawer.fontMap = font
        drawer.fill = ColorRGBa.BLACK
        drawer.text("HELLO WORLD", width / 2.0 - 100.0, height / 2.0)
    }
}
``` 
 
 [Link to the full example](https://github.com/openrndr/openrndr-examples/blob/master/src/main/kotlin/examples/04_Drawing_basics/C02_Text000.kt) 
 
 ## Advanced text rendering
OPENRNDR comes with a [`Writer`](https://api.openrndr.org/org.openrndr.text/-writer/index.html) class that allows for basic typesetting. The `Writer` tool is based on the concept of text box and a cursor.

Its use is easiest demonstrated through an example: 
 
 <img src="media/text-002.png"/> 
 
 ```kotlin
program {
    val font = loadFont("file:data/IBMPlexMono-Bold.ttf", 24.0)
    extend {
        drawer.clear(ColorRGBa.PINK)
        drawer.fontMap = font
        drawer.fill = ColorRGBa.BLACK
        
        writer {
            newLine()
            text("Here is a line of text..")
            newLine()
            text("Here is another line of text..")
        }
    }
}
``` 
 
 [Link to the full example](https://github.com/openrndr/openrndr-examples/blob/master/src/main/kotlin/examples/04_Drawing_basics/C02_Text001.kt) 
 
 ### Specifying the text area
The `box` field of `Writer` is used to specify where text should be written. Let's set the text area
to a 300 by 300 pixel rectangle starting at (40, 40).

We see that the text is now drawn with margins above and left of the text, and that the second line of
text is set on two rows. 
 
 <img src="media/text-003.png"/> 
 
 ```kotlin
program {
    val font = loadFont("file:data/IBMPlexMono-Bold.ttf", 24.0)
    extend {
        drawer.clear(ColorRGBa.PINK)
        drawer.fontMap = font
        drawer.fill = ColorRGBa.BLACK
        
        writer {
            box = Rectangle(40.0, 40.0, 300.0, 300.0)
            newLine()
            text("Here is a line of text..")
            newLine()
            text("Here is another line of text..")
        }
    }
}
``` 
 
 [Link to the full example](https://github.com/openrndr/openrndr-examples/blob/master/src/main/kotlin/examples/04_Drawing_basics/C02_Text002.kt) 
 
 ### Text properties
Text tracking -the horizontal space between characters- and leading -the vertical space between lines- can be
set using `Writer.style.leading` and `Writer.style.tracking`. 
 
 <video controls>
    <source src="media/text-004.mp4" type="video/mp4"></source>
</video>
 
 
 ```kotlin
program {
    val font = loadFont("file:data/IBMPlexMono-Bold.ttf", 24.0)
    extend {
        drawer.clear(ColorRGBa.PINK)
        drawer.fontMap = font
        drawer.fill = ColorRGBa.BLACK
        
        writer {
            // -- animate the text leading
            leading = cos(seconds) * 20.0 + 24.0
            // -- animate the text tracking
            tracking = sin(seconds) * 20.0 + 24.0
            box = Rectangle(40.0, 40.0, width - 80.0, height - 80.0)
            newLine()
            text("Here is a line of text..")
            newLine()
            text("Here is another line of text..")
            newLine()
            text("Let's even throw another line of text in, for good measure! yay")
        }
    }
}
``` 
 
 [Link to the full example](https://github.com/openrndr/openrndr-examples/blob/master/src/main/kotlin/examples/04_Drawing_basics/C02_Text003.kt) 
