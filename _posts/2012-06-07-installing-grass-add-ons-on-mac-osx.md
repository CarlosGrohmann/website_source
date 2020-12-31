---
layout: post
title: Installing GRASS Add-Ons on Mac OSX
author: CarlosGrohmann
date: 2012-06-07
categories: 
tags: GRASS install mac
permalink: /blog/installing-grass-add-ons-on-mac-osx/
published: true
---

After some searching and asking on the GRASS mailing list, I found a good way to install the GRASS add-ons on my OSX Lion. On William Kyngesburye's [page](http://www.kyngchaos.com/software/grass), we find this note: 

> **Addon Modules** Included is a build template similar to the GEM system for modules. But it doesn't require the module source to be configured for GEM (I haven't seen any that are yet). It's a bit rough. See the included readme for details.

But there's not much more. There is a nice [topic](http://www.forumsig.org/showthread.php?t=33173) in the french forumSIG, but you need to be registered in order to see the pictures. So I decided to post the instructions here.  

First you need to install XCode from the AppleStore and the CLI (command line interface) tools. (the CLI tools can be installed from XCode preferences). Next, fix the SDKs path: findo the Xcode.app, right-click over it and choose **Show package contents**. Now go to **Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs** and copy **MacOSX10.7.sdk** to **/Developer/SDKs** (you might need to create this folder).  

Then, download and install KyngChaos' [package](http://www.kyngchaos.com/files/software/grass/GRASS-6.4.2-3-Snow.dmg). It will create a directory for your GRASS version under **/Library**. Since the directory is read-only, we need to copy the **modbuild** sub-directory to another place. In my case, I copied it to **/Users/guano/Documents/installs/grass/modbuild**   

![](/img/addons1.png){:width="70%"}    

Now we put the directory of the module we want to compile under the **module** subdir of our new modbuild directory (I'm using **r.stream.order** here).   

![](/img/addons2.png){:width="70%"}    

Open the Terminal and go to the module's directory, in my case **/Users/guano/Documents/installs/grass/modbuild/module/r.stream.order**, and run this (it's a single line command): 

`> make GRASS_HOME='/Users/guano/Documents/installs/grass/modbuild/module/r.stream.order' GRASS_APP='/Applications/GRASS-6.4.app'`


![](/img/addons3.png){:width="70%"}   

just make sure that GRASS_HOME points to your module's directory (you can drag the folder from Finder in the Terminal and it will give you the full path to it). After the compilation ends, you should have a directory named **dist.i386-apple-darwin10.7.0** under your module's directory (if you are on Lion. If you run an older version of OSX, the "10.X" part will reflect your system's version). Now you just copy the relevant files to **/Library/GRASS/6.4/Modules/**: copy the executable under **bin** to **/Library/GRASS/6.4/Modules/bin** and the files under **html** to **/Library/GRASS/6.4/Modules/doc/html**.  

![](/img/addons4.png){:width="70%"}   

Now you should be able to run the add-on via the GRASS terminal:   

![](/img/addons5.png){:width="70%"}   

Nice, huh?



#### Comments


**[Manuel](#24 "2012-06-23 12:53:25"):** Nice indeed. However I am getting trouble compiling because it complains on some dependencies while compiling your very same module. The error is the following: ld: warning: directory not found for option '-L/Users/Shared/unix/pgsql-pq-snow/usr/local/pgsql-9.1/lib' ld: duplicate symbol \_main in OBJ.i386-apple-darwin11.3.0/prueba.o and OBJ.i386-apple-darwin11.3.0/main.o for architecture i386 collect2: ld returned 1 exit status ld: warning: directory not found for option '-L/Users/Shared/unix/pgsql-pq-snow/usr/local/pgsql-9.1/lib' ld: duplicate symbol \_main in OBJ.i386-apple-darwin11.3.0/prueba.o and OBJ.i386-apple-darwin11.3.0/main.o for architecture x86_64 collect2: ld returned 1 exit status Have you had this problem also? Any idea on how to overcome it? Thank you a lot for your post


**[carlosgrohmann](#25 "2012-06-24 15:29:30"):** Hi there. It seems your errors are related to PostgreSQL (the 'pgsql' part). Try installing it and see if it works. I can't really tell from experience, since I installed all GRASS dependencies via macports (I also run GRASS' development version). According to PostgreSQL's page, the OSX package contains the C libraries, so it should be what you need. here: http://www.postgresql.org/download/macosx/ hope that helps!


**[Marcello](#26 "2012-09-13 20:46:16"):** Caro professor Carlos, faz apenas alguns dias que eu comprei meu MacBook. Gostaria de saber como é o procedimento para baixar as dependências através do MacPorts (é similar ao home brew?), você teria algum passo a passo referente ao GRASS para isso? outra dúvida, caso haja algum problema na instalação, como eu verifico? estou habituado a compilar o GRASS no Ubuntu, mas no Mountain Lion eu estou completamente perdido! (e quase jogando ele no chão, rs). Um abraço e parabéns pelo seu excelente Post!


**[carlosgrohmann](#27 "2012-09-14 21:01:49"):** Caro Marcello, O Mac Ports é bem legal e cuida de todas as dependências pra você. Um simples `sudo port install grass` dever ser suficiente. Quando eu compilei o GRASS 7 no meu Mac, o processo de instalar as dependências foi um pouco manual. Eu rodava meu ./configure e a cada erro, instalava a dependência até não ter mais erros. Ultimamente tenho preferido usar o pacote pronto do William Kyngesburye. Ele tem pacotes do GRASS 6.4, QGIS 1.8 e das dependências (GDAL, FreeType etc). Funciona perfeitamente. http://www.kyngchaos.com/software/grass abraços Carlos


**[Brian Miles](#28 "2013-02-01 16:26:23"):** Thanks so much for putting this together. I can't tell you how much time I wasted before finding this. Thank you!!! I made the following makefile to make it easy to copy the executable and HTML into the correct place (see the "deploy" target): MODULE_TOPDIR = ../.. GRASS_VERSION_STR = 6.4 PGM = r.findtheriver LIBES = $(GISLIB) DEPENDENCIES = $(GISDEP) include $(MODULE_TOPDIR)/include/Make/Module.make default: cmd deploy: cp dist.*/bin/$(PGM) /Library/GRASS/$(GRASS_VERSION_STR)/Modules/bin cp dist.*/docs/html/* /Library/GRASS/$(GRASS_VERSION_STR)/Modules/docs/html



