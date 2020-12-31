---
layout: post
title: Installing Orfeo Toolbox and Monteverdi on OSX
author: CarlosGrohmann
date: 2016-05-13
categories: 
tags: osx mac install remote-sensing
permalink: /blog/installing-orfeo-toolbox-and-monteverdi-on-osx/
published: true
---

The Orfeo ToolBox (OTB) is an open-source C++ library for processing of remote sensing image, and it is shipped with Monteverdi, an end-users oriented software for for classical remote sensing tasks. With the recent release of OTB version 5.4, I decided to make this brief post on how to get it running on OSX. I'm running El Capitan (10.11), but it should be the same for other versions.    

First, go to <https://www.orfeo-toolbox.org/download/> and select "Mac OS X". Right-click and select "Save link as". I ended with a file named `OTB-5.4.0-Darwin64.run.txt`. Rename that file and remove the ".txt" extension (if you will get a warning from the system, just select "keep .run").  

Now you must give this file [execution permission](https://en.wikipedia.org/wiki/File_system_permissions). You can't do that with the Graphical Interface (GUI), so you must use the [Command Line Interface](https://en.wikipedia.org/wiki/Command-line_interface). Open the Terminal (it's probably in Applications/Utilities) and navigate to the directory where you saved the file, or, in GUI terms, go to the Folder where the file is. So if your file is in Downloads:  

`Serenity:~ guano$ cd Downloads/`  

In this case, "Serenity" is the name of my computer, and "guano" is my username (yours will be different). the command [cd](http://ss64.com/osx/cd.html) means `c`hange `d`irectory and there is a space between it and the name of the Directory (Folder) you want to go. Another way of doing this is to write cd (and a space) and drag the folder from a Finder window over the Terminal window. Hit return and you are inside the Downloads directory.  

Check to see if the file is there with the [ls](http://ss64.com/osx/ls.html) command:  

`Serenity:Downloads guano$ ls
OTB-5.4.0-Darwin64.run`

Now give it execution permission with the [chmod](http://ss64.com/osx/chmod.html) command:  

`Serenity:Downloads guano$ chmod +x OTB-5.4.0-Darwin64.run `  

Ok, now move (or copy) the file to a place where it will be installed. You can install it in the system-wide Applications folder (/Applications) or in your user's Applications (/Users/your_user/Applications). You can drag the file to the folder or continue doing thing on the command line:  

`Serenity:Downloads guano$ mv OTB-5.4.0-Darwin64.run /Applications`  

This will move the file to the Applications folder that's under the [root](http://www.linfo.org/root.html) of the FileSystem (/Applications).  

Now navigate to that folder and run the installer (note the single dot before the slash when running the installer):  

```
Serenity:Downloads guano$ cd ../Applications
Serenity:Applications guano$ ./OTB-5.4.0-Darwin64.run
Creating directory OTB-5.4.0-Darwin64
Verifying archive integrity... All good.
Uncompressing OrfeoToolBox 5.4.0 100%
Configuring...
Serenity:Applications guano$
```

The installer will deflate and create a directory called `OTB-5.4.0-Darwin64`, and inside it you will find two apps: `Mapla.app` and `Monteverdi.app`. If you like to use LaunchPad (like me), just hit F4 and they will be there.  

&nbsp;

![](/img/Screen-Shot-2016-05-13-at-11.44.15.png){:width="20%"}  
Mapla window (Monteverdi Application Laucher)  

&nbsp;

![](/img/Screen-Shot-2016-05-13-at-11.44.00.png){:width="60%"}  
Main Monteverdi window  

&nbsp;

That's it. Happy Processing!  


#### Comments

**[Juan Manuel Lopez](#18926 "2018-10-01 16:06:16"):** Last login: Mon Oct 1 20:42:23 on ttys000 MacBook-Air-de-Juan:~ Juancho08$ cd Applications/OTB-6.6.0-Darwin64.run -bash: cd: Applications/OTB-6.6.0-Darwin64.run: No such file or directory MacBook-Air-de-Juan:~ Juancho08$ cd Applications/ MacBook-Air-de-Juan:Applications Juancho08$ ./OTB-6.6.0-Darwin64 -bash: ./OTB-6.6.0-Darwin64: No such file or directory MacBook-Air-de-Juan:Applications Juancho08$ ./OTB-6.6.0-Darwin64.run -bash: ./OTB-6.6.0-Darwin64.run: No such file or directory MacBook-Air-de-Juan:Applications Juancho08$ I appear this error knows what can it be? Thank you very much and greetings  

**[Carlos Grohmann](#18927 "2018-10-01 16:15:06"):** Hello Juan It can be a number of things. The error you are seeing means that your system couldn't find the file, so you probably are trying to run it from the wring place. First, be sure of where you copied the OTB-6.6.0-Darwin64.run file, if it was to `/Applications` or if it was to `/Users/your_user/Applications`. Then navigate to that directory in the command line using cd (`cd /Applications` or cd `/Users/your_user/Applications`). From there try to execute the OTB-6.6.0-Darwin64.run file. Also remember to give it permission to be executed (the `chmod` part of the post). best Carlos



