from openai import OpenAI
from api_key import api_data
import os
import speech_recognition as sr
import pyttsx3
import webbrowser

Model = "GPT-4o"
client = OpenAI(api_key=api_data)

def Reply(questions):
    completion = client.chat.completions.create(
        model=Model,
        messages = [
            {'role':"system","content":"You are a helpful asistant"},
            {'role':'user','content':question}
        ],
        max_tokens = 200
    )
    answer = completion.choices[0].message.content
    return answer


# text to speech
engine = pyttsx3.init("sapi5")
voices = engine.getProperty("voices")
engine.setproperty("voice" , voices[0].id)

def speak(text):
    engine.say(text)
    engine.runAndWait()
speak("Hello How are you?")

def takeCommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening ......")
        r.pause_threshold = 1
        audio = r.listen(source)
    try:
        print("Recognizing...")
        query = r.recognize_google(audio  ,language = "en-in")
        print("User Said: {}\n".format(query))
    except Exception as e:
        print("Say that again...")
        return "none"
    return query
if __name__ == "__main__":
    while True:
        query = takeCommand().lower()
        if query == "none":
            continue
        ans = Reply(query)
        print(ans)
        speak(ans)

        if "Open youtube" in query:
            webbrowser.open("www.youtube.com")
        if "Open google" in query:
            webbrowser.open("www.google.com")
        if "bye" in query:
            break
