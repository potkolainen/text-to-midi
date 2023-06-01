# TEXT to MIDI converter 1.0 build
   # Main features
`this python script writes .MID file from inputted text in SMF0 format. can be used with external Ai such as Chat-GPT`

# Text input windows

it has 4 text windows to input text and function detailed next to them. very easy to use.
listed from up to down all windows.
| Rank |  Function     |
|-----:|---------------|
|     1| Track name    |
|     2| Time siganture|
|     3| BPM           |
|     4| Text to .MID  |
|     5| Example text  |
|     6| Log           |

EMPTY one without description is where you insert text to turn into .MID file such as shown in window under it.

![MIDIconvUI](https://github.com/potkolainen/text-to-midi/assets/135180930/82ee6cf9-b70d-4349-83c2-469cd11a648f)


# Errors
Log lists events for you, such as .MID save status or errors. 
Most common error is when all text fields are not filled. 
It will be shown as:

    Error occurred while saving MIDI: invalid literal for int() with base 10: ''
This means track name, time signature or BPM was not inserted

# Reddit

https://www.reddit.com/r/musicproduction/comments/13xlfwd/text_to_midi_file/?utm_source=share&utm_medium=android_app&utm_name=androidcss&utm_term=1&utm_content=share_button
If you run in issues. You can comment them there, or here on github. Also you can give feedback and suggestions on reddit.

# Needed Packages for the python script
python script uses packages that are needed for running the script
| Rank | Packages  |
|-----:|-----------|
|     1| Python3.11|
|     2| mido      |
|     3| pyperclip |

Rest are included in standard python library.
For me it helped when i installed Python from microsoft store. My cmd terminal didnt find the one i installed first from python.org

once python 3.11 is installed open your windows command terminal
type command:

    pip install mido
    
And

    pip install pyperclip
    
These commands will install nedded packages from python directory. 


# .exe
includes also .exe file in standalone BRANCH.
MAIN branch has only Open source python code.
This does not need Python or packages installed. (download .exe from STANDALONE Branch) 

