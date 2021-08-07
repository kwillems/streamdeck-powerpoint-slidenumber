# streamdeck-powerpoint-slidenumber
## Introduction
There are several ways to control PowerPoint with a Stream Deck. But so far, no method has been published by which the slide number is displayed on the stream deck. The scripts in this repository make that possible.

Given the various differences, the way this can be accomplished is different for macOS and Windows. Therefore, different scripts are included for each of those systems. When using macOS, Keyboard Maestro is required, https://www.keyboardmaestro.com. On Windows we have to use AutoHotkey, https://www.autohotkey.com.

Basically, a PowerPoint macro saves the current slide number in a text file. That file is then read by either Keyboard Macro or AutoHotkey and then published to the Stream Deck. 
On both systems, the Stream Deck will look like this picture. 

![image stream deckpowerpoint slidenumber](https://user-images.githubusercontent.com/2992051/128610860-d135c847-7085-4fdc-9766-f427daf2f761.png)

## Installing the PowerPoint macro
This is the macro that neds to be executed by PowerPoint. On the **View tab**, choose **Macros**. In the Macro dialog box, type the name for the macro: **storeSlideNumber**. Hit the **+ sign** and copy and paste the following piece of code into the editor window.

This function saves the slide number in a text file called **numberSlide.txt**.
Note that the pathFile variable contains a different path for this file, depending on the operating system. On macOS, I personally prefer to store numberSlide.txt in **/usr/local/bin/**. However, I can imagine someone would prefer to store that file in their Documents folder. Then the path on macOS becomes **/Users/username/Documents/numberSlide.txt**. It goes without saying that the pathFile variable in the function below should be modified accordingly. That also applies to Windows. In the function below is, the variable pathFile is defined twice. It makes swapping between macOS and Windows easier (to me). If running under Windows one should uncomment the Windows line and comment the macOS line.

Finally, the Powerpoint presentations that use this macro must of course be saved as a PPTM file. When opening the presentation, macros must be enabled. 

For the numberSlide.txt file, use an empty text file. An example of such a file is in the repository. It must be saved to the pathFile location.

```VBScript
Sub storeSlideNumber()
    Dim slideNumber
    Dim pathFile As String
    
    'Windows
    'pathFile = "C:\Users\gebruiker\Documents\OBS\PowerPoint\numberSlide.txt"
    
    'macOS
    pathFile = "/usr/local/bin/numberSlide.txt"
    
    slideNumber = ActivePresentation.SlideShowWindow.View.Slide.SlideIndex
    Open pathFile For Output As #1
    Print #1, slideNumber
    Close #1
End Sub
```

## Installation on macOS
### Keyboard Maestro
As mentioned, macOS must use the Keyboard Maestro program. So it must be installed on your system. Download the macros nextSlide.kmmacros and previousSlide.kmmacros and double click on each of those files. They are then automatically saved to Keyboard Maestro. All you have to do is tick the checkbox "**Triggered by any of the following:**". 

Note that the action "**Read File to Variable 'slideNumber'**" uses the path as defined in pathFile. See the previous passage about the variable pathFile. 

At **button ID** you see that it says "**R2C8**", meaning row 2 and cell 8. So the number indicator is on the Stream Deck in the second row on the eighth button. Keep this in mind and change this if you want to move this button to a different location on your Stream Deck. 

<img width="1030" alt="screenshot Keyboard Maestro" src="https://user-images.githubusercontent.com/2992051/128613031-5b544004-62de-4f2c-b003-cc83009fe263.png">

### Stream Deck
An example profile for the Stream Deck is in the repository. Download that file and double click it. You also need to add two plugins to the Stream Deck app. It concerns the plugin "**Keyboard Maestro**" and the plugin "**KMLink**". You can find both in the Stream Deck Store. 

### So how does this all work in macOS?
The buttons 'previous' and 'next' call the Keyboard Maestro macros 'previousSlide' or 'nextSlide' respectively. Those macros make PowerPoint go to the previous or next slide and that slide number is stored in numberSlide.txt. The value stored therein is then read again by Keyboard Maestro and displayed on the correct button on the Stream Deck. 

I'm not a professional programmer, but you may already have noticed that. :-)
