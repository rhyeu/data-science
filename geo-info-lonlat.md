---
layout: page
title: <eb>��<ec>��<ed>�� 과학
subtitle: 지리정�<b4> <ec>��각화 - 주소<ec><99>� <ec>��<eb>��경도
output:
  html_document: 
    keep_md: yes
  pdf_document:
    latex_engine: xelatex
mainfont: NanumGothic
---



> ## <ed>��<ec>�� 목표 {.objectives}
>
> *  <ed>���<ad> 주소명을 지리정�<b4>(<ec>��<eb>��, 경도)�<9c> 변<ed>��<ed>��<eb>��. [^geoCodingWithR]
> * `dplyr` <ed>��<ed>��지 `mutate_geocode` <ec>��<eb>��경도 <ed>��<ec>���<bc> <ed>��<ec>��<ed>��<ec>��<ec>��<ec>��<ec><99>� 결합<ed>��<ec>�� 코드�<bc> 간결<ed>��<ed>��<eb>��. 

### 1. 지리정�<b4> API - `geocode` 

<eb>��<ec>��<ed>���<bc> 지리정보�<99>� 결합<ed>��<ec>�� <ec>��공할 경우 <ed>��<ec>��<ec>�� <eb><8c>�<ed>�� <ec>��<ed>��, <ec>���<a1>, <ed>��찰력<ec>�� <ec>��<ec>�� <ec>�� <ec>��<eb>��.
<eb>��<ec>��<ed>���<bc> 지리정보�<99>� 결합<ed>�� <eb>��, 가<ec>�� <ed>��<ec>��<ed>�� 것이 주소<ec>��보에 <ec>��<eb>��<ec><99>� 경도 <ec>��보�<a5><bc> 붙여 지<eb>��<ec>�� <ed>��<ec>��<ed>���<8c> <eb>��<eb>��.

주소<ec>��보�<b0>� <ec>��공되<ec>��<ec>�� <eb>��, <ec>��<ec>�� <ed>��<eb>��<eb>��<eb>�� <ec>��<eb>��<ec><99>� 경도�<bc> 불러<ec>�� <eb>�� <ec>��<ec>��<ed>��<eb>�� 것이 <ed>��<ec>��<ec>�� <ec>��종인 API<eb>��.
<ec>��경도 <ec>��보�<a5><bc> <ec>��공하<eb>�� <ec>��체로 구�<b8>�, <eb>��<ec>���<84>, <eb>��<ec>�� <eb>�� <ec>��<eb>�� <ec>��체�<b0>� <ec>��<eb>��.

R<ec>��<ec>�� 구�<b8>�, <eb>��<ec>���<84>, <eb>��<ec>��<eb>��<ec>��<ec>�� <ec>��공하<eb>�� 지리정�<b4> API�<bc> <ed>��<ec>��<ed>�� 경우, <ed>���<8c> <eb>��가지 방법<ec>�� 존재<ed>��<eb>��. 
<ed>��<eb>��<eb>�� 직접 구�<b8>�, <eb>��<ec>���<84>, <eb>��<ec>�� 지리정�<b4> API 문서�<bc> <ec>���<a0> R코드�<9c> <ec>��<ec>��<ed>��<eb>�� 방식<ec>�� <ec>���<a0>,
<eb>�� <eb>���<b8> <ed>��<eb>��<eb>�� `ggmap` <ed>��<ed>��지<ec>��<ec>�� <ec>���<b8> 지리정�<b4> API�<bc> <eb>��<ec>��<ed>��<ed>��<ec>�� <ed>��<ec>���<9c> 구현<ed>�� <eb>��<ec><9d>� 것을 <ed>��출해<ec>�� <ec>��<ec>��<ed>��<eb>�� 방법<ec>��<eb>��.

