# voice-recognition-project program
import sounddevice as sd
import speech_recognition as sr

def recognize_from_microphone():
    recognizer = sr.Recognizer()

    # Set the sample rate and duration for recording
    sample_rate = 44100
    duration = 10
    print("Say something:")
    # Record audio from the microphone
    audio_data = sd.rec(int(sample_rate * duration), samplerate=sample_rate, channels=1, dtype='int16')
    sd.wait()
    
    
    # Convert NumPy array to AudioData
    audio_data = sr.AudioData(audio_data.tobytes(), sample_rate, 2)
    print("Recognizing audio...")
    # Recognize speech from the recorded audio
    try:
        #print("Say something:")
        text = recognizer.recognize_google(audio_data, show_all=False)
        print("You said: " + text)
    except sr.UnknownValueError:
        print("Google Web Speech API could not understand audio")
    except sr.RequestError as e:
        print("Could not request results from Google Web Speech API; {0}".format(e))

# Call the function to start real-time recognition
recognize_from_microphone()
