---
layout:     post
title:      Up-to-date compile sources and headers with folder reference
date:       2016-07-21 05:00:00
summary:    Keep your compile sources and header up-to-date with git submodule folder added to the Xcode project by reference.
categories: Xcode submodule compile sources
---
### Tl;dr
Script is available [here](https://gist.github.com/Gladkov-Art/a01d8ba969e411ff36ac2518ae577757) 

## Intro
Xcode allows you to add folder to the project in 2 ways:

* group
* reference

Let go through these options, even though it is not the main topic.

### Group
The most common case. Usually it is exactly what you need. It will copy folder with content into the project preserving directory structure.

### Reference
If you choose this way, Xcode won't copy folder and content into project structure. It will only save reference to the folder. When folder's content changes you can see it in Xcode project navigation right away. 

In both ways you have an opportunity to add resources to any of your project's targets. This function is quite useful because it adds sources to the "Compile sources" build phase automatically.  

## Why should I care?
Some of you might asking this fair question, why do I even need to add something by reference?  Not too far ago, I've encountered situation where reference way is exactly what I needed. 
The situation was not very ordinary, our team developed iOS application, that is using C module to communicate with embedded devices. This C module was added to the project as submodule. So, this module was located right next to the project folder. And I had to make a choose, add it as group and on every submodule update go though each file and copy new ones. Or add submodule folder as reference and see actual files in project navigator, but still manually add new ones to the target. Really terrifying perceptive. Lazy hackers hate routines, you know.

# Solution
The solution I've found is to add submodule folder as reference and use homegrown Ruby script that is responsible for adding new files from referenced folder to "Compile sources" and "Headers" build phases.

Script is available [here](https://gist.github.com/Gladkov-Art/a01d8ba969e411ff36ac2518ae577757) 

I've decided not to go the hard way and choose [Xcodeproj](https://github.com/CocoaPods/Xcodeproj) to read and modify project file. So to use my script make sure that you have Xcodeproj installed.

P.S. If any ruby developer will take a look at source code, I will be really ashamed. Any fixes and recommendations are highly appreciated.
