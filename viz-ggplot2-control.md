---
layout: page
title: <eb>��<ec>��<ed>�� 과학
subtitle: ggplot2 <ec>��<ec>�� <ec>��<ec>��
output:
  html_document: 
    keep_md: yes
  pdf_document:
    latex_engine: xelatex
mainfont: NanumGothic
---



### `gapminder` <eb>��<ec>��<ed>�� 준�<84>[^viz-ggplot2-control] 

[^viz-ggplot2-control]: [Taking control of qualitative colors in ggplot2](https://stat545-ubc.github.io/block019_enforce-color-scheme.html)


�<ad>가가 2개만 <ed>��<ed>��<eb>�� <ec>��<ec>��<ec>��<eb>��<ec>���<bc> <ec>��<ec>��<ed>�� `gapminder` <eb>��<ec>��<ed>���<bc> 불러<ec>��<eb>��.

<ec>��구수<ec>�� 기반<ed>��<ec>�� �<ad>가 <ec>��<ec>��<ec>�� <ec>��<eb>��<ed>���<a0> <eb>��<ec>�� <eb>��<ec>��<ed>��<eb>�� <ec>��<eb>��<ed>��<eb>��.
<ec>��<ec>��<eb>�� <ec>��<eb>�� 거품그림<ec>��<ec>�� <ed>�� �<ad>가가 <ec>��<ec><9d>� �<ad>가�<bc> 가리는 것을 방�<a7>�<ed>���<b0> <ec>��<ed>��<ec>��<eb>��.
<ec>��<ed>��게도, <eb>��<ec>��<ed>�� <ed>��<ec>�� <ec>��<ec>��가 <ec>��각적 <ec>��출물<ec>�� <ec>��<ed>��<ec>�� 미치<eb>�� <ec>��례<eb>��.
<ed>��지�<8c>, `ggplot2`<eb>�� `lattice` <ed>��<ec><9d>� 기본 그래<ed>�� <ec>��<ec>��<ed>��보다 <ec>��<eb>�� 것에 <eb>�� <ec>��<ed>��<ec>�� 받는<eb>��.

*2015-10-19: GitHub<ec>��<ec>�� 가<ec>��<ec>�� `ggplot2` 버젼 1.0.1.9003 <ec>�� <ec>��<ec>��<ed>��<eb>��.
`dev` 개발버젼<ec>�� CRAN <ec><a0>�<ec>��<ec>�� 버젼보다 변경사<ed>��<ec>�� 많이 반영<eb>��<ec>�� <ec>��<eb>��!*


~~~{.r}
library(ggplot2)
library(gapminder)
~~~



~~~{.output}
Error in library(gapminder): there is no package called 'gapminder'

~~~



~~~{.r}
suppressPackageStartupMessages(library(dplyr))
jdat <- gapminder %>% 
  filter(continent != "Oceania") %>% 
  droplevels() %>% 
  mutate(country = reorder(country, -1 * pop)) %>% 
  arrange(year, country)  
~~~



~~~{.output}
Error in eval(expr, envir, enclos): object 'gapminder' not found

~~~

### <ec>��<ec>�� <eb><8c>�<ed>�� <ed>��기�<99>� <ec>��<ec>�� <ec>��<ec>��

`ggplot2`�<bc> <ec>��<ec>��<ed>��<ec>�� <ec>��<ed>��<ec>�� `gapminder` 거품그림<ec>�� <ec>��<ec>��<ed>�� <eb>��간다.
기어가�<a0> <eb>��<ec>��, 걷고, 마�<a7>�막으�<9c> <eb>��<eb>��.

먼�<a0>�, <eb>��<eb>�� <ed>��<eb>���<bc> <ec>��<ec>��<ed>��<ec>�� 간단<ed>�� <ec>��<ec>��<eb>���<bc> <ec>��<ec>��<ed>��<eb>��.


~~~{.r}
j_year <- 2007
q <-
  jdat %>% 
  filter(year == j_year) %>% 
  ggplot(aes(x = gdpPercap, y = lifeExp)) +
  scale_x_log10(limits = c(230, 63000))
~~~



~~~{.output}
Error in eval(expr, envir, enclos): object 'jdat' not found

~~~



~~~{.r}
q + geom_point()
~~~



~~~{.output}
Error in q + geom_point(): non-numeric argument to binary operator

~~~

<ec>��<eb>��<eb>��<eb>�� 기호, <ed>���<b0>, <ec>��<ec>��<ec>�� <ec>��<ec>��<ed>��<eb>��.
<eb>��<ec>�� 불쾌<ed>�� <ec>��<ec>��<ec>�� <ec>��<ec>��<ed>��<ec>��, <ec>��공과 <ec>��<ed>���<bc> <ed>��<ec>��<ed>�� 명확<ed>�� <ed>��<eb>��.
멎진 <ec>��<ec>��체계�<bc> <ec>��<ec>��<ed>��<eb>��<eb>�� <ec>��교한 조작<ec>�� <ed>�� <ec>��<ec>��<ec>�� 지금�<9d>� <ec>��<eb>��<eb>��.
배짱<ec>�� 가<ec>��<eb>��!


~~~{.r}
## 기호<U+653C><U+3E63>�� <U+653C><U+3E62><U+383C><U+3E63>�<U+653C><U+3E64>�� <U+653C><U+3E64>��기�<U+393C><U+3E39>� <U+653C><U+3E63>��<U+653C><U+3E63>��<U+653C><U+3E63>�� 채우<U+653C><U+3E62>�� 것을 <U+653C><U+3E63>��<U+653C><U+3E63>��<U+653C><U+3E64>�� <U+653C><U+3E63>�� <U+653C><U+3E63>��<U+653C><U+3E62>��가? 그렇<U+653C><U+3E62>��!
q + geom_point(pch = 21, size = 8, fill = I("darkorchid1"))
~~~



~~~{.output}
Error in q + geom_point(pch = 21, size = 8, fill = I("darkorchid1")): non-numeric argument to binary operator

~~~

### <ec>��<ed>���<b0> = <ec>��구수

<ec>��<ed>��기로 <ec>��구수�<bc> 반영<ed>��고자 <ed>��<eb>��. 
반�<a7>�름을 바로 <ec>��<ec>��<ed>�� <ec>�� <ec>���<b0> <eb>��문에, �<ad>가�<84> <ec>��구에<ec>�� <ec>��<ec>�� <ed>��기�<a5><bc> 결정<ed>��<eb>���<9d> 관계�<a5><bc> $면적 = \pi r^2$<ec>���<9c> <ec>��<ec>��<ed>��<eb>��.
첫번�<b8> <ec>��<eb>��<ec>��<ec>�� <ec>��부 미비<ec>��<ec>�� 발견<eb>��<ec>��<eb>��: <ec>��<ec>�� <ed>��기�<b0>� <eb>���<b4> <ec>��<ec>���<a0>, <ed>��기별 범�<a1>�<eb>�� <ec>��<ed>��<eb>�� 것이 <ec>��<eb>��<eb>��.
<eb>��번째 <ec>��<eb>��<ec>��<ec>��, `show_guide = FALSE` <ec>��<ed>��<ec>��<ec>�� <ec>��<ec>��<ec>���<9c> 범�<a1>��<bc> <ec>��겼고, 
$\sqrt(pop / \pi)$ �<9c> <ec>��<ed>��기�<a5><bc> 매핑<ed>��<ec>�� 명시<ec>��<ec>���<9c> 규모<ec>�� <eb><8c>�<ed>�� 범위�<bc> <ec>��<ec>��<ed>��<ec>�� <ec>��<ec>�� <ed>��기�<a5><bc> 증�<b0>�<ec>��켰다.


~~~{.r}
## ggplot2 ALERT: size now means size, not radius!
q + geom_point(aes(size = pop), pch = 21)
~~~



~~~{.output}
Error in q + geom_point(aes(size = pop), pch = 21): non-numeric argument to binary operator

~~~



~~~{.r}
(r <- q +
   geom_point(aes(size = pop), pch = 21, show.legend = FALSE) +
   scale_size_continuous(range=c(1,40)))
~~~



~~~{.output}
Error in q + geom_point(aes(size = pop), pch = 21, show.legend = FALSE): non-numeric argument to binary operator

~~~

### <ec>��<ec>��<ec>���<9c> 결정<eb>�� <ec>��<ec>��<ec>���<9c> <ec>��<ec>�� 채워<eb>��<eb>��<eb>��.

`aes()` <ed>��<ec>���<bc> <ec>��<ec>��<ed>��<ec>�� <ec>��<ec>��<ec>�� <ec>��<ec>��<ec>���<9c> 매핑<ed>��<eb>��.
<ec>��<ec>��, `continent` <ec>��<ec>���<bc> <ec>��<eb>�� <ec>��<ec>��조합<ec>�� 맞춰 <ec>��<ec>��<ed>��<eb>��.
<eb><8c>�륙별 <ed>��<ec>��(facet)<ec>�� <ec>��<ec>��<ed>��<eb>��. <ed>��<ec>��<ec>�� <ec>��<ec>��<ed>��<eb>�� <ec>��<ec>��<eb>�� 맞춤<ed>�� <ec>��<ec>��조합<ec>�� <ec>��<ec>��<ed>��면서 진도<ec>��<ed>��<ec>�� 
<ec>��검<ed>�� <eb>��가<eb>��<eb>�� <eb>��<ec><9b>�<ec>�� <eb>��<eb>��. 가<eb>�� <ec>��<eb>��<ec>�� <ec>��<eb>�� 모든 �<ad>가가 <eb>��<ec>�� <ec>��조�<a5><bc> <eb>���<b0> <eb>��문에,
만약 <eb><8c>��<99> <ed>��<ec>��<ec>�� <eb>��<ec>��<ed>�� <ec>��<ec>��<ec>�� <ec>��<ec>�� <ec>��<eb>���<b4>, 뭔�<b0>� <ec>��못된 것을 <ec>��지<ed>�� <ec>�� <ec>���<8c> <eb>��<eb>��.


~~~{.r}
(r <- r + facet_wrap(~ continent) + ylim(c(39, 87)))
~~~



~~~{.output}
Error in eval(expr, envir, enclos): object 'r' not found

~~~



~~~{.r}
r + aes(fill = continent)
~~~



~~~{.output}
Error in eval(expr, envir, enclos): object 'r' not found

~~~

### �<ad>가�<84> <ec>��<ec>��조합<ec>�� <ec>��<ec>��<ed>��<eb>��.

`gapminder` <ed>��<ed>��지<ec>��<eb>�� <eb><8c>�륙과 �<81> �<ad>가�<84> <ec>��<ec>�� <ed>��<eb>��<ed>��가 <eb>��<eb>��<ec>��<eb>��.
<ec>���<bc> <eb>��<ec>��, [�<ad>가�<84> <ec>��<ec>��조합](https://github.com/jennybc/gapminder/blob/master/data-raw/gapminder-color-scheme-ggplot2.png)<ec>�� 
<ed>���<ad><ed>��<eb>��.


~~~{.r}
str(country_colors)
~~~



~~~{.output}
Error in str(country_colors): object 'country_colors' not found

~~~



~~~{.r}
head(country_colors)
~~~



~~~{.output}
Error in head(country_colors): object 'country_colors' not found

~~~

`country_colors` <ec>��<ec>��가 <ec>��<ed>���<b3> <ec>��<ec>�� <ec>��<eb>��<eb>��.
�<ad>가가 <ec>��<ec>���<9c> <eb><8c>�륙내 <ed>��기로 <ec>��<eb>��<eb>��<ec>�� <ec>��<ec>��, <ec>��<ec>��조합<ec>�� <ec>��<ec>��<eb>�� 로직<ec>�� 반영<ed>���<a0> <ec>��<eb>��.
<ec>��<ec>��<ec>��<ec>���<9c>, <ec>��<ec>��<ec>��<ec>��<eb>�� <ed>��<ec>�� 그렇지<eb>�� <ec>��지�<8c>, 분석<ec>�� <ed>��<ec>��<ec>��<ec>�� <ec>��존하�<b4> <ec>��<eb>��<eb>��.

### `ggplot2`<ec>�� <ec>��<ec>��<eb>�� <ec>��<ec>��조합<ec>�� 준비한<eb>��.

그래<ed>�� 문법(Grammar of Graphics)<ec>��<ec>��, **scale** <ed>��<ec>��가 <eb>��<ec>��<ed>�� 변<ec>��<ec>��<ec>�� `aes` 미학<ec>�� <eb><8c>�<ed>�� 매핑<ec>�� <ec>��<ec>��<ed>��<eb>��.
지금까지, <ec>��<eb>��<ec>���<9c> `ggplot2`가 <ec>��<ec>�� / 채우�<b0> scale <ec>�� 결정<eb>��<eb>���<9d> <eb>��버려 <eb>��<ec>��<eb>��.
<ed>��지�<8c>, 맞춤<ed>�� <ec>��<ec>��조합<ec>�� <ec>��<ec>��<ed>��<eb>���<b4>, `country` <ec>��<ec>��<ec>�� `geom_point`<ec>�� <ec>��<ec>��<ec>�� 채우<eb>��<eb>�� 매핑<ec>�� <eb>��<eb>���<9d> <ec>��<ec>��<ed>��<eb>��.

`scale_fill_manual` <ed>��<ec>���<bc> <ec>��<ec>��<ed>��<eb>��. <ec>��<ec>��<ed>�� 척도�<bc> 맞춤<ed>��<ec>���<9c> <ec>��<ec>��<ed>��<eb>��<eb>�� <ec>��<ec>��<eb>��<eb>�� <ed>��<ec>�� 가�<b1> �<91> 구성<ec>��<ec>��<eb>��.
<ed>��<ec>�� <ec>��<ec>��<eb>�� `value =`<ec>���<9c> 미학�<92> 벡터�<9c> <ec>���<88> 경우<ec>�� <ec>��<ec>��<ec>�� 채워<eb>��<eb>��<eb>��.
벡터가 명칭<ec>�� 갖게<eb>���<b4>, 매핑과정<ec>��<ec>�� 참고<eb>��<eb>��. <ec>��<eb>�� 기능<ec>�� 믿을 <ec>�� <ec>��<ec>�� <ec>��<eb>���<9c> <ec>��<ec>��<ed>��<eb>��!
`country_colors` 가 <ec>�� **<ec>��<ed>��<ed>���<8c> <ec>��<ec>��**<ec>�� <ec>��<ed>��<ed>��<eb>�� <ec>��<ec>��<eb>��.
<ec>���<bc> <ed>��<ed>�� `country` <ec>��<ec>�� <ec>��준<ec>�� <eb><8c>�<ed>�� <ec>��<ec>��, <eb>��<ec>��<ed>�� <ed>�� <ec>��<ec>��, <ed>��<ec><9d>� <ec>��<ed>��<ed>���<8c> <ec>��<eb>�� �<ad>가가 <ec>��<eb>��<eb>��<ec>��<ec>�� <ed>��<eb>��지<ec>�� 
관<ed>�� 걱정<ec>�� <eb>��<ec>��준<eb>��.

### `ggplot2` 거품그림<ec>�� <ec>��<ec>��<ed>��<eb>��.

<ec>�� 지<ec>��<ec>�� <ec>���<b4> <ec>��기성<ec>�� <ec>��<ec>�� <ec>��<eb>���<9c> <eb>��<ec>��<ed>�� 진다.
<eb>���<b8> 많�<9d>� 것과 마찬가지�<9c>, <ec>��<ec>�� 모든 것을 <ed>��결하�<b4>, <ec>���<90> <ec>��<eb>��. 
마�<a7>�막으�<9c> 추�<b0>�<ed>�� 최종 비트 <eb>��개는 `aes()`�<bc> <ec>��<ec>��<ed>��<ec>�� �<ad>가가 <ec>��<ec>��<ec>�� 매칭<eb>���<8c> <ed>���<a0>,
`scale_fill_manual()`<ec>�� <ec>��<ec>��<ed>��<ec>�� 맞춤<ed>�� <ec>��<ec>��조합<ec>�� 명세<ed>��<eb>��.


~~~{.r}
r + aes(fill = country) + scale_fill_manual(values = country_colors)
~~~



~~~{.output}
Error in eval(expr, envir, enclos): object 'r' not found

~~~

### <ed>��곳에 모두 모아보자.

<ec>��<eb>���<bc> <ec>��<ec>��<ed>��<eb>�� <ec>���<b4> 코드<eb>�� <eb>��<ec>���<bc> 같다.


~~~{.r}
j_year <- 2007
jdat %>% 
  filter(year == j_year) %>% 
  ggplot(aes(x = gdpPercap, y = lifeExp, fill = country)) +
  scale_fill_manual(values = country_colors) +
  facet_wrap(~ continent) +
  geom_point(aes(size = pop), pch = 21, show.legend = FALSE) +
  scale_x_log10(limits = c(230, 63000)) +
  scale_size_continuous(range = c(1,40)) + ylim(c(39, 87))
~~~



~~~{.output}
Error in eval(expr, envir, enclos): object 'jdat' not found

~~~
