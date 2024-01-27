import sounddevice as sd
import numpy as np
import keyboard
import time

def record_audio(callback, duration=10, samplerate=44100):
    with sd.InputStream(callback=callback, channels=1, samplerate=samplerate):
        sd.sleep(int(duration * 1000))

def candle_blow_callback(indata, frames, time, status):
    volume_norm = np.linalg.norm(indata) * 10
    if volume_norm > 1.5:  # Adjust this threshold based on your microphone sensitivity
        print("Candle blown! 🎉")
        keyboard.press_and_release('b')  # Simulate pressing 'b' key

if __name__ == "__main__":
    print("Blow on the microphone to simulate blowing the candle. Press 'q' to quit.")
    record_audio(callback=candle_blow_callback)

    while True:
        if keyboard.is_pressed('q'):
            print("Exiting the birthday card. Bye!")
            break
        time.sleep(0.1)

