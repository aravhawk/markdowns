# Music Gen Example Using ChatGPT
## Source Code
#### This code was written with the help of ChatGPT, thus it is "Using ChatGPT". The key is finding the right prompt.
```python
import numpy as np
from scipy.io.wavfile import write

def generate_sine_wave(frequency, duration, sample_rate=44100, amplitude=0.5):
    t = np.linspace(0, duration, int(sample_rate * duration), endpoint=False)
    wave = amplitude * np.sin(2 * np.pi * frequency * t)
    return wave

def generate_drum_sound(drum_type, duration, sample_rate=44100, amplitude=0.5):
    if drum_type == 'kick':
        wave = generate_sine_wave(100, duration, sample_rate, amplitude)
    elif drum_type == 'snare':
        noise = amplitude * (2 * np.random.random(int(sample_rate * duration)) - 1)
        envelope = np.linspace(1, 0, int(sample_rate * duration))
        wave = noise * envelope
    return wave

def compose_music(sound_list, sample_rate=44100, amplitude=0.5):
    music = []
    for sound_type, duration in sound_list:
        if sound_type in ['kick', 'snare']:
            wave = generate_drum_sound(sound_type, duration, sample_rate, amplitude)
        music.append(wave)
    return np.concatenate(music)

def save_music(filename, music, sample_rate=44100):
    music = np.int16(music / np.max(np.abs(music)) * 32767)
    write(filename, sample_rate, music)

sound_list = [
    ('kick', 0.5), ('snare', 0.5), ('kick', 0.5), ('snare', 0.5),
    ('kick', 0.5), ('snare', 0.5), ('kick', 0.5), ('snare', 0.5),
    ('kick', 0.5), ('snare', 0.5), ('kick', 0.5), ('snare', 0.5),
    ('kick', 0.5), ('snare', 0.5), ('kick', 0.5), ('snare', 0.5),
    ('kick', 0.5), ('snare', 0.5), ('kick', 0.5), ('snare', 0.5)
]

music = compose_music(sound_list)
save_music('10_second_drum_beat.wav', music)
print("10-second drum beat generated and saved as '10_second_drum_beat.wav'")
```
## Usage Instructions
- Make sure you have `numpy` and `scipy` installed, using `pip3`
- Simple installation command: `pip3 install -q -U numpy scipy`
- Open a terminal and run `python3`
- Copy the above code, paste it there, and press enter
