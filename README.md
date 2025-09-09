# Display-GTK-demo

A demo with a python based GTK application for the Moduline Display (av101hdt-a10)

## The demo

The demo is meant to demonstrate some concepts that can be used to develop  
graphical applications for the Moduline display.  
Because it is a regular Debian systems there are a lot GUI toolits available:  
GTK, QT, LVGL, Makepad, Slint, Electron/Web, Flutter, Crank Storyboard...  

This demo shows how to run a GTK application in the Cage wayland compositor but  
Cage can also be used for other GUI toolkits. Some toolkits like Crank Storyboard  
enable rendering without Wayland or X11 through the KMS interface directly.  

## Removing the demo
```
apt purge go-gtk-demo
apt autoremove
```
## What is what

gtk_demo is the python GTK application  
gocontroll_demo is the companion simulink model  
98-fix.rules is a udev rule that rotates the touch input 180 degrees  
in gtk_demo wlr-randr is used to rotate the display output itself  
root contains user authentication required by cage, the filename is the username  
debian/cage@.service is responsible for launching the GUI  
debian/gocontroll_demo.service is responsible for launching the demo simulink application  

## Points of note

This demo uses the pyuio package to read and write the Simulink models virtual memory.  
It is however not entirely recommended, this approach has two downsides:  

1. The GUI now has to run under the root user for the correct permissions  
2. Read and write access is not synchronized  

However it also has some advantages:

1. No need to set up your own IPC protocol
2. Infrastructure is present by default in Simulink

When using Crank Storyboard, there is a companion [Simulink blockset](https://github.com/GOcontroll/GOcontroll-Simulink-Crank-Storyboard) to provide the IPC.  
However this toolkit requires a paid license to use.

This application is in no means a display of best practices but merely a demonstration of  
an application running in a wayland compositor and how that is done.
