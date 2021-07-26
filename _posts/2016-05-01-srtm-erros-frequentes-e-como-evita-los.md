---
layout: post
title: SRTM - erros frequentes e como evitá-los
author: CarlosGrohmann
date: 2016-05-01
categories: 
tags: dem amazonia army ram insar srtm 
permalink: /blog/srtm-erros-frequentes-e-como-evita-los/
published: true
---

Os modelos de elevação SRTM são muito utilizados aqui no Brasil, já que não temos uma cobertura de mapas topográficos em escala decente (1:50.000 ou melhor) da maior parte de nosso território.  

Porém, tenho notado quatro erros muito frequentes nos artigos e monografias (TCCs, dissertações e teses) que vou comentar a seguir.  

O primeiro é com relação à citação do SRTM. Com tantos artigos que falam sobre o SRTM, é compreensível que surja uma dúvida sobre qual usar para citar os dados.  

A melhor citação para o SRTM é esta aqui:  

Farr, T.G., Rosen, P.A., Caro, E., Crippen, R., Duren, R., Hensley, S., Kobrick, M., Paller, M., Rodriguez, E., Roth, L., Seal, D., Shaffer, S., Shimada, J., Umland, J., Werner, M., Oskin, M., Burbank, D., &amp; Alsdorf, D., 2007. The Shuttle Radar Topography Mission. _Review of Geophysics_, 45:RG2004. DOI: <https://dx.doi.org/10.1029%2F2005RG000183>  

Esse artigo traz uma descrição bastante completa da missão SRTM, dos sistemas de radar, etc.  

O segundo ponto é sobre o acrônimo SRTM, que significa **S**huttle **R**adar **T**opography **M**ission. Notem que o "T" é de Topograph**y** e não de Topogra**phic**, como tenho visto em muitos artigos e teses.  

O terceiro ponto é um pouco mais conceitual. Vejo muitos textos dizendo que "os modelos de elevação foram construídos com dados SRTM", ou algo nessa linha. O problema aqui é que os dados SRTM **já são** modelos de elevação. Para construir os modelos de elevação com dados SRTM, seria necessário ter acesso aos dados brutos de radar, fazer o processamento da interferometria, etc. Então é melhor dizer que "foram utilizados dados de elevação SRTM (Farr et al., 2007)".  

O último ponto é sobre o que os dados SRTM representam. Por terem sido gerados com interferometria de radar das bandas C e X (vejam lá os detalhes no artigo do Tom Farr), os valores de elevação só representam o terreno em espaços abertos. Em áreas com vegetação, as ondas de radar (nesses comprimentos de onda) não penetram no dossel das árvores, então a elevação do SRTM é a de uma superfície que passa perto do topo do dossel. Desse modo, não é correto dizer que o SRTM seja um Modelo Digital de Terreno (MDT), mas sim um Modelo Digital de **Elevação** (MDE) ou de **Superfície** (MDS).  

A figura abaixo mostra a relação entre Modelos Digitais de Superfície e de Terreno para uma área no norte da Amazônia e deve ilustrar bem a diferença entre os dois.  

![](/img/profiles_600dpi.png)     
Perfis topográficos de dados SRTM, ASTER GDEM e Radiografia da Amazônia (Grohmann, 2015).

&nbsp;

É isso. Espero que este post ajude um pouco a sanar essas dúvidas comuns.  

**Referência**
Grohmann, C.H., 2015. ‘Radiography of the Amazon’ DSM/DTM data: comparative analysis with SRTM, ASTER GDEM.
Geomorphometry 2015, Poznam, Poland. Proceedings. [PDF disponível aqui](http://geomorphometry.org/system/files/Grohmann2015geomorphometry.pdf) 



