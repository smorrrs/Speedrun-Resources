# Autosplitter Creation Guide
A guide for creating a LiveSplit autosplitter/ load remover for a game on PC.

An autosplitter works by reading the values stored by your game in your computer's memory and executing logic based on these values. For example, an autosplitter can observe the location in memory where the game store the name of the current level you're in, and can trigger a split when it detects that that value has changed (indicating you've completed one level and have moved on to the next one.)

[This page](https://github.com/LiveSplit/LiveSplit.AutoSplitters) has good information about autosplitters. This guide will focus on the exact steps needed to implement an autosplitter.


# Required Tools

## LiveSplit

## Cheat Engine
Cheat Engine is a tool that allows you to view (and edit) values in memory used by a given process (e.g. a game). 

Download Cheat Engine directly from its GitHub repo: https://github.com/cheat-engine/cheat-engine 

DO NOT download Cheat Engine from anywhere else as some websites package it with poopware.




# Finding values in Cheat Engine

## Find variables:

Watch these three videos: GH102, GH103, and GH104
https://www.youtube.com/watch?v=_THZIUELKrw&list=PLt9cUwGw6CYHfDY-vj1AFxfWCd5r9bPd4&index=3 

## Pointer scan: 

Watch GH105
https://www.youtube.com/watch?v=rBe8Atevd-4&t=332s

important!: change type


# ASL file
Autosplitters are created as a script written in a simple programming language called ASL (Auto Splitter Language), which is a file that uses a .asl extension.



Address variable: [picture]

![Autosplitter_File_Pointer_Specification](https://user-images.githubusercontent.com/104397629/223018810-32d32c06-0a50-47c6-8a14-b254fa33e94c.PNG)


# Additional Resources

Discord for asking questions: https://discord.gg/N6wv8pW

