# Score Follow


## Introduction

Score Follow is a Max for Live device that allows real-time scrolling and/or playback of graphical score files. The device supports a variety of image and video formats. Each instance of the device generates its own video output window and can host up to six score files, allowing for mulitple scores to be played in sequence for concert presentation. Multiple instances of the device may be loaded on separate tracks within the same Max for Live set in order to support synchronized output of distinct score files; for example, one instance could host a score to be projected for viewing by an audience, while another could host an annotated version of the same score to be viewed on displays by instrumentalists. Playback may be directly linked to Live's transport or controlled via automation curves. Score Follow can also be loaded as a standalone application, in which all parameters are exposed via MIDI and OSC.

Score Follow was developed in 2018 for use by the Ensemble d'oscillateurs at the Université de Montréal. The project was directed by Nicolas Bernier and implemented by Evan Montpellier.

## Main Window

### Maximum image width

Score Follow stores score image files as OpenGL textures. This number is the maximum width (in pixels) of a texture that can be used on your system as determined by your GPU. Score files with a dimenstion that is larger than this value will not load correctly.

### Score image slots

Drag an image or video file onto one of the slots in order to load it, or click on a slot to open a file dialog box.

### Timing controls

#### dur (min)

Sets the amount of time you want it to take for the score to scroll from beginning to end.

#### post-pixels

If your score file contains horizontal space after the graphical elements (e.g., because it has a border), you must specify the width of this trailing space in pixels. This quantity must be entered accurately in order for the score to scroll at the correct rate. It is suggested that you measure this precisely using Preview, Photoshop or another image viewing/editing application.

#### pre-pixels

Same as above, but for horizontal pixels that precede the graphical elements in the score file.

#### hold (ms)

The amount of time to wait after the end of one score file before the next score file is loaded. Useful for creating pauses in a concert program.

### Clear buttons

Click to remove a score file from the corresponding slot.

### Overlay settings

Score Follow allows you to superimpose several overlays, including a playhead cursor, a timecode display and an instrument guide.

#### Cursor

The cursor is a vertical bar used to indicate the current position in the score.

##### On/off

Toggle the cursor on or off.

##### Colour

Set the colour of the cursor.

##### Alpha

Set the transparency of the cursor.

##### Position

Set the horizontal position of the cursor.

##### Width

Set the width of the cursor.

#### Timecode

The timecode overlay shows the current time in the format HH:MM:SS:msmsms. The time value is derived from Live's transport (Max for Live version) or Score Follow's internal transport (standalone version).

##### On/Off

Toggle the timecode overlay on or off.

##### Colour

Set the colour of the timecode overlay.

##### Alpha

Set the transparency of the timecode overlay.

##### Position

Set the horizontal position of the timecode overlay.

##### Scale

Sets the size of the timecode overlay.

#### Instruments

The instruments guide is a vertical bar that appears at the left-hand side of the output window with labels for each individual instrument (by default, oscillators 1-10) used to visually divide the score into parts for individual instrumentalists.

##### On/Off

Toggle the instrument guide on or off.

### Scrolling settings

#### Scroll mode
Sets the scrolling mode. In mode 0 (internal), scrolling is controlled by Live's transport. In mode 1 (automation), scrolling is controlled by the Scroll Position parameter.

#### Scroll position
Only works when scroll mode is set to 1 (automation). Sets the position of the scrolling image as a value from 0. (start) to 1. (end). Useful for automating complex scroll movements, including reversals, pauses and speed changes.

#### Scroll speed

Only works when scroll mode is set to 0 (internal). Controls the speed at which the score image scrolls, ranging from 0. (fully stopped) to 1. (100% speed).

### Window settings

#### Retrieve
Returns the output window to a default position.

#### Floating
Toggles whether the output window floats over other windows.

#### Fullscreen
Toggles whether the output window is fullscreen.

### Instance ID

Shows the three-digit ID tag automatically assigned to this instance of Score Follow by Live. This is mostly only useful for debugging.

### Framerate counter

Displays the framerate of the video output window in FPS.

## Video output

Score images appear in a video output window. The name of the window is always (instance-id)_score, e.g. 024_score. To make an output window fullscreen, click on the window and then press the escape key or click the fullscreen button in the Score Follow interface. If you have additional displays or projectors connected, drag the window to the display that you wish for it to appear fullscreen on before pressing escape. If you lose the window, click the Retrieve button in the Score Follow interface to return it to a default positon.


