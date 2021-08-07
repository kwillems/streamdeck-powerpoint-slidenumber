# streamdeck-powerpoint-slidenumber
## Introduction
There are several ways to control PowerPoint with a Stream Deck. But so far, no method has been published by which the slide number is displayed on the stream deck. The scripts in this repository make that possible.

Given the various differences, the way this can be accomplished is different for macOS and Windows. Therefore, different scripts are included for each of those systems. When using macOS, Keyboard Maestro is required, https://www.keyboardmaestro.com. On Windows we have to use AutoHotkey, https://www.autohotkey.com.

Basically, a PowerPoint macro saves the current slide number in a text file. That file is then read by either Keyboard Macro or AutoHotkey and then published to the Stream Deck. 
On both systems, the Stream Deck will look like this picture. 

![image stream deckpowerpoint slidenumber](https://user-images.githubusercontent.com/2992051/128610860-d135c847-7085-4fdc-9766-f427daf2f761.png)

## Installation on macOS
