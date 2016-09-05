---
layout: page
title: <eb>��<ec>��<ed>�� 과학
subtitle: 지리정�<b4> <ec>��각화
output:
  html_document: 
    keep_md: yes
  pdf_document:
    latex_engine: xelatex
mainfont: NanumGothic
---


> ## <ed>��<ec>�� 목표 {.objectives}
>
> *  지리정�<b4> <ec>��각화�<bc> <ec>��<ed>�� 기본 개념<ec>�� <ed>��<ec>��<ed>��<eb>��.



[지<eb>��<ed>��(Cartography)](https://en.wikipedia.org/wiki/Cartography)<eb>�� 지<eb>���<bc> <ec>��<ec>��<ed>��<eb>�� 방식<ec>��<eb>��. <ed>��<ec>��<ed>�� 목적<ec>�� <eb>��<eb>�� <ed>��<ec>��<ed>�� 주제 <ed>��<ec><9d>� <eb>��<ec>��만을 <eb>��<ed><83>�<eb>��<ec>�� 그린 지<eb>���<bc> **[주제<eb>��(Thematic Map)](https://ko.wikipedia.org/wiki/지<eb>��<ec>��_종류)** <eb>���<a0> <ed>��<eb>��.  <ec>��<eb>�� <ec>��<ec>��<ec>��<ec>��<ec>�� <ec>���<b0> <ec>��<ed>��<ec>�� <eb>��<ed><83>�<eb>�� 기상<eb>��, <ec>��<ec>��<ed>�� <eb>�� <ec>��<ec>��<eb>�� <eb>��로도, <ed>��<ed>��<ed>�� <eb>�� <ec>��<ec>��<eb>�� <ed>��<eb>��, <ed>��계값<ec>�� 지<eb>��<ec>�� 그려 <eb>��<ec><9d>� <ed>���<84> 지<eb>�� <eb>��<ec>�� 좋�<9d>� <ec>��례<eb>��.

지리정보�<a5><bc> <ed>��<ed>��<ed>���<b0> <ec>��<ed>��<ec>��<eb>�� <eb>��<ec>���<bc> 같�<9d>� 기본 <ec>��<ec>��가 <ed>��<ec>��<ed>��<eb>��.

1. `.shp` <ed>��<ec>��<ec>���<bc> 갖는 지<eb>��<ec>���<b4> <ed>��<ec>��
2. <eb><8c>�<ed>��민국<ec>�� <eb><8c>�<ed>�� 기본 지리정�<b4>: <ec>��<eb>�� 경도 

### 1. 지리정�<b4> <ed>��<ec>��(SHP)

<eb><8c>�<ed>��민국 <ec>��<ec>��<ec>��<ec>�� <ed>��<ec>��구역경계(<ec>��군구) <ec>��료는 [<ed>��계�<a7>�리정보서비스](http://sgis.kostat.go.kr/contents/shortcut/shortcut_05.jsp) <ec>��<ec>��<ed>��<ec>��<ec>�� <ec>��료신�<ad><ec>�� <ed>���<b4> <ec>��<ec>�� <ec>�� <ec>��<eb>��. 그리�<a0>, <ec>��공되<eb>�� <ec>��<ec>��<ed>�� <ed>��<ec>��<ec>�� <eb><8c>�<ed>�� <ec>��보는 *<ec>��료신�<ad>* &rarr; *<ec>��료제�<b5> 목록*<ec>�� 참조<ed>��<eb>��. <ed>��<ec><9d>�, [Encaion](https://goo.gl/KyHR46) 구�<b8>� <eb>��<eb>��<ec>��브에<ec>�� 직접 <eb>��<ec>��로드 받을 <ec>��<eb>�� <ec>��<eb>��. <ed>��계청<ec>���<9c> <ec>���<ad><ed>���<b4> <ec>��<ec>��까�<a7>� <ec>��<ec>��<ec>�� <ec>��<ec>��<eb>���<b0> <ed>��<ec>��처리<ec>�� 기�<a4>�<ec>���<9c> 처리<eb>���<b0> <eb>��<ec>��로드 가<eb>��<ed>�� 기간<eb>�� 1주일<ec>��<eb>��.

  * [GADM](http://www.gadm.org/) <eb>��<ec>��<ed>��베이<ec>��<ec>��<ec>�� *Country*<ec>��<ec>�� **South Korea*<ec>�� <ec>��<ed>��<ed>���<a0>, *File Format*<ec>��<ec>�� *Shapefile*<ec>�� <ec>��<ed>��<ed>��<ec>�� <eb>��<ec>��로드<ed>��<eb>��.
  * [DIVA-GIS](http://www.diva-gis.org/gdata) <ec>��<ec>��<ed>��<ec>��<ec>��<eb>�� <ec>��<ec>��로이 <ed>���<ad><ec>�� <ed>��<ed>��<ed>�� <ec>��<eb>���<ad>가 지<eb>���<bc> <eb>��<ec>��로드 받을 <ec>�� <ec>��<eb>��.

- [<ed>��계�<a7>�<ec>��경계](http://sgis.kostat.go.kr/contents/shortcut/shortcut_05.jsp)
- [Global Administrative Areas](http://www.gadm.org/country)
- [<ed><8c>� <ed>��<ed>�� GitHub](https://github.com/southkorea/southkorea-maps)

~~~ {.python}
FILEMAP = {
    'shp': [('skorea-shp.zip','http://biogeo.ucdavis.edu/data/gadm2/shp/KOR_adm.zip')],
    'kmz': [('skorea.kmz','http://biogeo.ucdavis.edu/data/gadm2/kmz/KOR_adm0.kmz'),
            ('skorea-provinces.kmz','http://biogeo.ucdavis.edu/data/gadm2/kmz/KOR_adm1.kmz'),
            ('skorea-municipalities.kmz','http://biogeo.ucdavis.edu/data/gadm2/kmz/KOR_adm2.kmz')],
    'r'  : [('skorea.RData','http://biogeo.ucdavis.edu/data/gadm2/R/KOR_adm0.RData'),
            ('skorea-provinces.RData','http://biogeo.ucdavis.edu/data/gadm2/R/KOR_adm1.RData'),
            ('skorea-municipalities.RData','http://biogeo.ucdavis.edu/data/gadm2/R/KOR_adm2.RData')]
~~~

### 2.지리정�<b4> <ec>��각화�<bc> <ec>��<ed>�� <eb><8c>�<ed>��민국 <ec>���<b4>

<eb><8c>�<ed>��민국 지<eb>��<ec>�� 관<ed>�� <ec>��반정보의 경도범위<eb>�� 124 -- 132, <ec>��<eb>��범위<eb>�� 33 -- 43 <ec>��<eb>��. 

> ### <eb><8c>�<ed>��민국 <ec>��<eb>��<ec><99>� 경도 [^kor-lonlat] {.callout}
>
> #### <eb><8c>�<ed>��민국 <ec>���<b4>
> - 극동: 경상북도 <ec>��릉군<ec>�� <eb>��<eb>�� <eb>��<eb>�� <eb>���<bd> 131° 52<e2>�<b2>20", 
> - 극서: <ed>��<ec>��북도 <ec>��천군 <ec>��<eb>���<b4> 마안<eb>�� <ec>��<eb>�� <eb>���<bd> 124° 11<e2>�<b2>45"
> - 극남: <ec>��주도 <eb>��<ec>��주군 <eb><8c>�<ec>��<ec>�� 마라<eb>�� <eb>��<eb>�� 북위 33° 06<e2>�<b2>40"
> - 극북: <ed>��경북<eb>�� <ec>��<ec>���<b0> <eb>��<ec>���<b4> 북단 북위 43° 00<e2>�<b2>35"
>
> #### 북한 <ec>��<ec>��
> - 극동: 경상북도 <ec>��릉군<ec>�� <eb>��<eb>��(<e7>���<b6>)�<9c> <eb>���<bd> 131° 52<e2>�<b2>, 
> - 극서: <ec>��<eb>��<eb>��<eb>�� <ec>��<ec>��군의 <ec>��<ed>��<ec>��<eb>��(小黑山島)�<9c> <eb>���<bd> 125° 04<e2>�<b2>, 
> - 극북: 강원<eb>�� 고성�<b0> <ed>��<eb>���<b4> <ec>��<ed>��진으�<9c> 북위 38° 27<e2>�<b2>, 
> - 극남: <ec>��주도 <eb>��<ec>��주군 마라<eb>��(馬羅�<b6>)�<9c> 북위 33° 06<e2>��이<eb>��.

#### 2.1 `rworldmap` <ed>��<ed>��지�<bc> <ed>��<ec>��<ed>�� 지<eb>�� 그리�<b0> 기초

지<eb>��가 구해졌으�<b4> 범위�<bc> <ed>��<ec>��<ed>���<b0> <ec>��<ed>�� 극점(extreme point) <ec>��보�<a5><bc> <ec>��<ec>��<eb>��<eb>�� 것이 중요<ed>��<eb>��.
[<eb>��<ed>�� 극단<ec>���<b4>](https://en.wikipedia.org/wiki/Extreme_points_of_South_Korea)
<ec>��<ed>��<ed>��<eb>��<ec>��<ec>��<ec>�� <ed>��<ec>��<ed>�� 극점<ec>��보�<a5><bc> <ec>��<ec>��<ed>��<ec>�� <eb>��<ed>��<ed>�� 지<eb>���<bc> 그려본다. 


~~~{.r}
#install.packages(rworldmap)
library(rworldmap)
~~~



~~~{.output}
FALSE Error in library(rworldmap): there is no package called 'rworldmap'

~~~



~~~{.r}
library(ggmap)
korea.map <- getMap(resolution = "high")
~~~



~~~{.output}
FALSE Error in eval(expr, envir, enclos): could not find function "getMap"

~~~



~~~{.r}
south.korea.limits <- geocode(c(
  "Daegang-ri, Hyeonnae-myeon, County of Goseong, Gangwon",
  "Marado, Daejeong-eup, Seogwipo, Jeju",
  "Dokdo-ri,Ulleung-eup, County of Ulleung, North Gyeongsang",
  "Baengnyeongdo, Baengnyeong-myeon,    County of Ongjin, Incheon")
)  

south.korea.limits
~~~



~~~{.output}
FALSE        lon      lat
FALSE 1 128.3445 38.60602
FALSE 2 126.2522 33.22682
FALSE 3 131.8597 37.24397
FALSE 4 126.1783 37.21389

~~~



~~~{.r}
plot(korea.map,
     xlim = range(south.korea.limits$lon),
     ylim = range(south.korea.limits$lat),
     asp = 1
)
~~~



~~~{.output}
FALSE Error in plot(korea.map, xlim = range(south.korea.limits$lon), ylim = range(south.korea.limits$lat), : object 'korea.map' not found

~~~

[<eb>��<ed>�� 극단<ec>���<b4>](https://en.wikipedia.org/wiki/Extreme_points_of_South_Korea) �<91> <ec>��<ec>�� <ec>��<ec>��<ed>�� 
본토�<bc> 기�<a4>�<ec>���<9c> 지리정보�<a5><bc> <ec>��각화<ed>���<b4> <eb>��<ec>���<bc> 같다.


~~~{.r}
south.korea.mainland.limits <- geocode(c(
  "Daegang-ri, Hyeonnae-myeon, County of Goseong, Gangwon",
  "Songho-ri, Songji-myeon, Haenam, South Jeolla",
  "Guryongpo-eup, Pohang, North Gyeongsang",
  "Mohang-ri, Sowon-myeon, Taean, Chungcheong")
)  
south.korea.mainland.limits
~~~



~~~{.output}
FALSE        lon      lat
FALSE 1 128.3445 38.60602
FALSE 2 126.5351 34.32605
FALSE 3 129.5471 35.98531
FALSE 4 126.1413 36.76856

~~~



~~~{.r}
plot(korea.map,
     xlim = range(south.korea.mainland.limits$lon),
     ylim = range(south.korea.mainland.limits$lat),
     asp = 1
)
~~~



~~~{.output}
FALSE Error in plot(korea.map, xlim = range(south.korea.mainland.limits$lon), : object 'korea.map' not found

~~~

[^kor-lonlat]: [<eb><8c>�<ed>��민국<ec>�� <ec>��<eb>��<ec><99>� 경도�<bc> <ec>���<a0> <ec>��<ec>��<ec>��](http://tip.daum.net/question/3092152)

#### 2.2 `ggmap` <ed>��<ed>��지�<bc> <ed>��<ec>��<ed>�� 지<eb>�� 그리�<b0> 기초

`ggmap` API�<bc> <ed>��<ec>��<ed>��<ec>�� 지<eb>���<bc> 그린<eb>��.


~~~{.r}
library(ggmap)
# <U+653C><U+3E63>��치���<U+3E35><U+623C><U+3E63> 지<U+653C><U+3E63>��<U+653C><U+3E64>��<U+653C><U+3E62>��.
krLocation <- c(124.11, 33.06, 131.52, 43.00) #좌측<U+653C><U+3E64>��<U+653C><U+3E62>��경도, 좌측<U+653C><U+3E64>��<U+653C><U+3E62>��<U+653C><U+3E63>��<U+653C><U+3E62>��, <U+653C><U+3E63>��측상<U+653C><U+3E62>��경도, <U+653C><U+3E63>��측상<U+653C><U+3E62>��<U+653C><U+3E63>��<U+653C><U+3E62>��
southKrLocation <- c(125.04, 33.06, 131.52, 38.27)
#krLocation <- c(lon=126, lat=37) # <U+653C><U+3E62><U+383C><U+3E63>�<U+653C><U+3E64>��민국 <U+653C><U+3E63>��<U+653C><U+3E63>��
krMap <- get_map(location=krLocation, source="stamen", maptype="toner", crop=FALSE) #terrain, toner, watercolor
ggmap(krMap)
~~~

<img src="fig/unnamed-chunk-4-1.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" style="display: block; margin: auto;" />

`googlemap`<ec>�� <ec>��<eb>��경도 지<eb>��중앙, `stamen`, `openstreetmap`, `cloudmade`<eb>�� 
<ec>��<eb>��경도 <ec>��<ec>��<ed>��기�<a5><bc> 권장<ed>��<eb>��.


~~~{.r}
krMap <- get_map(location=krLocation, source="stamen", maptype="toner", crop=FALSE) #terrain, satellite, roadmap, hybrid, toner, watercolor
ggmap(krMap)
~~~

### 3. 지리정보처�<ac> <ed>��체인 [^1]

<img src="fig/R_SAGA_GE_logo.jpg" alt="LAMP<ec><99>� Docker가 <ec>��치된 <ec>��분투 공용 <ec>��미�<a7>�" width="40%" /> 

[^1]: http://spatial-analyst.net/wiki/index.php?title=Main_Page

- <ec>��<ed>�� GIS <ec>��<ed>��<ed>��<ec>��<ec>��
    - [System for Automated Geoscientific Analyses (SAGA GIS)](https://en.wikipedia.org/wiki/SAGA_GIS)
    - [Geographic Resources Analysis Support System (GRASS GIS)](https://en.wikipedia.org/wiki/GRASS_GIS)
- [TileMill](https://www.mapbox.com/tilemill/)
- KML 마크<ec>�� <ec>��<ec>��
    - [Keyhole Markup Language, KML](https://en.wikipedia.org/wiki/Keyhole_Markup_Language)


### 4. 지리정�<b4> <ec>��각화 <ec>��례

- 미국 <eb><8c>�<ec>��(2012) [<eb>��<ec>��<ed><83>�<ec>���<88> President Map](http://elections.nytimes.com/2012/results/president)
- 미국 빈곤<ec>�� <ec>���<b4> <ec>��각화 [The Topography of Poverty in the United States](http://www.cdc.gov/pcd/issues/2007/oct/07_0091.htm)
- [http://indiemapper.com/](http://indiemapper.com/app/learnmore.php?l=choropleth)


### 참고<ec>���<8c>

- [Thematic Cartography and Geovisualization](http://www.amazon.com/Thematic-Cartography-Geovisualization-3rd-Edition/dp/0132298341)
- [Web Cartography: Map Design for Interactive and Mobile Devices](https://www.crcpress.com/Web-Cartography-Map-Design-for-Interactive-and-Mobile-Devices/Muehlenhaus/9781439876220)
- [R Development Translation Team (Korean)](http://www.openstatistics.net/)

### R <ec>��<ec>�� 참고 <ec>��<ec>��<ec>��<ed>��

- [spatial.ly](http://spatial.ly/r/)
- [Spatial data in R: Using R as a GIS](https://pakillo.github.io/R-GIS-tutorial/)
- [Introduction to Spatial Data and ggplot2](http://rpubs.com/RobinLovelace/intro-spatial)
- [Spatial analysis in R: <eb>��커스<ed>�� <eb><8c>�<ed>��](http://www.maths.lancs.ac.uk/~rowlings/Teaching/- Sheffield2013/index.html)
- [Notes on Spatial Data Operations in R](https://dl.dropboxusercontent.com/u/9577903/- broomspatial.pdf)
- [Making maps with R](http://www.molecularecologist.com/2012/09/making-maps-with-r/)