<ed>���<ad>주소�<bc> <ec>��<eb>��<ed>���<b4> <ec>��<eb>��, 경도 <ec>��보�<a5><bc> 반환<ed>��<eb>�� API�<9c> [구�<b8>� 지<eb>�� API](https://developers.google.com/maps/?hl=ko)�<bc> 기본<ec>���<9c> <ec>��<ec>��<ed>��<eb>��. 
`library(ggmap)` <ed>��<ed>��지�<bc> 불러<ec>���<b4> `geocode` <ed>��<ec>��가 주소명을 받아 <ec>��<eb>��, 경도 <ec>��보�<a5><bc> 반환<ed>��<eb>��.
<ed>��지�<8c>, Hadley Wickham<ec>�� 관<ec>��<ed>�� <ed>��<ed>��지<eb>�� [<ec>��코딩](encoding.html)<ec>���<9c> **utf-8**<ec>�� <ec>��<ec>��<ed>��<eb>��. 
<eb>��<eb>��<ec>��, <ed>���<ad><ec>��<eb>�� `enc2utf8` <ed>��<ec>���<bc> <ec>��<ec>��<ed>��<ec>�� <ec>��코딩<ec>�� 바꿔 <eb>��<ec><9d>� <ed>��<ec>�� `geocode` <ed>��<ec>��<ec>�� <ec>��<ec>���<9c> <eb>��<ec>��<ec>�� <ec>��<ed>��<eb>�� <ec>��<eb>��경도 <ec>��보�<a5><bc> 반환받을 <ec>�� <ec>��<eb>��. 

<img src="fig/geo-googleapi.png" alt="Google 지<eb>�� API" width="77%" />


~~~{.r}
library(ggmap)
library(ggplot2)
geocode(enc2utf8("<U+FFFD>�초"), source='google')
~~~



~~~{.output}
FALSE Error: invalid multibyte character in parser at line 3

~~~

주소<ec>��보�<a5><bc> <ed>���<98> 출력<ed>��고자<ed>�� 경우 `output="latlona"` <ec>��<ed>��<ec>��<ec>��<ec>�� 추�<b0>�<ed>��<eb>��.


~~~{.r}
#geocode(enc2utf8("<U+FFFD>�초"), source='google', output="latlona")
geocode(enc2utf8("<U+FFFD>�초&language=ko"), source='google', output="latlona")
~~~



~~~{.output}
FALSE Error: invalid multibyte character in parser at line 2

~~~
`"<ec>���<88>"`�<bc> `geocode` <ed>��<ec>�� <ec>��<ec>���<9c> <eb>��<ec><9d>� 경우<ec><99>� `"<ec>���<88>&language=ko"` <eb>��<ec>�� <ed>���<98> <eb>���<b4> 경우 <ed>��글주소�<9c> 출력<eb>���<8c> <ed>��<eb>��.


### 2. <ed>���<9c> <ec>��<ec>�� 주소<ec>��보에<ec>�� <ec>��<eb>��경도 <ec>���<b4> 뽑아<eb>���<b0> 

구�<b8>� 지<eb>�� API�<bc> <ec>��<ec>��<ed>�� 경우, 무료�<9c> <ec>��<ec>��<ed>�� <ec>�� <ec>��<eb>�� 반면<ec>�� <ec>��<ec>��<ec>��<ec>�� <ec>��<eb>��<ec>��<ec>�� 방�<a7>�<ed>���<b0> <ec>��<ed>��<ec>�� <ec>��<eb>�� API <ec>��비스<eb>�� 마찬가지지�<8c>,
구�<b8>�<ec>��<eb>�� API <ec>��비스 <ec>��공자 <ec>��<ec>���<9c> API�<bc> 변경할 <ec>�� <ec>���<a0>, <ec>��<ec>��<ec>��<ed>��<ec>�� <eb>��<eb>��.
<ed>��<ec>�� 글<ec>�� <ec>��<ec>��<ed>��<eb>�� <ec>��<ec>��<ec>��<ec>�� 구�<b8>� 지<eb>�� API<ec>�� 경우 <ec>��<ec>�� 2,500 �<88> 무료�<9c> <ec>��<ec>��<ec>�� 가<eb>��<ed>��<eb>��.

`geocodeQueryCheck(userType = "free")` 명령<ec>���<bc> <ec>��<ec>��<ed>��<ec>�� 구�<b8>� 지<eb>�� API <ec>��<ec>��<eb>��<ec>�� <ed>��<ec>��<ed>�� <ec>�� <ec>��<eb>��.


~~~{.r}
geocodeQueryCheck(userType = "free")
~~~



~~~{.output}
Error in eval(expr, envir, enclos): could not find function "geocodeQueryCheck"

~~~

경기<eb>�� �<8f> 강원<eb>�� 3�<9c> 지<ec>��<ec>�� <eb><8c>�<ed>�� <ec>��<eb>��경도 <ec>��보�<a5><bc> 받아<ec>��<eb>�� 경우, 먼�<a0>� <eb>��<ec>��<ed>��<ed>��<eb>��<ec>��<ec>�� <ec>��<ec>��<ed>���<a0> <eb>��<ec>��,
`enc2utf8()` <ed>��<ec>���<9c> <ec>��코딩<ec>�� 검증하�<a0> <eb>��<ec>�� `geocode` API�<bc> <ed>��출해<ec>�� <ec>��<eb>��경도 <ec>��보�<a5><bc> 받아<ec>��면서
바로 <eb>��<ec>��<ed>��<ed>��<eb>��<ec>��<ec>�� 붙인<eb>��.


~~~{.r}
library(ggmap)
library(ggplot2)
library(plyr)

geocodeQueryCheck(userType = "free")

kangwon.loc <- data.frame(addr=c("강원<U+FFFD><U+FFFD> <U+FFFD>�초<U+FFFD><U+FFFD> <U+FFFD>�랑<U+FFFD><U+FFFD>", 
                                 "경기<U+FFFD><U+FFFD> <U+FFFD>�왕<U+FFFD><U+FFFD> <U+FFFD>�일<U+FFFD>�거리로 73",
                                 "경기<U+FFFD><U+FFFD> <U+FFFD>�남<U+FFFD><U+FFFD> 분당�<U+FFFD> 미금<U+FFFD><U+FFFD>"), stringsAsFactors = FALSE)

kangwon.loc$addr <- enc2utf8(kangwon.loc$addr)

kangwon.loc.latlon <- geocode(kangwon.loc$addr, source="google")

kangwon.loc.latlon <- with(kangwon.loc, data.frame(addr,
                                   laply(addr, function(val){geocode(val)})))

kangwon.loc.latlon  
~~~



~~~{.output}
FALSE Error: invalid multibyte character in parser at line 7

~~~

`geocodeQueryCheck(userType = "free")` 명령<ec>���<9c> <ec>��<ec>��<eb>��<ec>�� 3�<9c> 준 것을 <ed>��<ec>��<ed>�� <ec>�� <ec>��<eb>��.


~~~{.r}
geocodeQueryCheck(userType = "free")
~~~



~~~{.output}
Error in eval(expr, envir, enclos): could not find function "geocodeQueryCheck"

~~~

### 3. `dplyr` <ed>��<ec>���<bc> <ed>��<ec>��<ed>�� <eb>�� 간결<ed>�� 코드

`dplyr`<ec>��<ec>�� <ec>��공하<eb>�� `mutate_geocode` <ed>��<ec>���<bc> <ec>��<ec>��<ed>��<ec>�� <ec>��<eb>��경도 <ec>��보�<a5><bc> <ec>��괄적<ec>���<9c> 받아<ec><99>�<ec>�� R <eb>��<ec>��<ed>��<ed>��<eb>��<ec>��<ec>���<9c> <ec><a0>�<ec>��<ed>��<eb>��.


~~~{.r}
library(dplyr)
kangwon.loc.dplyr <- kangwon.loc %>% mutate_geocode(addr)
~~~



~~~{.output}
FALSE Error in eval(expr, envir, enclos): object 'kangwon.loc' not found

~~~



~~~{.r}
kangwon.loc.dplyr
~~~



~~~{.output}
FALSE Error in eval(expr, envir, enclos): object 'kangwon.loc.dplyr' not found

~~~

경기<eb>��<ec><99>� 강원<eb>�� 3�<9c> 주소<ec>��보�<a5><bc> 구�<b8>� 지<eb>�� API 지<ec>��<ec>�� <ec>��<eb>��<ed>��<ec>�� <ec>��<eb>��<ec><99>� 경도<ec>��보�<a5><bc> 받아<ec><99>�<ec>�� <ec>���<bc> <eb>��<ec>��<ed>��<ed>��<eb>��<ec>��<ec>�� 붙인<eb>��.
받아<ec>�� <ec>��보�<a5><bc> `kangwon.loc.dplyr` <eb>��<ec>��<ed>��<ed>��<eb>��<ec>��<ec>�� <ec><a0>�<ec>��<ed>���<a0> <ec>���<bc> <ed>��<ec>��<ed>��<ec>�� 구�<b8>�지<eb>��<ec>�� <ec>��각화�<bc> <ed>��<eb>��.


~~~{.r}
kangwonMap <- qmap(enc2utf8("<U+FFFD>�초"), zoom = 8, maptype = "toner-lite")

kangwonMap + geom_point(data = kangwon.loc.dplyr, aes(lon,lat), size = 2, colour="blue")
~~~



~~~{.output}
FALSE Error: invalid multibyte character in parser at line 1

~~~

[^geoCodingWithR]: [GeoCoding with R](http://lumiamitie.github.io/r/geocoding-with-r-02/)
