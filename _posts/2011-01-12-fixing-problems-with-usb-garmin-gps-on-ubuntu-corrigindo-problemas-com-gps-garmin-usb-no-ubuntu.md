---
layout: post
title: Fixing problems with USB Garmin GPS on Ubuntu - Corrigindo problemas com GPS Garmin USB no Ubuntu
author: CarlosGrohmann
date: 2011-01-12
categories: 
tags: linux garmin
permalink: /blog/fixing-problems-with-usb-garmin-gps-on-ubuntu-corrigindo-problemas-com-gps-garmin-usb-no-ubuntu/
published: true
---


[EN] After my last caving expedition, I had some problems to download my GPS data with QGIS/Gpsbabel. I found out that it was a problem with Ubuntu udev rules. Here's how to fix that.  

[PT-BR] Após a última expedição de exploração espeleológica, tive problemas para baixar os dados do meu GPS Garmin usando QGIS/Gpsbabel. Decobri se tratar de um problema com o Ubuntu, que não me dava o devido acesso ao dispositivo. Veja como corrigir esse problema.  

**1 - Determine if this is your problem. / Determine se este é mesmo o seu problema.**  

[EN] Open up a terminal window (Accessories -> Terminal) and type:  
[PT] Abra uma janela de terminal (Acessórios -> Terminal) e digite:  
`gpsbabel -i garmin -f usb:-1`   

[EN] If you got something like this, this post is for you:  
[PT] Se você receber uma mensagem de erro como esta, continue lendo:  
`Claim interface failed: could not claim interface 0: Operation not permitted.`  

**2 - Solution: change the udev rules. / A solução: alterar as regras do udev.**  

[EN] Relax, this is easy. All we need is to create a text file with the new rules.  
You must do this with administrator (root) privileges. So, in that terminal window (you didn't closed it, did you?) start you favorite text editor (gedit, kedit, mousepad, etc) as root:  
`sudo gedit`  

Create a new file and paste this in it:  

`SYSFS{idVendor}=="091e", SYSFS{idProduct}=="0003", MODE="666"`  

Save the file as  **51-garmin.rules** under **/etc/udev/rules.d**  

Now restart the udev rules: `sudo udevadm control --reload-rules`  

And try again to see if you were successful:  
`gpsbabel -i garmin -f usb:-1 0 3724240363 292 GPSMap60CSX Software Version 4.10`  
That's it! Now you're good to go!  

[PT] Fique tranquilo que a coisa é simples.  
Tudo o que precisamos é criar um arquivo de texto com novas regras para o udev. Isso tem que ser feito com privilégios de administrador (root).  
Então, naquela janela de terminal (você não a fechou, né?) inicie seu editor de textos favorito (gedit, kedit, mousepad, etc) como root:  
`sudo gedit`  
Crie um arquivo novo e cole o seguinte nele:  

`SYSFS{idVendor}=="091e", SYSFS{idProduct}=="0003", MODE="666"`  

Salve o arquivo como **51-garmin.rules** no diretório **/etc/udev/rules.d**  

Agora reinicie as regras do udev: `sudo udevadm control --reload-rules`  
Tente de novo com o gpsbabel para ver se deu certo:  
`gpsbabel -i garmin -f usb:-1 0 3724240363 292 GPSMap60CSX Software Version 4.10`  
Pronto! Agora você pode baixar seus dados tranquilamente.



#### Comments

**[Robert Lipe](#22 "2011-01-14 03:02:24"):** Described in the GPSBabel doc at <http://www.gpsbabel.org/os/Linux_Hotplug.html> The OS vendors really should fix this....



