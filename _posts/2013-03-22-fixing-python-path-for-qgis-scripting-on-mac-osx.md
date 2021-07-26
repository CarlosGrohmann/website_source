---
layout: post
title: Fixing Python path for QGIS scripting on Mac OSX
author: CarlosGrohmann
date: 2013-03-22
categories: 
tags: QGIS install mac osx python
permalink: /blog/fixing-python-path-for-qgis-scripting-on-mac-osx/
published: true
---


So, QGIS 1.8 'Lisboa' is out! Lots of cool new features, and lots of fixes. Check out the oficial release [here](http://qgis.org/index.php?option=com_content&view=article&id=149).  

And since [Kyngchaos](http://www.kyngchaos.com/software/qgis) updated his Mac OSX packages, I went for an upgrade. After a clean removal of version 1.7 (using the awesome [AppCleaner](http://www.freemacsoft.net/appcleaner/)), I upgraded both the complete GDAL and QGIS.  

After installing, time to set things right. Type this in a terminal:  
`$ export DYLD_LIBRARY_PATH=/Applications/QGIS.app/Contents/MacOS/lib/:/Applications/QGIS.app/Contents/Frameworks/`  
`$ export PYTHONPATH=/Applications/QGIS.app/Contents/Resources/python/`  

Now test it:  
```
$ python  
Python 2.7.1 (r271:86832, Jun 16 2011, 16:59:05)  
[GCC 4.2.1 (Based on Apple Inc. build 5658) (LLVM build 2335.15.00)] on darwin  
Type "help", "copyright", "credits" or "license" for more information.  
>>> import qgis.core  
>>> import qgis.gui  
>>> import PyQt4.QtCore  
>>> import PyQt4.QtGui
``` 

Nice! While you're at it, set the path for you command-line GDAL programs:  
`export PATH=/Library/Frameworks/GDAL.framework/Programs:$PATH`  

Now, this will only work in the current terminal session. To make it permanent, add these lines to your `.bash_profile`
