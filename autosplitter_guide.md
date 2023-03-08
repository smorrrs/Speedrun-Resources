# Autosplitter Creation Guide
A guide for creating a LiveSplit autosplitter/ load remover for a PC game.

This guide will focus on the specific, comprehensive steps to write an autosplitter script.
[This page](https://github.com/LiveSplit/LiveSplit.AutoSplitters) has good information about other aspects of autosplitters (making them available to others, making a splitter for a console game, etc.)


# Functions of a Splitter
An autosplitter works by reading the values stored by your game in your computer's memory and executing logic based on these values to affect your timer.

You can implement several capabilities for a LiveSplit timer with autosplitter script. The basic ones:

* Auto start: Automatically begin a timer (e.g. the timer starts when the player begins the first level of the game)
* Auto split: Automatically split, which means ending timing for one section and beginning timing for the next section (e.g. when the player starts the second level, time counted toward level 1 ends and time counted toward level 2 begins)
* Auto end: Automatically end a timer. Functionally this is the same as split and it will often not be distinguished from such.
* Load removal: Automatically pause the timer whenever the game is on a loading screen and resume the timer afterward


# Required Software
All tools here are free.


## LiveSplit

See [link]


## Cheat Engine
Cheat Engine is a tool that allows you to view values in memory used by a given process (e.g. a game). It also allows you to edit these values (hence the name "cheat") but we don't need that.

Download Cheat Engine directly from its [GitHub repo](https://github.com/cheat-engine/cheat-engine)

DO NOT download Cheat Engine from anywhere else as some websites package it with poopware.


## GitHub
You'll need to have a GitHub account in order to distribute your autosplitter to others through LiveSplit.



# Finding Memory Addresses for Game Values

## How to Find Values:

Watch these three videos from the Guided Hacking 100 series to learn how to scan for values in Cheat Engine: 
* [GH102](https://www.youtube.com/watch?v=_THZIUELKrw&list=PLt9cUwGw6CYHfDY-vj1AFxfWCd5r9bPd4&index=3)
* [GH103](https://youtu.be/cJLbFh_74wg)
* [GH104](https://youtu.be/NaGJXChkwGc)

Important Note: When adding an address to the addresslist, you may need to change its Type in order to see its value.

Example 1: you scan for a 4-Byte value and add a result to the addresslist, it may get added as type String. Double click this type value and change the Type to 4-Bytes

[Add screenshot]

Example 2: you scan for a String value and add results to addresslist. They're added as String values, but you can't see the value. This may be because the String's length is too small. If it shows String[0], it's displaying 0 characters. Double-click the type value and change Length to something large (like 120).

[Add screenshot]


## What Values to Search For
The values you need to find depend on what functions you hope to implement and what game you're working with.

For load removal, you'll want to find a true/false value (boolean) that gets set to true when the game is loading and gets sets to false when the game is not loading.
* This will often be a Byte value with value 1 while loading and value 0 while not loading.

For basic autostart and autosplit, 


Find level names:
Depends on what engine the game is created in.

Unity Engine:
* Scan for String where value = "Assets/Scenes/"
* Add all addresses found to the addresslist.
* Edit the Type of all these addresses to String with a very large length so that you can see the whole value (e.g. 120)
* Level file names will be shown as [LEVEL NAME].unity


## How to Permanently Find Values: 
Most games change the memory address it stores a given value at every time you boot up the game, sometimes every time you boot up an individual level, meaning a value address you find will become invalid if you quit and restart the game. 

However, we can find something called a pointer that will lead us to the right memory address even across sessions by performing a pointer scan.

Watch [GH105](https://www.youtube.com/watch?v=rBe8Atevd-4)

important!: change type


# Writing an Autosplitter Script
Autosplitters are created as a script written in a simple programming language called ASL (Auto Splitter Language), which is a file that uses a .asl extension.



Address variable: [picture]

![Autosplitter_File_Pointer_Specification](https://user-images.githubusercontent.com/104397629/223018810-32d32c06-0a50-47c6-8a14-b254fa33e94c.PNG)


# Testing Your Autosplitter

Game timer setting


# Sharing Your Autosplitter
You can add a link to your autosplitter file to LiveSplit's list of autosplitter files, allowing people to access your autosplitter through LiveSplit itself.

See this page [link]


# Additional Resources

Discord for asking questions (and more tutorials): https://discord.gg/N6wv8pW

