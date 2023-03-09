# Autosplitter Creation Guide
A guide for creating a LiveSplit autosplitter/ load remover for a PC game.

This guide will focus on the specific, comprehensive steps to write an autosplitter script, centralizing information I gained from watching many different tutorials plus knowledge gained from my own experience. The [LiveSplit Autosplitters page](https://github.com/LiveSplit/LiveSplit.AutoSplitters) is a good place to go for additional information.


# Functions of a Splitter
An autosplitter works by reading the values stored by your game in your computer's memory and executing logic based on these values to affect your timer.

You can implement several capabilities for a LiveSplit timer with autosplitter script:

* **Auto start**: Automatically begin a timer (e.g. the timer starts when the player begins the first level of the game)
* **Auto split**: Automatically split, which means ending timing for one section and beginning timing for the next section (e.g. when the player starts the second level, time counted toward level 1 ends and time counted toward level 2 begins)
* **Auto end**: Automatically end a timer. Functionally this is a special case of splitting and it will generally not be distinguished from such.
* **Auto reset**: Automatically clear a timer, preparing for a timer restart.
* **Load removal**: Automatically pause the timer whenever the game is on a loading screen and resume the timer afterward
* **In-game time**: Display in-game time on the timer (as opposed to real time).


# Required Programming Knowledge
Creating an autosplitter requires very basic programming in the C# programming language. At a minimum you'll want to understand: 
* [Variables](https://www.w3schools.com/cs/cs_variables.php) 
* [Boolean expressions](https://www.w3schools.com/cs/cs_booleans.php)
* [If-else statements](https://www.w3schools.com/cs/cs_conditions.php)
* [Return statements](https://www.w3schools.com/cs/cs_method_parameters_return.php), which are used for [methods](https://www.w3schools.com/cs/cs_methods.php) but we don't need to worry about parameters or anything related to classes.

Note: you won't have to write full C# programs, just snippets of C#-like logic within the simple Auto Splitter Language used for writing autosplitter scripts.

More advanced knowledge of C# coding and software in general is helpful to have, but not strictly necessary. That being said some games require more advanced knowledge than others.


# Required Software
All tools here are free.


## LiveSplit

See [link]


## Cheat Engine
Cheat Engine is a tool that allows you to view values in memory used by a given process (e.g. a game). It also allows you to edit these values (hence the name "Cheat" Engine) but we don't need that functionality.

Download Cheat Engine directly from its [GitHub repo](https://github.com/cheat-engine/cheat-engine).

DO NOT download Cheat Engine from anywhere else as some websites package it with poopware.


## GitHub
You'll need to have a GitHub account in order to distribute your autosplitter to others through LiveSplit.



# Finding Memory Addresses for Game Values

## How to Find Values:

Watch these three videos from the Guided Hacking 100 series to learn how to scan for values in Cheat Engine: 
* [GH102](https://www.youtube.com/watch?v=_THZIUELKrw&list=PLt9cUwGw6CYHfDY-vj1AFxfWCd5r9bPd4&index=3)
* [GH103](https://youtu.be/cJLbFh_74wg)
* [GH104](https://youtu.be/NaGJXChkwGc)

**Important Note**: When adding an address to the addresslist, you may need to change its Type in order to see its value.

Example 1: you scan for a 4-Byte value and add a result to the addresslist, it may get added as type String. Double click this type value and change the Type to 4-Bytes

[Add screenshot]

Example 2: you scan for a String value and add results to addresslist. They're added as String values, but you can't see the full value or perhaps any value at all because the String's length is too small. String[14] indicates only 14 characters are being displayed. Double-click the value and change Length to something large (like 80).

![short string](https://user-images.githubusercontent.com/104397629/223780216-fdd9f981-56b4-4012-b311-0d3a46722df0.PNG)
![edit string type](https://user-images.githubusercontent.com/104397629/223780243-c6626a59-2cde-45a1-990e-1ff6b20e1539.PNG)
![edit string type post](https://user-images.githubusercontent.com/104397629/223780262-278f11f8-b56a-4353-8b77-99549f0d5e02.PNG)
![string type edited](https://user-images.githubusercontent.com/104397629/223780290-6567d1aa-f275-4b45-b6cc-72bb0ad6ab87.PNG)



## What Values to Search For
The values you need to find depend on what functions you hope to implement and what game you're working with.

For load removal, you'll want to find a true/false value (boolean) that gets set to true when the game is loading and gets sets to false when the game is not loading.
* This will often be a Byte value with value 1 while loading and value 0 while not loading.

For basic autostart and autosplit, 

## Finding Current Level Name
An address holding the name of the current level can be very useful for auto start and split for games that feature different levels.

Level names can be stored in many ways and it varies game to game and also based on what game engine the game was created with.

In the best case, scanning for the level name displayed in-game will yield a useable address. 

StarCraft II (Havok engine) is an example of this. Enter the level "Liberation Day" in game, scan for "Liberation Day" in Cheat Engine, enter the level "The Devil's Playground" in game, then find addresses whose value changed to "The Devil's Playground" in Cheat Engine:

![ce - enter devils playground](https://user-images.githubusercontent.com/104397629/223781359-9b7e3173-9407-4694-80ad-a3a83986570c.PNG)

Some games may use a different name in the code than what is displayed in the level select screen though. One trick to find these is to know where its game engine stores level files.

Unity Engine:
* Scan for String with value "Assets/Scenes/"
* Add all addresses found to the addresslist.
* Edit the Type of all these addresses to String with a very large length so that you can see the whole value (e.g. 120)
* Level file names will be shown as [LEVEL NAME].unity

Desperados III (Unity engine) has level names like "Byers Pass" and "Flagstone" displayed in-game, but scanning for level files we see internal level names like "lvl_train_00_easy" and "lvl_town_00_hard", and we have to deduce which name lines up with which level.

![byers pass](https://user-images.githubusercontent.com/104397629/223785475-aef89b8d-a797-40f1-85c0-2869c67e2e63.png)
![d3 internal level names](https://user-images.githubusercontent.com/104397629/223785524-4d9398ed-bdc1-4e51-bf49-8a6fdeedac55.PNG)



## How to Permanently Find Values: 
Most games change the memory address it stores a given value at every time you boot up the game, sometimes every time you boot up an individual level, meaning a value address you find will become invalid if you quit and restart the game. 

However, we can find something called a pointer that will lead us to the right memory address even across sessions by performing a pointer scan.

Watch [GH105](https://www.youtube.com/watch?v=rBe8Atevd-4)


# Writing an Autosplitter Script
Autosplitters are created as a script written in a simple programming language called ASL (Auto Splitter Language), which is a file that uses a .asl extension.

Description of ASL https://github.com/LiveSplit/LiveSplit.AutoSplitters#state-descriptors 



Address variable: [picture]

![Autosplitter_File_Pointer_Specification](https://user-images.githubusercontent.com/104397629/223018810-32d32c06-0a50-47c6-8a14-b254fa33e94c.PNG)


# Testing Your Autosplitter
1. Open LiveSplit
2. If you have an existing setup for the game of interest, open it. Otherwise close any other games' setup.
3. Right click the LiveSplit window > Edit Layout > click "+" > Add a Scripted Auto Splitter
4. Upload your file 
5. Some actions are toggleable. 

Game timer setting


# Sharing Your Autosplitter
1. [Create](https://github.com/new) a GitHub repository with a license. The **Creative Commons Zero v1.0 Universal** [license](https://choosealicense.com/licenses/cc0-1.0/) is recommended, but you can choose another if you wish. You can also add this license to an existing repository if you're not creating a new one or created a new one without adding a license. 
2. Upload your splitter file to this repository.
3. Add a link to your splitter file's location in LiveSplit's official list, allowing people to access your autosplitter through LiveSplit itself. See the **Adding an Auto Splitter** section of [this page](https://github.com/LiveSplit/LiveSplit.AutoSplitters#adding-an-auto-splitter).

After an autosplitter link is merged into the central repository, it should become available when you choose its associated game in LiveSplit.

Changing where you store the autosplitter will break the link stored in the LiveSplit repo, meaning your autosplitter will stop working, unless the link is also updated.


# Additional Resources

Discord for asking questions (and more tutorials): https://discord.gg/N6wv8pW

