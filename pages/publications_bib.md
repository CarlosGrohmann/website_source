---
layout: page
title: Publications
subtitle: 
published: true
---
<sup>[Journal Articles](#papers) · [Book Chapters](#chapters) · [Abstracts](#abstracts) · [Datasets](#datasets) · [GRASS-GIS](#grass) · [Magazine Articles](#magazine) · [Other Documents](#other)</sup>  

Here you can find a list of the papers I published, as well as some selected conference abstracts. The references are sorted, listed and formatted with [Jekyll Schollar](https://github.com/inukshuk/jekyll-scholar).   

I intend to keep an open access copy of my papers at [EarthArXiv.org](https://osf.io/preprints/eartharxiv/) and [ArXiv.org](https://arxiv.org/), which means that you can read them even without a subscription to the publisher, but be warned that most of these are [postprints](http://www.sherpa.ac.uk/romeoinfo.html) created from the "accepted manuscript" (that is, they have the exact same content of the final published version, except for the publisher's typesetting). For a final version, please refer to the publisher's website (which may be behind a paywall).  

And if you use reference managers (you should), you can get a file with all my publications: [BibTex](http://en.wikipedia.org/wiki/Bibtex) format: [here](../../downloads/CarlosGrohmann_papers.bib) (good for [JabRef](http://jabref.sourceforge.net/), [Zotero](http://www.zotero.org/) and a bazillion others) [RIS](http://en.wikipedia.org/wiki/RIS_\(file_format\)) format: [here](../../downloads/CarlosGrohmann_papers.ris) (good for [Mendeley](http://www.mendeley.com/) or [EndNote](http://endnote.com/)) (last update: 2020-12) 

<!-- &nbsp;   -->
&nbsp;  


<!-- <a name="landslides_lucas_meena"></a>
Meena, S.R., Soares, L.P., Grohmann, C.H., - Landslide Detection with Small Datasets: Evaluation of Machine and Deep Learning Algorithms.   -->

<!-- <a name="fruta_floodplains"></a>
Sawakuchi, A.O., Schultz, E., Pupim, F.N., Ribas, C.C., Bertassoli Jr., D.J., Souza, D.F., Cunha, D.F., Mazoca, C.E., Ferreira, M.P., Grohmann, C.H., Wanhfried, I.D., Chiessi, C.M., Cruz, F.W., Almeida, R.P. - Congruent expansion of Amazonian riverine environments and populations of birds specialized on seasonally flooded habitats -->
<!-- 

<a name="praias_natal_pca5017"></a>
Silva, B.B.S., Sergipe, P.P., Silva, R.S., Quintanilha, J.A., Grohmann, C.H. - Classificação supervisionada de imagens de satélite como ferramenta para análise temporal da morfodinâmica costeira entre as praias de Areia Preta e do Forte, Natal (RN).  
_Submitted for revision_  

<a name="alynne_pca5017"></a>
Affonso\*, A.A., Mandai, S.S., Portella, T.P., Grohmann, C.H., Quintanilha, J.A. - Assessing land use and land cover change in the Volta Grande do Xingu (Pará - Brazil) between 2000 and 2017.  
_Submitted for revision_  

<a name="landslides_helen_pca5017"></a>
Dias\*, H.C., Sandre, L.H., Alarcón, D.A.S., Grohmann, C.H., Quintanilha, J.A. - Landslides recognition using SVM, Random Forest and Maximum Likelihood on high-resolution satellite images: case study in Itaóca, southeastern Brazil.  
_Submitted for revision_  

<a name="lucas_unet"></a>
Soares\*, L.P., Dias\*, H.C., Grohmann, C.H. - Landslide Segmentation with U-Net: Evaluating Different Sampling Methods and Patch Sizes  
_Submitted for revision_  
Preprint available at [arXiv:2007.06672](https://arxiv.org/abs/2007.06672) [eess.IV] (open access)  
 -->



<a name="papers"></a>
## Journal Articles
\* Denotes student co-author.  
&dagger; Denotes post-doc co-author.  

{% bibliography --query @article[year<=2021 && kind=journal] %}

&nbsp;  
&nbsp; 
<a name="chapters"></a>
## Book Chapters  

{% bibliography --query @inbook %}

&nbsp;  
&nbsp; 
<a name="chapters"></a>
## Selected Abstracts/Conference Papers
(This list changes constantly. Check the Bib/RIS file to see all abstracts. )

{% bibliography --query @inproceedings[selection=yes] %}

&nbsp;  
&nbsp; 
<a name="datasets"></a>
## Datasets

{% bibliography --query @misc[kind=dataset] %}

&nbsp;  
&nbsp; 
<a name="magazine"></a>
## Magazine Articles

{% bibliography --query @article[kind=magazine] %}

&nbsp;  
&nbsp; 
<a name="grass"></a>
## GRASS-GIS Tutorials and Add-ons  
### Tutorials  

{% bibliography --query @techreport[kind=grasstut] %}

### Add-ons  
[r.denoise.py](https://github.com/CarlosGrohmann/grass_gis/tree/master/r_denoise_py) – is a port of [r.denoise](http://trac.osgeo.org/grass/browser/grass-addons/grass6/raster/r.denoise/description.html) from bash to python. Originally written by John Stevenson, its purpose is to remove noise (smooth/despeckle) from topographic data, particular DEMs derived from radar data (including SRTM), using Xianfang Sun’s [denoising algorithm](http://www.cs.cf.ac.uk/meshfiltering/index_files/Page342.htm). It is designed to preserve sharp edges and to denoise with minimal changes to the original data.  

[r.roughness.vector.py](http://grasswiki.osgeo.org/wiki/AddOns/GRASS7/raster#r.roughness.vector) – is a python script to calculate the surface roughness of a DEM as vector dispersion, using a moving-window approach ([Grohmann et al., 2011. IEEE Trans.Geos.Rem.Sens.](#ieee_roughness)).  
Resulting maps are: Vector Strength (R) and Inverted Fisher’s k parameter. This script is updated for GRASS-GIS version 7. Contributions to the code by Helmut Kudrnovsky.  

(old) [r.roughness](https://github.com/CarlosGrohmann/grass_gis/blob/master/r_roughness_old/r.roughness) – is a GRASS-GIS (versions 6.1 or above) shell script to calculate the surface roughness of a DEM, using r.surf.area and v.surf.rst. (uses **sh** as shell. Use [r.roughness_bash](https://github.com/CarlosGrohmann/grass_gis/blob/master/r_roughness_old/r.roughness_bash), if you run **bash**).  

(old) [r.roughness60](https://github.com/CarlosGrohmann/grass_gis/blob/master/r_roughness_old/r.roughness60) – for GRASS-GIS versions 6.0.x.  

(old) [azimuth.c](/downloads/azimuth2.c) – is a small C program to calculate the azimuth and length of vector lines exported by GRASS-GIS as ASCII files. It is useful for create rose diagrams of lineament maps.
Improvements on the original code after suggestions by Örs Téglásy, Hungary.  

See all [GRASS AddOns](http://grass.osgeo.org/download/addons/)  

You can also check the code for these AddOns at my [GitHub page](https://github.com/CarlosGrohmann/grass_gis).    


&nbsp;  
&nbsp; 
<a name="other"></a>
## Theses (Mixed Portuguese and English)

{% bibliography --query @phdthesis && @mastersthesis %}


