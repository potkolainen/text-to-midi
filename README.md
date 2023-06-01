# text-to-midi-converter
# Main features
`this python script writes .MID file from inputted text in SMF0 format. can be used with external Ai such as Chat-GPT`

it has 4 text windows to input text and function detailed next to them. very easy to use

![midi to text](https://github.com/potkolainen/text-to-midi/assets/135180930/4bf9aa96-6e3f-48dd-8c8e-a383a452ff7f)

Lowest text window works as a log. It gives you information if file is saved succesfully or if you encountered with an error. If you cannot see the message. Use mouse wheel. 

# errors
Lowest text field is log. 
It lists events for you such as .mid save status or errors. 
Most common error is when all text fields are not filled. 


# reddit

https://www.reddit.com/r/musicproduction/comments/13xlfwd/text_to_midi_file/?utm_source=share&utm_medium=android_app&utm_name=androidcss&utm_term=1&utm_content=share_button
If you run in issues. You can comment them there, or here on github. 

# Needed Packages for the script
python script uses packages that are needed for running the script or .exe so far
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
includes also .exe file (this for now needs python and packages installed, i will fix this later)

# Code
Here i will soon add some parts of the code that will present their functions
