# Picture Frame

This example creates a digital picture frame using images from [picsum.photos](http://picsum.photos/) - you'll definitely need an Internet connection to run this game! The code demonstrates some of the key abstraction features that have been implemented in the Predigame platform.


## Prerequisites
You'll need to have the Predigame platform installed, a trusty text editor handy, and the command prompt (or terminal) open to complete this tutorial. Visit [http://predigame.io](http://predigame.io) for installation instructions.

## Download Existing Game (Optional)
We have a version of this game already done and ready to go. Just run the following command:

```
pred new pictureframe
```

Then read the rest of the tutorial and follow along.


## Getting Started
To get things started, we're going to create a new Predigame game. This can be done by typing the following the command in the terminal:

```
pred new pictureframe
```
Now in the text editor, find and open the file `pictureframe/game.py`. This file is used to create a basic Predigame canvas that we'll use to place our fireworks. For the code, we'll start by defining our screen dimensions (30 x 20 grid cells) and provide a title.

```python
WIDTH = 30
HEIGHT = 20
TITLE = 'Fireworks'
```

For this example, we'll want to enable fullscreen mode:

```python
FULLSCREEN=True
```

Next we'll add the background function call. In Predigame we always try to provide defaults for functions. The `background()` function can be used for loading static images (provided they are in your `backgrounds/` directory) or static colors (defined as a constant or (RED, GREEN, BLUE) values). If no argument is provided to `background()`, we fetch an image from [picsum.photos](http://picsum.photos/).

Add this line to your file:
```python
background()
```

Now let's give it a test run!

```
pred game.py
```
You'll notice that the game is loaded in full screen, but the picture is static. To fix this up, let's add a timer callback.

```python
background()
callback(background, 10, repeat=FOREVER)
```

The code calls `background()` by itself to seed the display with the first image. The second and beyond image will be loaded by the `callback()` function with a `10` second delay.

Here's the completed version:
```python
WIDTH=30
HEIGHT=20
FULLSCREEN=True

background()
callback(background, 10, repeat=FOREVER)
```

Save your changes and enjoy the pics!

```
pred game.py
```

## CHALLENGE - Add the time!
One of the neat things about Predigame is that you can always drop in python code to help complete a game. The following example is an extension to the previous example, but now  adds the time. We had to refactor things a bit, but the code has a similar operation.

```python
WIDTH=30
HEIGHT=20
FULLSCREEN=True

from time import localtime, strftime
clock = None
def update():
   global clock
   if clock:
      clock.destroy()
   background()
   clock = text(strftime("%H:%M", localtime()), color=WHITE, pos=(25, 18), size=2)
update()
callback(update, 10, repeat=FOREVER)
```
