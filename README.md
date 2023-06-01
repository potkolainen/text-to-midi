# text-to-midi-converter
# Main features
`this python script writes .MID file from inputted text. can be used with external Ai such as Chat-GPT`

it has 4 text windows to input text and function detailed next to them. very easy to use

![midi to text](https://github.com/potkolainen/text-to-midi/assets/135180930/4bf9aa96-6e3f-48dd-8c8e-a383a452ff7f)

# reddit
https://www.reddit.com/r/synthesizers/comments/13x3lan/text_to_midi_file/?utm_source=share&utm_medium=android_app&utm_name=androidcss&utm_term=1&utm_content=share_button

# Needed Packages for the script
python script uses  !!!OPEN SOURCE!!! packages that are needed for running the script or .exe so far
| Rank | Packages  |
|-----:|-----------|
|     1| Python3.11|
|     2| mido      |
|     3| pyperclip |

Rest are invluded in standard python library.
For me it helped when i installed Python from microsoft store. My cmd terminal didnt find the one i installed first from python.org

once python 3.11 is installed open your windows command terminal
type:
pip install mido
pip install pyperclip

# .exe
includes also .exe file (this for now needs pyhon and packages installed, i will fix this later)

# Code
Here under you will see the whole code used in this project



    # import tkinter as tk
    from tkinter import filedialog, messagebox
    import mido
    import pyperclip

    def save_midi_file(track_name, time_signature, bpm, midi_text, file_path):
    try:
        mid = mido.MidiFile()
        track = mido.MidiTrack()
        mid.tracks.append(track)

        # Set track name
        track.name = track_name

        # Set time signature
        numerator, denominator = map(int, time_signature.split("/"))
        time_signature_meta = mido.MetaMessage("time_signature", numerator=numerator, denominator=denominator)
        track.append(time_signature_meta)

        # Calculate tempo from BPM
        tempo = mido.bpm2tempo(float(bpm))
        tempo_meta = mido.MetaMessage("set_tempo", tempo=tempo)
        track.append(tempo_meta)

        for line in midi_text.split("\n"):
            line = line.strip()
            if line.startswith("MetaMessage"):
                parts = line.split(",")
                if parts[0] == "MetaMessage('end_of_track'":
                    track.append(mido.MetaMessage("end_of_track", time=int(parts[1].split("=")[1].strip(")"))))
            elif line.startswith("note_on") or line.startswith("note_off"):
                parts = line.split()
                note_on = line.startswith("note_on")
                channel = int(parts[1].split("=")[1])
                note = int(parts[2].split("=")[1])
                velocity = int(parts[3].split("=")[1])
                time = int(parts[4].split("=")[1])
                if note_on:
                    track.append(mido.Message("note_on", channel=channel, note=note, velocity=velocity, time=time))
                else:
                    track.append(mido.Message("note_off", channel=channel, note=note, velocity=velocity, time=time))
            elif line.startswith("control_change"):
                parts = line.split()
                channel = int(parts[1].split("=")[1])
                control = int(parts[2].split("=")[1])
                value = int(parts[3].split("=")[1])
                time = int(parts[4].split("=")[1])
                track.append(mido.Message("control_change", channel=channel, control=control, value=value, time=time))

        # Add the .mid extension to the file path if it doesn't have one
        if not file_path.endswith(".mid"):
            file_path += ".mid"

        mid.save(file_path)
        log_text.insert(tk.END, "MIDI file saved successfully!\n")
    except Exception as e:
        log_text.insert(tk.END, f"Error occurred while saving MIDI: {str(e)}\n")

    def select_save_path():
    file_path = filedialog.asksaveasfilename(filetypes=[("MIDI files", "*.mid")])
    if file_path:
        save_midi_file(track_name_entry.get(), time_signature_entry.get(), bpm_entry.get(), text_field.get(1.0, tk.END), file_path)

    def copy_example_text():
    example_text = example_label.cget("text")
    pyperclip.copy(example_text)

    # Create the main window
    window = tk.Tk()
    window.title("MIDI Converter")

    # Configure rows and columns to expand and fill available space
    window.grid_rowconfigure(0, weight=1)
    window.grid_rowconfigure(1, weight=1)
    window.grid_rowconfigure(2, weight=1)
    window.grid_rowconfigure(3, weight=1)
    window.grid_rowconfigure(4, weight=1)
    window.grid_rowconfigure(5, weight=1)
    window.grid_rowconfigure(6, weight=1)
    window.grid_rowconfigure(7, weight=1)
    window.grid_rowconfigure(8, weight=1)
    window.grid_columnconfigure(0, weight=1)
    window.grid_columnconfigure(1, weight=1)
    window.grid_columnconfigure(2, weight=1)

    # Create the track name label and entry
    track_name_label = tk.Label(window, text="Enter track name:")
    track_name_label.grid(row=0, column=0, padx=10, pady=5, sticky=tk.W)

    track_name_entry = tk.Entry(window, width=30)
    track_name_entry.grid(row=0, column=1, padx=10, pady=5, sticky=tk.W)

    # Create the time signature label and entry
    time_signature_label = tk.Label(window, text="Enter time signature (e.g., 4/4):")
    time_signature_label.grid(row=1, column=0, padx=10, pady=5, sticky=tk.W)

    time_signature_entry = tk.Entry(window, width=30)
    time_signature_entry.grid(row=1, column=1, padx=10, pady=5, sticky=tk.W)

    # Create the BPM label and entry
    bpm_label = tk.Label(window, text="Enter BPM:")
    bpm_label.grid(row=2, column=0, padx=10, pady=5, sticky=tk.W)

    bpm_entry = tk.Entry(window, width=30)
    bpm_entry.grid(row=2, column=1, padx=10, pady=5, sticky=tk.W)

    # Create the text field
    text_field = tk.Text(window, height=10, width=60)
    text_field.grid(row=3, column=0, columnspan=2, padx=10, pady=5, sticky="nsew")

    # Create the example text
    example_text = """
    note_on channel=0 note=60 velocity=64 time=100
    note_off channel=0 note=60 velocity=0 time=50
    note_on channel=1 note=64 velocity=72 time=80
    note_off channel=1 note=64 velocity=0 time=70
    note_on channel=2 note=67 velocity=80 time=60
    note_off channel=2 note=67 velocity=0 time=90
    control_change channel=0 control=64 value=127 time=0
    control_change channel=1 control=64 value=64 time=0
    control_change channel=2 control=64 value=32 time=0
    """

    example_label = tk.Label(window, text=example_text, font=("Courier New", 10), bg="lightgray", padx=10, pady=10)
    example_label.grid(row=4, column=0, columnspan=2, padx=10, pady=5, sticky="nsew")

    # Create the log text
    log_text = tk.Text(window, height=6, width=60)
    log_text.grid(row=5, column=0, columnspan=2, padx=10, pady=5, sticky="nsew")
    log_text.insert(tk.END, """HELLO, thank you for using my text to MIDI converter
    Above you see example MIDI text that you can copy and paste
    to any Ai that is capable of providing you melodies using
    it as an EXAMPLE. For now i recommend chat-GPT.
    NOTE is note ON or OFF etc. CONTROL CHANGE is sustain pedal.
    HAVE FUN!
    \n""")

    # Create the copy example text button
    copy_button = tk.Button(window, text="Copy Example Text", command=copy_example_text)
    copy_button.grid(row=6, column=0, columnspan=2, padx=10, pady=10)
 
    # Create the save button
    save_button = tk.Button(window, text="Save MIDI File", command=select_save_path)
    save_button.grid(row=7, column=0, columnspan=2, padx=10, pady=10)

    # Start the main loop
    window.mainloop()
