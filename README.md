# Voice-Assistant-app
Voice assistant app using python code 


import speech_recognition as sr
import pyttsx3

# Initialize recognizer and engine
recognizer = sr.Recognizer()
engine = pyttsx3.init()

# Function to convert text to speech
def speak(text):
    engine.say(text)
    engine.runAndWait()

# Function to listen for commands
def listen():
    with sr.Microphone() as source:
        print("Listening...")
        recognizer.adjust_for_ambient_noise(source)
        audio = recognizer.listen(source)
        
        try:
            command = recognizer.recognize_google(audio)
            print("You said:", command)
            return command.lower()
        except sr.UnknownValueError:
            print("Could not understand audio")
            return ""
        except sr.RequestError as e:
            print("Error fetching results; {0}".format(e))
            return ""

# Main function
if __name__ == "__main__":
    speak("Hello! I am your voice assistant. How can I help you today?")
    
    while True:
        command = listen()
        
        if "hello" in command:
            speak("Hello there! How can I assist you?")
        elif "how are you" in command:
            speak("I'm great, thanks for asking!")
        elif "goodbye" in command or "bye" in command:
            speak("Goodbye!")
            break
        else:
            speak("Sorry, I didn't catch that. Could you repeat?")
