---
layout: post
title: Some thoughts on a fresh install of gvSIG
author: CarlosGrohmann
date: 2010-11-05
categories: 
tags: SIG gvsig install
permalink: /blog/some-thoughts-on-a-fresh-install-of-gvsig/
published: true
---


I just did a fresh install of the just-released [gvSIG 1.10](http://www.gvsig.org/web/projects/gvsig-desktop/official/gvsig-1.10/). This is a nice Free and Open Source Software (FOSS) GIS that is written in java, so it runs pretty much anywhere, even from a flash drive. So I downloaded the installer, set up the execution permission (I'm on Linux) and run it. Te first thing the installer asks you is about the Java Runtime Environment (JRE). I only had two choices (the other two were unavailable): selecting a JRE already present in my machine or install a JRE ready to use **in my home directory** (this is the recommended option). Hey, gvSIG devs: I don't want that JRE in my HOME directory. I'd like to have it somewhere else, in a place **I** can choose (not you guys). Turns out i only realized this after I completed the install, so I went and deleted the directory with the binaries (for this one I can choose the location...) and move the folder with the JRE to another place, and did a second install selecting a pre-existent JRE. OK, done. Yeah, right.    

![](/img/gvsig_install11.png){:width="70%"}    

After the installation completed, of course I started the program. Now... besides creating the /home/you/gvSIG with the JRE (unless you change thing by hand0, when the program starts, it creates **two** new directories under you home dir. One called gvSIG (which will be the same as the JRE) and one for the Sextante extensions. Now, devs... again: _I. Don't. Want. This._ I want to _choose_ where this thing go. I have a 'gisworks' dir just for that. I would happily have a 'gvSIGworks' _under_ 'gisworks', but not above it. Looking the gvSIG.sh file, I found no way of altering the location of these directories. That sucks.   In the end, these thing only drive me away from the software. I know this is a good GIS program, but I have my way of working, and I don't want to change a lot of things now. So, gvSIG developers: PLEASE, give us the ability to choose _where_ we want the directories. Don't force your decisions on us.



#### Comments

**[Jorge](#17 "2010-11-06 12:58:33"):** I agree that this behavior is a PITA. I also like to have everything in place, but well is up to you if you don't want to use a soft because of this (specially in linux where you can do symlinks easily). You can install gvSIG without JRE, and select manually witch one to use, one of your defaults or anywhere, as you know if you've seen the bash script. Anyway I see a lot of room for improvement here and it should be easy to implement (but I could be wrong). I will add your idea to the CodeSprint wiki for next gvSIG conf, just in case anyone wants to work on that side. http://www.doowikis.com/m/Jy3H1rZ7AP Best Jorge

**[Jorge](#18 "2010-11-06 13:33:48"):** ups sorry s/witch/which/g :-)

**[carlosgrohmann](#19 "2010-11-08 07:59:33"):** Thank you for your comments, Jorge. I agree that this is not a motive to not use the software. Its just that I like to have everythinhg organized, so I don't like to have 'extra' directories in my /home. Thank you for adding this to the CodeSprint. Allowing the user to customize a bit more the installation will be a great improvement, IMO. best Carlos