## Multiple instances

Multiple instances of Score Follow may be loaded simultaneously. Each instance of the device generates its own video output window. Timing and overlay controls are shared between all instances of the device in a given set. Score image files are stored independently for each instance, as are output window settings. This mix of shared and independent parameters is designed for concert scenarios that require both a projected image for audience viewing as well as a separate image for performers. In such a scenario, one instance of the device can be loaded with score files intended for projection, while a second instance can be loaded with a related-but-distinct set of score files for viewing by performers (e.g., the same images, but with more explicit annotations).

## Standalone

In addition to the Max for Live device, Score Follow is available as a standalone application. The standalone version has several unique features, including an internal transport with keyboard controls, a distinct saving/loading mechanism and OSC control over all parameters.

### Transport controls

The standalone version of Score Follow runs off its own internal transport. Press the spacebar to pause or unpause the transport. Press the left arrow key to rewind by ten seconds and the right arrow key to fast-forward by ten seconds.

### Saving and loading

Whereas the Max for Live version of Score Follow benefits from Live's ability to save device parameters along with a Live set, the standalone version requires that you manually save and load parameter files. A set of parameters may be saved as a JSON file. To save your settings, click on the "save" button on the right of the application window. To reload parameters from a file, click the "load" button and select the file you wish to use.

### OSC namespace
In the standalone version of Score Follow, all parameters are exposed for control via OSC. The namespace is as follows:

/[1-6]/clear

data type: any

Clears the file from the slot.

/[1-6]/dur

data type: float (0-n)

Sets the time (in minutes) it will take to play through the score.

/[1-6]/pixels/pre

data type: int (0-n)

Sets the number of pixels before the graphical elements in the score image.

/[1-6]/pixels/post

data type: int (0-n)

Sets the number of pixels after the graphical elements in the score image.

/[1-6]/hold

data type: int (0-n)

Sets the hold time before the next score is loaded.

/[1-6]/file

data type: string

Sets the file to be loaded for a given slot.

/aspect/preserve

data type: string

Toggles whether the image should be displayed with its original aspect ratio or stretched to fill the output window.

/overlay/cursor/on

data type: bool

Toggles the cursor overlay on and off.

/overlay/cursor/colour

data type: vec3f (0.-1.)

Sets the colour of the cursor.

/overlay/cursor/alpha

data type: float (0.-1.)

Sets the transparency of the cursor.

/overlay/cursor/position

data type: float (0.-1.)

Sets the horizontal position of the cursor.

/overlay/cursor/width

data type: float (0.-100.)

Sets the width (in pixels) of the cursor.

/overlay/instruments/on

data type: bool

Toggles the instruments overlay on and off.

/overlay/timecode/on

data type: bool

Toggles the timecode overlay on and off.

/overlay/timecode/colour

data type: vec3f (0.-1.)

Sets the colour of the timecode overlay.

/overlay/timecode/alpha

data type: float (0.-1.)

Sets the transparency of the timecode overlay.

/overlay/timecode/position/x

data type: float (-1.-1.)

Sets the horizontal position of the timecode overlay.

/overlay/timecode/position/y

data type: float (-1.-1.)

Sets the vertical position of the timecode overlay.

/overlay/timecode/scale

data type: float (0.-3.)

Sets the size of the timecode overlay.

/scroll/mode

data type: bool

Sets the scrolling mode. In mode 0 (internal), scrolling is controlled by the internal transport. In mode 1 (automation), scrolling is controlled by the Scroll Position parameter.

/scroll/position

data type: float (0.-1.)

Only works when scroll mode is set to 1 (automation). Sets the position of the scrolling image as a value from 0. (start) to 1. (end). Useful for automating complex scroll movements, including reversals, pauses and speed changes.

/scroll/speed

data type: float (0.-1.)

Only works when scroll mode is set to 0 (internal). Controls the speed at which the score image scrolls, ranging from 0. (fully stopped) to 1. (100% speed).

/window/retrieve

data type: any

Returns the output window to a default position.

/window/floating

data type: bool

Toggles whether the output window floats over other windows.

/window/fullscreen

data type: bool

Toggles whether the output window is fullscreen.

/window/render

data type: bool

Toggles video rendering on or off.

/opacity

data type: float (0.-1.)

Sets the opacity of the score image. Useful for fading in and out.