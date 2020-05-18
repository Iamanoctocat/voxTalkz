# voxTalkz

voxTalkz is an open source python library that aims to provide a service to convert play-like-scripts to semi-relisic audio-dramas.

## Getting Started

### Prerequisites

voxTalkz needs several python libraries to function:
Google Text To Speach (gTTS)
Pydub (pydub)

to install those libraries, use the following commands:
```
pip3 install gTTs
pip3 install pydub
```
## Testing
Write a short script and save it as `test.script`.
```
# Assign a name to an actor
Susan:british_woman

# Make her say Hello, World!
Susan:Hello, World!
```
Open the commandline and navigate to your file.

Run the script.

```
./voxTalkz test.script test
```

Assuming all went well, you should see a file named test.mp3. Play it with your favorate mp3 playing programming.
(Other filetypes will be made avilable upon request)

### Use a sound Effect

Navigate to your home directory and create a folder named `.voxTalkz`.

Navigate into that folder and create a new folder named `soundEffects`.

Download a .mp3 sound effect and place it in the `/.voxTalkz/soundEffects/` folder, for this tutorial we will assume the file is called `footsteps.mp3`.

Write a short script and save it as `test2.script`.

```
# Assign a name to an actor
Susan:british_woman

# Make her say Hello, World!
Susan:Hello, World!
Susan:Goodbye, World!

# Add the soud effect
*footsteps
```

Open the commandline and navigate to your file.
Run the script.

```
./voxTalkz --debug test2.script test2
```

Play test2.mp3

### Adding a Modifier


Write a short script and save it as `test3.script`.

```
# Assign a name to an actor
Susan:british_woman

# Make her say Hello, World! as a little girl
Susan:Hello, World!@PITCH=0.3

# Make her say Goodbye, World! as an old woman
Susan:Goodbye, World!@PITCH=-0.3
```

Open the commandline and navigate to your file.
Run the script.

```
./voxTalkz --debug test3.script test3
```

Play the resulting test3.mp3.

## Using as a Python Library

Copy `voxTalkz.py` to the folder with the python file you want to use it with.

Add these line of code to your program:
```
import voxTalkz
...
TalkzBox = voxTalkz.voxTalkz(<scriptname>,<outputfilename>)
Parsed = TalkzBox.Parse(TalkzBox.file)
OutputSound = TalkzBox.ListToSound(Parsed)
# OutputSound is an instance of pydub.AudioSegment. It can be proccesed with pydub now.
OutputSound.export(filename, format='<.wav, .mp3, and others>')

```
## Contributing

Any and all help will be greatly appriciated!
Any feature requests will be implemented if possible.

## Authors

* **Don Flymoor** - *Initial work* - [DonFlymoor](https://github.com/DonFlymoor)

## License

This project is licensed under the GNUv3 License - see the [LICENSE.md](LICENSE.md) file for details

```
Usage: voxtalkz [input file, output file] 

Converts play-like script to a .mp3 file 
Script file must be written in this manner: 

#The first time a unknown name is called, instead of making the person talk, the name will be assigned to a person. 
Susan:normal_woman
#Then the person will "talk"
Susan:Hello, world!
#Comments are allowed!
*soundeffect_without_filename_extension

Effects can be applied by adding an @ symbal the the effect name, like so:
person1:hello, world!@VOLUME=8
A second effect can be applied by using the pipe("|") like so:
person1:Hello, World!@FADE|VOLUME=8

List of all effects:
	@FADE | Fade to nothing
	@FADE_IN | Fade in from silent
	@OVERLAY | Overlays the sound onto what has already been recorded. Use @OVERLAY=VAR1 to START the overlay at the begining of where you assigned @VAR=1
	@REPEAT= | Repeat audio segment however many times you specify. e.g. (normal_woman:Hello, world!@REPEAT=10) would produce Someone saying "Hello, world!" ten times
	@VAR=    | Assign a number to a temporary table. Only used with @OVERLAY
	@VOLUME= | Set volume change in decibels. A negitive number will reduce the volume
	@PITCH=  | Set pitch change. e.g. "normal_woman:Hello, world!@PITCH=0" would make the person sound like a little girl, while "normal_woman:Hello, world!@PITCH=-0.3" would sound like an old woman

List of all actors:
	indian_man | Clearly speaks
	american_woman | Clearly speaks
	scottish_woman
	russian_woman
	drawling_man
	danish_woman | Clearly speaks
	dutch_woman
	au_woman | Clearly speaks
	british_woman | Clearly speaks
	indian_woman | Clearly speaks
	spanish_woman
	french_woman
	hindu_woman
	alien_man
	italian_man
	phone_woman
	korean_man | Clearly speaks
	dramatized_woman
	silly_man
	robot_man
	dramitized_girl
	bored_teen
	happy_girl
	boss_lady
	youong_grandma
	spoiled_girl
	normal_woman
    
Sound effects must be in the .mp3 format and placed in /home/user/.voxtalk/soundEffects
To use footsteps.mp3: put *footsteps in your script
```