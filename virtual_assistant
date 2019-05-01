import wolframalpha
import wikipedia
import wx
import pyttsx3
import speech_recognition as sr
import os

engine = pyttsx3.init()
engine.say("Hi, I am your python virtual assistant")
engine.runAndWait()

class MyFrame(wx.Frame):
    def __init__(self):
        wx.Frame.__init__(self,None,
        pos = wx.DefaultPosition, size = wx.Size(450,100),
        style = wx.MINIMIZE_BOX | wx.SYSTEM_MENU | wx.CAPTION |
        wx.CLOSE_BOX | wx.CLIP_CHILDREN,title = "Python Virtual Assistant")
        panel = wx.Panel(self)
        my_sizer = wx.BoxSizer(wx.VERTICAL)
        lbl = wx.StaticText(panel,
        label = "Hello I am the Python Virtual Assistant. How can I help you?")
        my_sizer.Add(lbl,0,wx.ALL,5)
        self.txt = wx.TextCtrl(panel,style = wx.TE_PROCESS_ENTER,size = (400,30))
        self.txt.SetFocus()
        self.txt.Bind(wx.EVT_TEXT_ENTER,self.OnEnter)
        my_sizer.Add(self.txt,0,wx.ALL,5)
        panel.SetSizer(my_sizer)
        self.Show()

    def OnEnter(self,event):
        inp = self.txt.GetValue()
        inp = inp.lower()
        if inp == '':
            r = sr.Recognizer()
            with sr.Microphone() as source:
                audio = r.listen(source)
            try:
                self.txt.SetValue(r.recognize_google(audio))
            except sr.UnknownValueError:
                print("Google speech recognition could not understand audio")
            except sr.RequestError as e:
                print("Could not request results from Google speech recognition services ".format(e))
        else:
            def broswer():
                os.system('open /Applications/Safari.app')
                engine.say("Opening Safari Web Browser")
                engine.runAndWait()
            def calculator():
                os.system('open /Applications/Calculator.app')
                engine.say("Opening Calculator")
                engine.runAndWait()
            def calendar():
                os.system('open /Applications/Calendar.app')
                engine.say("Opening Calendar")
                engine.runAndWait()
            def notes():
                os.system('open /Applications/Notes.app')
                engine.say("Opening Notes")
                engine.runAndWait()
            def whatsapp():
                os.system('open /Applications/WhatsApp.app')
                engine.say("Opening Whatsapp")
                engine.runAndWait()
            def dictionary():
                os.system('open /Applications/Dictionary.app')
                engine.say("Opening Dictionary")
                engine.runAndWait()
            def OnStart(answer):
                print(answer)
            try:
                if inp == "open browser":
                    broswer()
                elif inp == "open calculator":
                    calculator()
                elif inp == "open calendar":
                    calendar()
                elif inp == "open whatsapp":
                    whatsapp()
                elif inp == "open dictionary":
                    dictionary()
                elif inp == "open notes":
                    notes()
                else:
                    # wolframalpha
                    app_id = "A2GXTJ-6PQAA3AP7R"
                    client = wolframalpha.Client(app_id)
                    res = client.query(inp)
                    answer = next(res.results).text
                    engine.connect('started-utterance',OnStart(answer))
                    engine.say(answer)
                    engine.runAndWait()
            except:
                try:
                    #wikipedia
                    inp = inp.split(' ')
                    inp = " ".join(inp[2:])
                    answer = wikipedia.summary(inp,sentences = 2)
                    engine.connect('started-utterance',OnStart(answer))
                    engine.say(answer)
                    engine.runAndWait()
                except:
                    answer = "Sorry, there was no match "
                    engine.connect('started-utterance',OnStart(answer))
                    engine.say(answer)
                    engine.runAndWait()

if __name__ == "__main__":
    app = wx.App(True)
    frame = MyFrame()
    app.MainLoop()
