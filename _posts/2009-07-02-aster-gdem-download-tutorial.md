---
layout: post
title: ASTER GDEM download tutorial
author: CarlosGrohmann
date: 2009-07-02
categories: 
tags: science dem aster gdem tutorial
permalink: /blog/aster-gdem-download-tutorial/
published: true
---


Agustin Castillo has a nice short tutorial on how to download ASTER GDEM tiles. Since it is in Spanish, I'm reproducing it in English.  

original post: [El mundo a tu alcance ASTER GDEM 30m en Mac](http://gvsigmac.blogspot.com/2009/07/el-mundo-tu-alcance-aster-gdem-30m-en.html)  

This works with Firefox, in Safari (Mac users), I couldn't see the selection map.  

Since last Monday, METI and NASA made available a Digital Terrain Model with 30x30 resolution (ASTER GDEM). This means that since this day, thanks to them, to gvSIG and Sextante, we can perform analysis of the physical environment of the whole world with first-class data. I will show a step-by-step with an example of an area in Ethiopia.  

![](/img/picture801.png){:width="70%"}   

Map of southwest Musilandia (south Ethiopia)  

First we go to the [metada](http://gcmd.nasa.gov/KeywordSearch/Metadata.do?Portal=GCMD&KeywordPath=%5BSource_Name%3A+Short_Name%3D%27TERRA%27%5D&OrigMetadataNode=GCMD&EntryId=ASTGTM1&MetadataView=Full&MetadataType=0&lbnode=mdlb2) page:    

![](/img/picture631.png){:width="70%"}   

Then we click on the get data link, which will take us to the [Welcome to WIST](https://wist.echo.nasa.gov/%7Ewist/api/imswelcome/) page:    

![](/img/picture641.png){:width="70%"}   

In the top of the page click on [ENTER WIST](https://wist.echo.nasa.gov/wist-bin/api/ims.cgi?mode=MAINSRCH&JS=1), and go to the data selection page.  

![](/img/picture651.png){:width="70%"}     

In order to download the data, we need to be logged in the system. We choose ASTER and digital elevation model. The system has a tutorial. Here you see an example of the area 5E-6E and 35N-36N.  

![](/img/picture661.png){:width="70%"}   

Now just hit Start Search:    

![](/img/picture671.png){:width="70%"}   

We get some info:  

![](/img/picture681.png){:width="70%"}   

And the search results:  

![](/img/picture691.png){:width="70%"}   

Now find the one you want and select it (in this case, 35N 5E):  

![](/img/picture701.png){:width="70%"}   

Now we can "buy" the image (you must "buy" it, although the cost will be zero), so add it to the cart:    

![](/img/picture711.png){:width="70%"}   

Mark the required options :    

![](/img/picture721.png){:width="70%"}   

In the next step, just confirm your personal data. Since it costs nothing, the billing address is not so important, but carefully check the email address.  


![](/img/picture731.png){:width="70%"}   

Revise your order and submit it:  

![](/img/picture7411.png){:width="70%"}   

You get a summary of the order  

![](/img/picture751.png){:width="70%"}   

We got two confirmation emails:  

![](/img/picture761.png){:width="70%"}   

This is the second email:  

![](/img/picture771.png){:width="70%"}   

After half hour we got an email with the ftp link to download the data:  

![](/img/picture781.png){:width="70%"}   

![](/img/picture791.png){:width="70%"}   

That's it!



#### Comments

**[Agustin](#2 "2009-07-03 17:21:17"):** Obrigado, Agustin

**[Cezar](#3 "2009-07-14 19:28:33"):** Thank you for this tutorial.

**[maelle.decherf](#4 "2009-07-16 10:19:08"):** Thank you very much ... well done !

**[philip nik](#5 "2010-03-16 13:05:10"):** nice and well explained.I wonder if I can use that data (DEM) in curious software "vizrt"?



