# python-voice-assistant
import speech_recognition as sr
import pyttsx3
 
# Initialize the recognizer and engine
recognizer = sr.Recognizer()
engine = pyttsx3.init()

# Function to convert text to speech
def speak(text):
    engine.say(text)
    engine.runAndWait()

# Function to listen to user's voice
def listen():
    with sr.Microphone() as source:
        print("Listening...")
        recognizer.adjust_for_ambient_noise(source)
        audio = recognizer.listen(source)

        try:
            text = recognizer.recognize_google(audio)
            print("You said:", text)
            return text
        except sr.UnknownValueError:
            print("Sorry, I could not understand your voice.")
            return ""
        except sr.RequestError:
            print("Sorry, I'm unable to process your request at the moment.")
            return ""

# Main loop
while True:
    command = listen().lower()

    if "hello" in command:
        speak("Hello! How can I assist you?")
    elif "goodbye" in command:
        speak("Goodbye! Have a nice day.")
        break
    else:
        speak("Sorry, I couldn't recognize that command. Could you please repeat?")
