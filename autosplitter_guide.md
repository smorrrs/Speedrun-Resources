# Autosplitter Creation Guide
A guide for creating a LiveSplit autosplitter/ load remover for a PC game.

This guide will focus on the steps to write an autosplitter script.
[This page](https://github.com/LiveSplit/LiveSplit.AutoSplitters) has good information about other aspects of autosplitters (making them available to others, making a splitter for a console game, etc.)


# Functions of a Splitter
An autosplitter works by reading the values stored by your game in your computer's memory and executing logic based on these values. 

You can implement several capabilities for a LiveSplit timer with autosplitter script. The basic ones:

* Auto start: Automatically begin a timer (e.g. the timer starts when the player begins the first level of the game)
* Auto split: Automatically split, or end timing for one section and begin timing for the next section (e.g. when the player starts the second level, time counted toward level 1 ends and time counted toward level 2 begins)
* Load removal: Automatically pause the timer whenever the game is on a loading screen and resume the timer afterward


# Required Software
All tools here are free.


## LiveSplit

See [link]


## Cheat Engine
Cheat Engine is a tool that allows you to view values in memory used by a given process (e.g. a game). It also allows you to edit these values (hence the name "cheat engine") but we don't need to do that.

Download Cheat Engine directly from its GitHub repo: https://github.com/cheat-engine/cheat-engine 

DO NOT download Cheat Engine from anywhere else as some websites package it with poopware.


## GitHub
You'll need to have a GitHub account 



# Finding Memory Addresses for Game Values

## How to Find Values:

Watch these three videos from the Guided Hacking 100 series: 
* GH102: https://www.youtube.com/watch?v=_THZIUELKrw&list=PLt9cUwGw6CYHfDY-vj1AFxfWCd5r9bPd4&index=3 
* GH103: 
* GH104: 


## What Values to Search For
The values you need to find depend on 

For a simple load remover, 

For basic autostart and autosplit, 

Find level names:
Depends on what engine the game is created in.

Unity Engine:
* Scan for String where value = "Assets/Scenes/"
* Add all addresses found to the addresslist.
* Edit the Type of all these addresses to String with a very large length so that you can see the whole value (e.g. 120)
* Level file names will be shown as [LEVEL NAME].unity


## Pointer scan: 

Watch GH105
https://www.youtube.com/watch?v=rBe8Atevd-4&t=332s

important!: change type


# Writing an ASL File
Autosplitters are created as a script written in a simple programming language called ASL (Auto Splitter Language), which is a file that uses a .asl extension.



Address variable: [picture]

![Autosplitter_File_Pointer_Specification](https://user-images.githubusercontent.com/104397629/223018810-32d32c06-0a50-47c6-8a14-b254fa33e94c.PNG)


# Additional Resources

Discord for asking questions (and more tutorials): https://discord.gg/N6wv8pW

