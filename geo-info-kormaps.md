---
layout: page
title: <eb>��<ec>��<ed>�� 과학
subtitle: Kormaps, leaflet 지리정�<b4> <ec>��각화 기초 
output:
  html_document: 
    keep_md: yes
  pdf_document:
    latex_engine: xelatex
mainfont: NanumGothic
---
 


> ## <ed>��<ec>�� 목표 {.objectives}
>
>  * <ec>��<eb>��경도 <ec>���<b4> <ed>��<ec>�� `ggmap` 지리정�<b4> <ec>��각화<ed>��<eb>��.
>  * `Kormaps` 지리정�<b4> <ec>��각화<ed>��<eb>��.

### 1. `Kormaps` 지리정�<b4> <ec>��각화 [^kormaps-01] 

[^kormaps-01]: [Kormaps <ed>��<ed>��지�<bc> <ec>��<ec>��<ed>�� <eb>��계구분도 <ec>���<8c> 그리�<b0>(1)](http://web-r.org/webrboard/6477)

2010<eb>�� <ec>��/<eb>��, <ec>��/�<b0>/�<ac>, <ec>��/�<b4>/<eb>�� <ed>��<ec>��구역지<eb>�� 3개�<a5><bc> 갖고 <ec>��구총조사(2010<eb>��) 기�<a4>� 지리정보�<a5><bc> <ec>��공하<eb>�� R <ed>��<ed>��지�<bc> 카톨�<ad><eb><8c>�<ed>���<90>
[문건<ec>��](http://web-r.org) 교수<eb>��께서 개발<ed>��<ec>�� 공개<ed>��<ec><98>�<eb>��.

`submap` 관<eb>�� <ec>��부 <eb>��<ec>��<ec>�� <eb>��지 <ec>��<eb>�� 경우<eb>�� <ec>��지�<8c>, 빠르�<8c> <ec>��구총조사결과�<bc> <eb><8c>�<ed>��민국 지리정보로 <eb>��<ec>��<ed>��<ed>��<eb>��<eb>�� 좋�<9d>� 기능<ec>�� <ec>��공하�<a0> <ec>��<eb>��.

`Kormaps` <ed>��<ed>��지�<bc> <ec>��치하�<a0>, 주제<eb>�� <ed>��<ed>��지 `tmap` <eb>�� 불러<ec>��<eb>��.


~~~{.r}
#install.packages("devtools")  # <U+653C><U+3E64>���<U+383C><U+3E38> <U+653C><U+3E63>��치한 경우<U+653C><U+3E63>��<U+653C><U+3E62>�� <U+653C><U+3E62>��<U+653C><U+3E63>�� <U+653C><U+3E63>��치할 <U+653C><U+3E64>��<U+653C><U+3E63>�� <U+653C><U+3E63>��<U+653C><U+3E63>��<U+653C><U+3E62>��<U+653C><U+3E62>��.
#devtools::install_github("cardiomoon/Kormaps")
library(Kormaps)
~~~



~~~{.output}
FALSE Error in library(Kormaps): there is no package called 'Kormaps'

~~~



~~~{.r}
library(tmap)
~~~



~~~{.output}
FALSE Error in library(tmap): there is no package called 'tmap'

~~~



~~~{.r}
library(raster)
~~~



~~~{.output}
FALSE Error in library(raster): there is no package called 'raster'

~~~

2010<eb>�� <ec>��/<eb>��, <ec>��/�<b0>/�<ac>, <ec>��/�<b4>/<eb>�� 3<eb>���<84> `Kormaps` <ed>��<ed>��지<ec>�� <eb>��<ec>��<eb>�� <ed>��<ec>��구역지<eb>��<eb>�� <eb>��<ec>���<bc> 같다.


~~~{.r}
p1 <- qtm(kormap1)
~~~



~~~{.output}
FALSE Error in eval(expr, envir, enclos): could not find function "qtm"

~~~



~~~{.r}
p2 <- qtm(kormap2)
~~~



~~~{.output}
FALSE Error in eval(expr, envir, enclos): could not find function "qtm"

~~~



~~~{.r}
p3 <- qtm(kormap3)
~~~



~~~{.output}
FALSE Error in eval(expr, envir, enclos): could not find function "qtm"

~~~



~~~{.r}
multiplot(p1, p2, p3, cols = 3)
~~~



~~~{.output}
FALSE Error in multiplot(p1, p2, p3, cols = 3): object 'p1' not found

~~~


`submap()` <ed>��<ec>���<bc> <ec>��<ec>��<ed>��<ec>�� <eb><8c>�<ed>��민국 <ed>��<ec>�� 지<ec>��<ec>�� 뽑아<eb>��<ec>�� 별도�<9c> 지리정보�<a5><bc> <ec>��각화 <ed>�� <ec>�� <ec>��<eb>��.


~~~{.r}
daejeon.lvl.3 <-  submap(korpopmap3, enc2utf8("<U+FFFD>�<U+FFFD><U+FFFD>"))
qtm(daejeon.lvl.3,"가�<U+FFFD>�<U+FFFD>가�<U+FFFD>")+tm_layout(fontfamily="AppleGothic")
~~~



~~~{.output}
FALSE Error: invalid multibyte character in parser at line 1

~~~

참고, `names(korpopmap1@data)` 명령<ec>���<bc> <ed>��<ed>��<ec>�� <ec>��구총조사(2010<eb>��)<ec>�� <ed>��<ed>��<eb>�� <eb>��<ec>��<ed>��<eb>�� <ed>��<ec>��<ed>�� <ec>�� <ec>��<eb>��.

### 2. `Kormaps`, `leaflet` <ed>��<ed>��지 <ed>��<ec>�� 지리정�<b4> <ec>��각화 [^kormaps-02]

[^kormaps-02]: [Kormaps <ed>��<ed>��지�<bc> <ec>��<ec>��<ed>�� <eb>��계구분도 <ec>���<8c> 그리�<b0>(2)](http://rpubs.com/cardiomoon/159305)

[leaflet](https://rstudio.github.io/leaflet/) <ed>��<ed>��지<eb>�� <ec>��<ed>��<eb>��<ed>���<8c> 지<eb>���<9c> 가<ec>�� <ec>��기있<eb>�� <ec>��<ed>��<ec>��<ec>�� <ec>��바스<ed>��립트 <eb>��<ec>��브러리로 
[<eb>��<ec>��<ed><83>�<ec>���<88>](http://www.nytimes.com/projects/elections/2013/nyc-primary/mayor/map.html), 
[<ec>��<ec>��<ed>��<ed>��<ec>��<ed>��](http://www.washingtonpost.com/sf/local/2013/11/09/washington-a-world-apart/), 
[GitHub](https://github.com/blog/1528-there-s-a-map-for-that), [<ed>��리커](https://www.flickr.com/map) 같�<9d>� �<ad><eb>��<ec>�� <ec>���<85> <ec>��<ec>��<ec>��<ed>��<ec>��<ec>�� <ec>��<ec>��<eb>���<a0> <ec>��<eb>��.



~~~{.r}
library(leaflet)
blue_palette <- colorNumeric(palette="Blues",domain=korpopmap3$가�<U+FFFD>�<U+FFFD>가�<U+FFFD>)
households <- paste0(korpopmap3@data$name,": ",korpopmap3@data$가�<U+FFFD>�<U+FFFD>가�<U+FFFD>)

leaflet(korpopmap3) %>%
  addTiles() %>%
  addPolygons(stroke=TRUE, 
              smoothFactor = 0.2,
              fillOpacity = .8, 
              popup=households,
              color= ~blue_palette(korpopmap3@data$가�<U+FFFD>�<U+FFFD>가�<U+FFFD>))
~~~



~~~{.output}
FALSE Error: <text>:2:66: unexpected input
FALSE 1: library(leaflet)
FALSE 2: blue_palette <- colorNumeric(palette="Blues",domain=korpopmap3$가
FALSE                                                                     ^

~~~

