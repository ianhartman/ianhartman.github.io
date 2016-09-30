---
layout: post
title: Getting Started #2
---

<div class="message">
  Second post in a quick series about my homebrew python-based vfx project pipeline. 
</div>

Quick breakdown of the high-level view of my Basket Pipeline Toolset.

## Breakdown

Created using the following...

**Languages (+ Libraries):**
* Python 2.7
* PySide (Qt 4.8.5)

Works with / Extends the following...

**Software:**
* Autodesk Maya 2016.5
* NUKE 10.0v4
* Houdini 15.5

### Launching Applications

Using PySide and Python2.7 I was able to build a GUI application that the user launches using a batch script / shell script. The user then can select their Scene/Shot (within the current Show, which is set during the batch/shell script for now). They can also select which stage (Previs, Anim, FX, etc.) to launch into, the GUI also allows for a tag to search for in that shot's working directory.
*The GUI also allows for the user to create a new shot*

The application related to the respective stage is then launched with the most recent working file (with/without given tag). This causes any environment variables set in the batch / shell script to carry through to the launched application. This allows for extension of file paths in Houdini/Maya/Nuke to hook into the defined project structure... such as setting favorite directories in NUKE that go straight to the working directory for the scene/shot.

The main environment variables that need to be set are **PATH, PYTHONPATH, and NUKE_PATH.** These allow for Maya, NUKE, and my launcher to find the necessary scripts on the server. Thus I only need to keep the scripts updated on our server and every user will have access to the pipeline tools without having to worry about downloading/copying them into local directories.

### Working in Applications

With access to crucial environmant variables and a server-based project directory, I am able to treat the project directory as a lo-fi database. With a few lines of code, Maya and NUKE know exactly where to save new scripts and with a bit more code Maya can version up the files... Because adding a .#### to the end of the file name isn't a very intuitive way to iterate on a file name.

One of the best resources for NUKE implementation as been the NUKE python guide](https://www.thefoundry.co.uk/products/nuke/developers/100/pythondevguide/asset.html). They outline successful ways in which to implement some basic functionality that I have added on top of.

I have also included a NUKE-based BurnIn script that adds a BurnIn node that adds basic information onto the render. Especially important for dailies and sharing shots for review / feedback.

### Extras

I call them extras but really they are extra bits I have to include for proper usage on the lab computers. These are mainly files like install_pip.bat and install_pyside.bat which allows me to set the proper python paths and install necessary libraries.

## Last Word

I haven't refactored all my code and the repository is really a learning experience for me and I may not be doing it the best way. I need to cleanout the unecessary files that are holdovers.