---
layout: post
title: Working with GRASS-7.0 and homebrew python on OS X
author: CarlosGrohmann
date: 2015-12-25
categories: 
tags: SIG grass osx mac python homebrew install 
permalink: /blog/grass-brew-python-osx/
published: true
---


Sometimes getting all the software you need for Scientific analysis updated and running smoothly in OS X can be a bit annoying. For most things, there's Homebrew (a nice post on setting your Mac for Scientific analysis with Python and homebrew is [this one](https://joernhees.de/blog/2014/02/25/scientific-python-on-mac-os-x-10-9-with-homebrew/).) And if you're into GIS, you probably know William Kyngesburye's [QGIS and GRASS packages](http://www.kyngchaos.com/software/unixport). Michael Barton also provides [GRASS packages](http://grassmac.wikidot.com), including the last stable version (7.0.2 at this moment). All seems good, but I started to have some problems because I wanted to have my Python stuff (Numpy, Scipy, Matplotlib, etc) updated via homebrew (to keep system python untouched) and then I tried to compile GRASS and QGIS with homebrew as well, but that didn't worked out so well. The [osgeo4mac formulas](https://github.com/OSGeo/homebrew-osgeo4mac) for 'brewing' QGIS are still for version 2.8 (the last stable is 2.12) and there is a ['tap' for GRASS 7](https://github.com/rkrug/homebrew-head-only), but despite compiling ok, I couldn't get 3D viewing to work. Eventually I managed to get all working. This is how:  



  1. Install python, numpy, scipy, matplotlib via homebrew.

  2. Install Michael Barton's frameworks and GRASS 7.

  3. Install QGIS from William Kyngesburye.

  4. Edit your [`.bash_profile`](http://osxdaily.com/2015/07/28/set-enviornment-variables-mac-os-x/).

The last part is the tricky one. Homebrew install everything under **/usr/local**, and this needs to be in your PATH. The usual approach is to add this line to `.bash_profile`:   

`export PATH=/usr/local/bin:$PATH`    

Doing this will make homebrew's python the one to be called if you type 'python' in a terminal window. But it will also change which python GRASS and QGIS will use. The thing is that both GRASS and QGIS packages are made to use OS X system python, not the one you installed with homebrew. The trick is to set a GRASS_PYTHON variable in **.bash_profile**, pointing to system python. 

`export GRASS_PYTHON=/System/Library/Frameworks/Python.framework/Versions/Current/bin/pythonw`   

Now, the really tricky thing is that GRASS_PYTHON must be called **before** setting the path for homebrew. So when you start GRASS, it will find the right python. Like this:   

```
export GRASS_PYTHON=/System/Library/Frameworks/Python.framework/Versions/Current/bin/pythonw

export PATH=/usr/local/bin:$PATH
```  

This got my setup working fine, with 3D view and all. And if you want to use homebrew's python for analysis inside GRASS (with pygrass) you just have to call `/usr/local/bin/python` from GRASS' terminal.

