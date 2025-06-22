pip install SpeechRecognition pyttsx3 pyaudio
import speech_recognition as sr

import pyttsx3

import datetime

import webbrowser

# Initialize engines

recognizer = sr.Recognizer()

engine = pyttsx3.init()

engine.setProperty('rate', 150) # Speed of speech

def speak(text):

 print(f"Mark: {text}")

 engine.say(text)

 engine.runAndWait()

def greet():

 hour = datetime.datetime.now().hour

 if 5 <= hour < 12:

 speak("Good morning! I am Mark, your assistant. How can I help you?")

 elif 12 <= hour < 18:

 speak("Good afternoon! I am Mark, your assistant. How can I help you?")

 else:

 speak("Good evening! I am Mark, your assistant. How can I help you?")

def listen_command():

 with sr.Microphone() as source:

 print("Listening...")

 recognizer.adjust_for_ambient_noise(source)

 audio = recognizer.listen(source)

 try:

 command = recognizer.recognize_google(audio)

 print(f"You said: {command}")

 return command.lower()

 except sr.UnknownValueError:

 speak("Sorry, I didn't understand. Could you repeat that?")

 return ""

 except sr.RequestError:

 speak("Sorry, my speech service is down.")

 return ""

def handle_command(command):

 if "your name" in command:

 speak("My name is Mark, your personal voice assistant.")

 elif "time" in command:

 now = datetime.datetime.now().strftime("%H:%M")

 speak(f"The current time is {now}")

 elif "open youtube" in command:

 speak("Opening YouTube.")

 webbrowser.open("https://www.youtube.com")

 elif "play music" in command:

 speak("Opening YouTube Music.")

 webbrowser.open("https://music.youtube.com")

 elif "open whatsapp" in command:

 speak("Opening WhatsApp Web.")

 webbrowser.open("https://web.whatsapp.com")
 elif "call" in command:

 name = command.replace("call", "").strip()

 if name:

 speak(f"Calling {name} on WhatsApp... Please scan the QR code if not logged in.")

 else:

 speak("Whom should I call? Please say the name.")

 elif "stop" in command or "exit" in command or "bye" in command:

 speak("Goodbye! Have a great day!")

 exit()

 else:

 speak("Sorry, I can't help with that yet.")

def main():

 greet()

 while True:

 command = listen_command()

 if command:

 handle_command(command)

if __name__ == "__main__":

 main()
