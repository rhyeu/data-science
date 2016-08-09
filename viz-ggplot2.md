---
layout: page
title: <eb>��<ec>��<ed>�� 과학
subtitle: <eb>��<ec>��<ed>�� <ec>��각화(ggplot2, ggvis)
output:
  html_document: 
    keep_md: yes
  pdf_document:
    latex_engine: xelatex
mainfont: NanumGothic
---





> ## <ed>��<ec>�� 목표 [^data-carpentry-ggplot2] {.objectives}
>
> * `ggplot2` <ed>��<ed>��지�<9c> <eb>��<ec>��<ed>���<bc> <ec>��각화<ed>��<eb>��. 
> * 고난<eb>�� 복잡<ed>�� <ec>��각화 <ec>��출물<ec>�� `ggplot2` <ed>��<ed>��지�<bc> <ed>��<ec>��<ed>��<ec>�� <eb>��계적<ec>���<9c> 구축<ed>��<eb>��.
> * Figshare [surveys.csv](http://files.figshare.com/1919744/surveys.csv), [mammals data](http://figshare.com/articles/Portal_Project_Teaching_Database/1314459)
<eb>��<ec>��<ed>���<bc> <ed>��<ec>��<ed>��<ec>�� <ec>��각화�<bc> <ec>��<ec>��<ed>��<eb>��.

[^data-carpentry-ggplot2]: [Data Carpentry R lessons on ecology](http://www.datacarpentry.org/R-ecology/)


### `ggplot2`�<9c> <ec>��각화�<bc> <ed>��<eb>�� <ec>��<ec>��

R<ec>�� 기본<ec>��<ec>���<9c> <ec>��각화�<bc> <ec>��<ed>�� <eb>��<ec>��<ed>�� 기능<ec>�� 존재<ed>��지�<8c>, `ggplot2`가 기본<ec>���<9c> <ec>��공되<eb>�� R <ec>��각화 기능 <ec>��<ec>�� <eb>��<ec>�� 강력<ed>�� 기능<ec>�� <ec>��공한<eb>��.
기본<ec>��<ec>�� R 기능<eb>�� <ec>��<eb><8c>�<ec>��<ec>���<9c> <eb>���<b8> <ec>��<ed>��<ed>��<ec>��<ec>�� <ec>��비스<eb>�� <ec>��<ed>���<bc> 비교가 <eb>��지 <ec>��<ec>�� <ec>��<eb>���<9d> 강력<ed>��<eb>��. <ec>��<eb>�� <ec>��<ec>��<ec>�� R<ec><9d>� �<b8> 겸손<ed>��<eb>��<eb>�� <ec>��각이 <eb>��<eb>��.

### <eb>��<ec>��<ed>�� <eb>��<ec>��로드<ec><99>� <ec>��각화 <ed>��체인 준�<84>


~~~{.r}
# read_csv�<U+393C><U+3E63> csv <U+653C><U+3E64>��<U+653C><U+3E63>��<U+653C><U+3E63>�� 불러 <U+653C><U+3E63>��<U+653C><U+3E63>��<U+653C><U+3E63>��<U+653C><U+3E62>��.
library(readr)
# <U+653C><U+3E63>��각화�<U+623C><U+3E63> <U+653C><U+3E63>��<U+653C><U+3E64>�� ggplot2 <U+653C><U+3E64>��<U+653C><U+3E64>��지�<U+623C><U+3E63> 불러 <U+653C><U+3E63>��<U+653C><U+3E63>��<U+653C><U+3E63>��<U+653C><U+3E62>��. 
library(ggplot2)
# ggplot2<U+653C><U+3E63>�� <U+653C><U+3E63>��<U+653C><U+3E62>��<U+653C><U+3E62>��<U+653C><U+3E63>��<U+653C><U+3E64>���<U+393C><U+3E63> <U+653C><U+3E63>��<U+653C><U+3E63>��<U+653C><U+3E62>�� <U+653C><U+3E62>��<U+653C><U+3E63>��<U+653C><U+3E64>���<U+623C><U+3E63> <U+653C><U+3E63>��처리<U+653C><U+3E64>��<U+653C><U+3E62>��.
library(dplyr)
# <U+653C><U+3E62>��<U+653C><U+3E63>��<U+653C><U+3E64>���<U+623C><U+3E63> 불러<U+653C><U+3E63>��<U+653C><U+3E62>��.
surveys.dat <- read_csv("http://files.figshare.com/1919744/surveys.csv")
~~~



~~~{.output}
FALSE Error in open.connection(con, "rb"): Timeout was reached

~~~

[figshare](https://figshare.com/)[^figshare-wired] <ec>��<ec>��<ed>��<ec>��<ec>�� <eb>��<ec>��<ed>���<bc> 가<ec>��<ec>��<eb>��. `surveys.csv` <eb>��<ec>��<ed>��<eb>�� <ed>��<ed>��<eb>�� <eb>��물에 관<ed>�� 측정<ec>��보�<b0>� <eb>���<a8> <ec>��<eb>��.

### <ec>��각화�<bc> <ec>��<ed>�� <eb>��<ec>��<ed>�� <ec>��처리 과정

<eb>��<ec>��로드 받�<9d>� <eb>��<ec>��<ed>��<ec>�� <eb><8c>�<ed>�� <ec>��<ec>��<ec>��보�<a5><bc> `summary` <ed>��<ec>���<bc> <ec>��<ec>��<ed>��<ec>�� <ec>��<ed>��본다.


~~~{.r}
summary(surveys.dat)
~~~



~~~{.output}
Error in summary(surveys.dat): object 'surveys.dat' not found

~~~

#### 1 <eb>���<84> - 결측�<92> <ec>���<b0>

<eb>��<ec>��<ed>��<ec>��<ec>�� <ec>��부 결측<ec>��보�<b0>� `summary` <ec>��<ed>��결과�<bc> 보여주고 <ec>��<ec>��, <ec>���<bc> <ec>��거한<eb>��. 
�<81> 변<ec>��마다 결측치�<b0>� <ec>��<ec>�� <ec>���<bc> <ed>��<eb><95>� <ed>��<eb><95>� <ec>��<ec>��<ec>��<eb>���<8c> 결측<ec>��보�<a5><bc> <ec>��거하<eb>�� <eb><8c>�<ec>��<ec>�� `dplyr` <ed>��<ec>��<ed>�� <ec>��<ec>��<ec>���<bc> <ec>��<ec>��<ed>��<ec>��
<ec>��괄적<ec>���<9c> 처리<ed>��<eb>��.


~~~{.r}
surveys.complete <- surveys.dat %>%
                    filter(species_id != "") %>%       # species_id 결측�<U+FFFD> <U+FFFD>�거
                    filter(!is.na(weight)) %>%          # weight 결측�<U+FFFD> <U+FFFD>�거
                    filter(!is.na(hindfoot_length))     # hindfoot_length 결측�<U+FFFD> <U+FFFD>�거
~~~



~~~{.output}
FALSE Error in eval(expr, envir, enclos): object 'surveys.dat' not found

~~~
#### 2 <eb>���<84> - 미�<af>�한 <ec>���<8c> <ec>���<b0>

개체<ec>��가 <ec>��<ec><9d>� 종이 많아<ec>��, 개체<ec>�� 기�<a4>� 10 보다 <ec>��<ec><9d>� 종�<9d>� <ec>��거하기로 <ed>��<eb>��.
먼�<a0>� `group_by` <ed>��<ec>���<9c> 개체종을 그룹<ec>���<9c> 군집<ed>��<ed>���<a0>, `tally` <ed>��<ec>���<9c> �<81> 종별�<9c> 개체<ec>���<bc> <ec>���<a0>, 
<eb>��부<ec>��<ec>���<9c> `sort=TRUE` �<bc> <eb>��<ec>��<ec>�� <eb>��림차<ec>��<ec>���<9c> <ec>��<eb>��<ed>��<eb>��. 



~~~{.r}
species.counts <- surveys.complete %>%
  group_by(species_id) %>%
  tally(sort=TRUE)
~~~



~~~{.output}
FALSE Error in eval(expr, envir, enclos): object 'surveys.complete' not found

~~~



~~~{.r}
tail(species.counts)
~~~



~~~{.output}
FALSE Error in tail(species.counts): object 'species.counts' not found

~~~

개체<ec>��가 10�<9c> 미만<ec>�� 종을 <ec>��거하�<a0>, <ec>��각화�<bc> <ec>��<ed>�� 기본 <eb>��<ec>��<ed>��<ec>�� 준비�<a5><bc> <ec>��료한<eb>��.


~~~{.r}
frequent.species <- species.counts %>%
                    filter(n >= 10) %>%
                    select(species_id)
~~~



~~~{.output}
FALSE Error in eval(expr, envir, enclos): object 'species.counts' not found

~~~



~~~{.r}
surveys.complete <- surveys.complete %>%
           filter(species_id %in% frequent.species$species_id)
~~~



~~~{.output}
FALSE Error in eval(expr, envir, enclos): object 'surveys.complete' not found

~~~

#### 기본 R <ec>��각화 기능 <ed>��<ec>��

`weight`�<bc> <ec>��측�<b3>�<ec>�� `x` <ec>��치에 <eb>���<a0>, 종속변<ec>�� `hindfoot_length`�<bc> `y`<ec>�� <eb>���<a0> R 기본 <ec>��각화 <ec>��<ec>��<eb>���<bc> <eb>��<ec>��<ed>��<ed>�� 보자.


~~~{.r}
plot(x = surveys.complete$weight, y = surveys.complete$hindfoot_length)
~~~



~~~{.output}
Error in plot(x = surveys.complete$weight, y = surveys.complete$hindfoot_length): object 'surveys.complete' not found

~~~

### `ggplot2` <ed>��<ed>��지�<9c> <ec>��각화

`ggplot2`�<bc> <ec>��<ec>��<ed>��<ec>�� R 기본 <eb>��<ec>��<eb>�� <ec>��각화 기능<ec>�� <eb><8c>�<ec>��<ed>��<ec>�� <eb>��<ec>��<ed>�� <ec>��<ec>��<ec>�� <ec>��<ed>��<ed>�� <ec>�� <ec>��<eb>��.

<eb>��<ec>��<ed>��<ed>��<eb>��<ec>�� <eb>��<ec>��<ed>��<ec>��<ec>�� 복잡<ed>���<a0> <ec>��교한 <ec>��각화 <ec>��출물<ec>��  `ggplot2` <ed>��<ed>��지�<9c> <ec>��<ec>��<ed>�� <ec>�� <ec>��<eb>��.
기본<ec>��<ec>��만으�<9c> 최소<ec>�� <eb>��<eb>��<ec>���<9c> 출판 <ed>���<88> <ec>��각화 <ec>��출물<ec>�� 만들<ec>�� <eb>�� <ec>�� <ec>��<eb>��.

`ggplot2` <ec>��각화 <ec>��출물<ec><9d>� <ec>��각화 <ec>��<ec>���<bc> 차곡차곡 추�<b0>�<ed>�� <eb>��가면서 만들<ec>�� 간다.

`ggplot2`  <ec>��각화 <ec>��출물<ec><9d>� <eb>��<ec>�� <eb>��계로 만들<ec>�� <eb>��간다:

- `data` <ec>��<ec>���<9c> <ed>��<ec>�� <eb>��<ec>��<ed>��<ed>��<eb>��<ec>���<bc> <ed>���<af><ec>�� 묶어 <ec>��결시<ed>��<eb>��.


~~~{.r}
ggplot(data = surveys.complete)
~~~

- 미적 <ec>��<ec>���<bc> `aes` �<9c> <ec>��<ec>��<ed>��<ec>��, <ed>���<af>축에 <eb>��<ec>��<ed>�� 변<ec>���<bc> 매핑<ed>���<a0>, <ed>���<b0>, 모양, <ec>��<ec>�� <eb>��<ec>�� <ec>��각화<ed>��<eb>��. 


~~~{.r}
ggplot(data = surveys.complete, aes(x = weight, y = hindfoot_length))
~~~

- <eb>��<ec>��<ed>��<ec>�� <eb><8c>�<ed>�� <ec>��각적 <ed>��<ed>��(<ec>��, <ec>��, 막�<8c>� <eb>��)<ec>�� <ed>��<eb>��<eb>�� `geoms` <ec>�� <ec>��<ec>��<ed>��<ec>�� <ed>���<af><ec>�� 반영<ed>��<eb>��. 
<ed>���<af><ec>�� `geoms`�<bc> 추�<b0>�<ed>��<eb>��<eb>�� `+` <ec>��<ec>��<ec>���<bc> <ec>��<ec>��<ed>��<eb>��::


~~~{.r}
ggplot(data = surveys.complete, aes(x = weight, y = hindfoot_length)) +
  geom_point()
~~~



~~~{.output}
Error in ggplot(data = surveys.complete, aes(x = weight, y = hindfoot_length)): object 'surveys.complete' not found

~~~

> #### 주의 <ec>��<ed>�� {.callout}
>
> - `ggplot` <ed>��<ec>��<ec>�� <eb>��<ec><9d>� <ec>��<eb>�� 것도 추�<b0>�<ed>�� `geom` 계층<ec>�� <ed>��<ed>�� 반영<eb>��<eb>��. �<89>, 보편<ec>��<ec>�� <ed>���<af> <ec>��<ec>��<ec>��<eb>��.
> - `aes()`<ec>�� <ec>��<ec>��<ed>�� `x`�<95>, `y`축도 <ec>��기에 <ed>��<ed>��<eb>��<eb>��.

### <ed>���<af> 변경하�<b0>

- <ed>��명도(transparaency, alpha)�<bc> 추�<b0>�<ed>��<eb>��.


~~~{.r}
ggplot(data = surveys.complete, aes(x = weight, y = hindfoot_length)) +
  geom_point(alpha=0.1)
~~~



~~~{.output}
Error in ggplot(data = surveys.complete, aes(x = weight, y = hindfoot_length)): object 'surveys.complete' not found

~~~

- <ec>��<ec>��<ec>�� 추�<b0>�<ed>��<eb>��.


~~~{.r}
ggplot(data = surveys.complete, aes(x = weight, y = hindfoot_length)) +
  geom_point(alpha=0.1, color = "blue")
~~~



~~~{.output}
Error in ggplot(data = surveys.complete, aes(x = weight, y = hindfoot_length)): object 'surveys.complete' not found

~~~

### <ec>��<ec>�� 그림

�<81> 종별�<9c> 체중 분포�<bc> <ec>��각화<ed>��<eb>��.


~~~{.r}
ggplot(data = surveys.complete, aes(x = species_id,  y = weight)) +
                   geom_boxplot()
~~~



~~~{.output}
Error in ggplot(data = surveys.complete, aes(x = species_id, y = weight)): object 'surveys.complete' not found

~~~

<ec>��<ec>��그림<ec>�� <ec>��<ec>�� 추�<b0>�<ed>��<ec>��, <ed>��<ec>��<ed>�� 관측점�<bc> 많이 관측된 측정값을 �<bc> <ec>�� <ec>��<eb>��.


~~~{.r}
ggplot(data = surveys.complete, aes(x = species_id, y = weight)) +
                   geom_jitter(alpha = 0.3, color = "tomato") +
                   geom_boxplot(alpha = 0)
~~~



~~~{.output}
Error in ggplot(data = surveys.complete, aes(x = species_id, y = weight)): object 'surveys.complete' not found

~~~

<ec>���<b0> <ec>��각화 <ec>��출물<ec>��<ec>�� <ec>��<ec>��그림<ec>�� 지<ed>�� 계층 <ec>��<ec>�� <eb>��<ec>�� 방식<ec>�� 주목<ed>��<eb>��.
`geoms` <ec>��<ec>���<bc> 조정<ed>���<a0>, <ed>��명도�<bc> 조절<ed>�� <ed>���<af><ec>�� 계층<ec>�� <ec>��<eb>�� 방식<ec>�� <ec>��<ec>��<ed>��<eb>��.

> ### <eb>��<ec>��과제 {.challenge}
>
> `hindfoot_length`<ec>�� <eb><8c>�<ed>�� <ec>��<ec>��그림<ec>�� <ec>��<ec>��<ed>��<eb>��.

### <ec>��계열 <eb>��<ec>��<ed>�� <ec>��각화

�<81> 종별�<9c> <eb>��<eb>���<84> 개체<ec>���<bc> 계산<ed>��<eb>��.
<ec>�� <ec>��<ec>��<ec>�� <ec>��<ed>��<ed>���<b0> <ec>��<ed>��<ec>��<eb>�� 먼�<a0>� <eb>��<ec>��<ed>���<bc> 그룹집단<ed>��<ed>���<a0>, �<81> 그룹마다 <ed>��<eb>�� <eb>��코드 개수�<bc> <ec>��<eb>��.



~~~{.r}
yearly.counts <- surveys.complete %>%
                 group_by(year, species_id) %>%
                 tally
~~~



~~~{.output}
Error in eval(expr, envir, enclos): object 'surveys.complete' not found

~~~

`x`축에 <ec>��<eb>��, `y` 축에 개수�<bc> <eb>���<a0> 직선<ec>���<9c> <ec>��간에 <eb>��<eb>�� 경과<ed>�� <ec>��보�<a5><bc> <ec>��각화<ed>��<eb>��.


~~~{.r}
ggplot(data = yearly.counts, aes(x = year, y = n)) +
                  geom_line()
~~~



~~~{.output}
Error in ggplot(data = yearly.counts, aes(x = year, y = n)): object 'yearly.counts' not found

~~~

불행<ed>��게도, <ec>���<b0> 그래<ed>��<eb>�� <ec>��<ed>��<eb>�� 바�<b0>� <ec>��<eb>��<eb>��, <ec>��<ec>��<eb>�� 모든 종에 <eb><8c>�<ed>�� <eb>��<ec>��<ed>���<bc> <ec>��각화<ed>���<8c> 명령<ec>���<bc> <ec>��<ec>��<ed>���<b0> <eb>��문이<eb>��.
`species_id`�<9c> <ec>��각화<ed>�� <eb>��<ec>��<ed>���<bc> 쪼갠 <ed>��<ec>�� `ggplot` 명령<ec>���<9c> <ec>��각화<ed>���<8c> <ed>��<eb>��.


~~~{.r}
ggplot(data = yearly.counts, aes(x = year, y = n, group = species_id)) +
  geom_line()
~~~



~~~{.output}
Error in ggplot(data = yearly.counts, aes(x = year, y = n, group = species_id)): object 'yearly.counts' not found

~~~

<ec>��<ec>��<ec>�� 추�<b0>�<ed>���<8c> <eb>���<b4>, 그래<ed>��<ec>��<ec>�� 개체�<bc> <ec>��별하�<8c> <eb>��<eb>��.


~~~{.r}
ggplot(data = yearly.counts, aes(x = year, y = n, group = species_id, color = species_id)) +
  geom_line()
~~~



~~~{.output}
Error in ggplot(data = yearly.counts, aes(x = year, y = n, group = species_id, : object 'yearly.counts' not found

~~~

###  측면보여주기(faceting)

`ggplot` <ec>��<eb>�� *측면 보여주기(faceting)* <eb>��<eb>�� <ed>��<ec>��<ed>�� 기능<ec>�� <ec>��<ec>��<ec>��, <ed>��<ec>�� <ec>��<ec>��<ec>�� <eb>��<eb>��
그래<ed>�� <ed>��<eb>���<bc> <eb>��<ec>�� 그래<ed>���<9c> 쪼갤 <ec>�� <ec>��<eb>��. <ec>���<bc> <eb>��<ec>��, �<81> 종마<eb>�� <ec>��계열 그래<ed>���<bc> 별도�<9c> 
<eb>��<ec>��<ed>��<ed>�� <ec>�� <ec>��<eb>��.


~~~{.r}
ggplot(data = yearly.counts, aes(x = year, y = n, color = species_id)) +
  geom_line() + facet_wrap(~species_id)
~~~



~~~{.output}
Error in ggplot(data = yearly.counts, aes(x = year, y = n, color = species_id)): object 'yearly.counts' not found

~~~

관측된 �<81> 개체 <ec>��별에 <eb>��<eb>�� 그래<ed>��<ec>�� 직선<ec>�� 쪼개고자 <ed>��<eb>��.
<ec>�� <ec>��<ec>��<ec>�� <ec>��<ed>��<ed>��<eb>���<b4>, <ec>��별로 그룹<ec>�� 만들<ec>�� <eb>��<ec>��<ed>��<ed>��<eb>��<ec>��<ec>�� 개수�<bc> <ec>��<ec>��<ec>�� <eb>��<eb>��.

> ### <eb>��<ec>��과제 {.challenge}
>
> - <eb>��<ec>��<ed>��<ed>��<eb>��<ec>��<ec>�� <ed>��<ed>��링해<ec>�� "F" <ed>��<ec><9d>� "M" 값을 갖는 <eb>��코드�<8c> 갖도�<9d> <ec>��<ec>��<ed>��<eb>��.
>  
> 
> 
> 
> ~~~{.r}
> sex_values = c("F", "M")
> surveys.complete <- surveys.complete %>%
>            filter(sex %in% sex_values)
> ~~~
> 
> 
> 
> ~~~{.output}
> Error in eval(expr, envir, enclos): object 'surveys.complete' not found
> 
> ~~~
> 
> - <ec>��<eb>��(`year`), 개체 <ec>��<ec>��<ec>���<b4>(`special_id`), <ec>��(`sex`) 별로 그룹<ec>�� 만든<eb>��.
>
> 
> ~~~{.r}
> yearly.sex.counts <- surveys.complete %>%
>                      group_by(year, species_id, sex) %>%
>                      tally
> ~~~
> 
> 
> 
> ~~~{.output}
> Error in eval(expr, envir, enclos): object 'surveys.complete' not found
> 
> ~~~
>
> - (개별 그래<ed>�� <eb>��부<ec>��) <ec>��별로 쪼개<eb>�� 측면보여주기 <ed>���<af><ec>�� <ec>��<ec>��<ed>��<eb>��.
>
> 
> ~~~{.r}
> ggplot(data = yearly.sex.counts, aes(x = year, y = n, color = species_id, group = sex)) +
>   geom_line() + facet_wrap(~ species_id)
> ~~~
> 
> 
> 
> ~~~{.output}
> Error in ggplot(data = yearly.sex.counts, aes(x = year, y = n, color = species_id, : object 'yearly.sex.counts' not found
> 
> ~~~
>
> - <eb>��문출<ed>��<ec>���<9c> <ed>��<ec>�� 배경<ec>�� 좀<eb>�� 가<eb>��<ec>��<ec>�� 좋게 <ed>��<eb>��.
> ` theme_bw()` <ed>��<ec>���<bc> <ec>��<ec>��<ed>��<ec>�� <ed>��<ec>�� 배경<ec>�� <ec>��<ec>��<ed>��<eb>��.
> 
> 
> ~~~{.r}
> ggplot(data = yearly.sex.counts, aes(x = year, y = n, color = species_id, group = sex)) +
>   geom_line() + facet_wrap(~ species_id) + theme_bw()
> ~~~
> 
> 
> 
> ~~~{.output}
> Error in ggplot(data = yearly.sex.counts, aes(x = year, y = n, color = species_id, : object 'yearly.sex.counts' not found
> 
> ~~~
> 
> > - 종�<8c>�<ec>��<ec>�� <ec>��별로 <ec>��<ec>��<ec>�� <ec>��<ed><98>�<ec>�� 그래<ed>�� 가<eb>��<ec>��<ec>�� 좋게 만들 <ec>�� <ec>��<eb>��.
> > (종�<9d>� <ec>���<b8> 별도 그래<ed>���<9c> <ec>��각화<eb>��<ec>��<ec>��, <eb>�� <ec>�� <ec>��별하�<8c> 만들 <ed>��<ec>��<eb>�� <ec>��<eb>��.)
> 
> 
> 
> ~~~{.r}
> ggplot(data = yearly.sex.counts, aes(x = year, y = n, color = sex, group = sex)) +
>   geom_line() + facet_wrap(~ species_id) + theme_bw()
> ~~~
> 
> 
> 
> ~~~{.output}
> Error in ggplot(data = yearly.sex.counts, aes(x = year, y = n, color = sex, : object 'yearly.sex.counts' not found
> 
> ~~~
> 
> > - <ec>��<eb>��<ec>�� 걸쳐 �<81> 종별�<9c> <ed>���<a0> 체중<ec>�� <ec>��각화<ed>��<eb>��.
> 
> 
> ~~~{.r}
> yearly.weight <- surveys.complete %>%
>                  group_by(year, species_id, sex) %>%
>                  summarise(avg_weight = mean(weight, na.rm = TRUE))
> ~~~
> 
> 
> 
> ~~~{.output}
> Error in eval(expr, envir, enclos): object 'surveys.complete' not found
> 
> ~~~
> 
> 
> 
> ~~~{.r}
> ggplot(data = yearly.weight, aes(x=year, y=avg_weight, color = species_id, group = species_id)) +
>   geom_line() + theme_bw()
> ~~~
> 
> 
> 
> ~~~{.output}
> Error in ggplot(data = yearly.weight, aes(x = year, y = avg_weight, color = species_id, : object 'yearly.weight' not found
> 
> ~~~
> 
> > - <ec>��각화�<bc> <ec>�� <ec>��<eb>�� <eb>��계�<a5><bc> 밟아<ec>�� <eb>��<ec>��<ed>�� <ec>��차�<a5><bc> 거친<eb>���<a0> <ec>��각하<eb>��가?
> > - <ec>��컷과 <ec>���<b7> 체중<ec>�� <ec>��<eb>��<ed>�� 차이가 <eb>��<ec>�� <ec>��별로 별도 <ec>��각화�<bc> <ec>��<ed>��<ed>��<eb>��.
> 
> 
> ~~~{.r}
> ggplot(data = yearly.weight, aes(x=year, y=avg_weight, color = species_id, group = species_id)) +
>   geom_line() + facet_wrap(~ sex) + theme_bw()
> ~~~
> 
> 
> 
> ~~~{.output}
> Error in ggplot(data = yearly.weight, aes(x = year, y = avg_weight, color = species_id, : object 'yearly.weight' not found
> 
> ~~~
> 지금까지 <ec>��각화 결과가 <ec>��<eb>��<ed>�� 좋았지�<8c>, <ec>���<81> 출판<ed>��기에<eb>�� 많이 부족하<eb>��.
> <ec>��각화 <ec>��출물 결과�<bc> <ed>��<ec>��<ed>�� <ec>�� <ec>��<eb>�� <eb>���<b8> 방법<ec><9d>� 무엇<ec>�� <ec>��<ec>���<8c>?
> `ggplot2` [컨닝쪽�<a7>�(cheat sheet)](https://www.rstudio.com/wp-content/uploads/2015/08/ggplot2-cheatsheet.pdf)�<bc> 
> 참조<ed>���<a0>, <ec>��<ec>��<eb>�� <ec>��가지 <ec>��<ec>��<eb>��<ec>���<bc> <ec>��<ec>��본다.
> 
> `x`축과 `y`축에 'year'<ec><99>� 'n' 보다 <eb>�� 많�<9d>� <ec>��보�<a5><bc> <ec>��<eb>��<ed>��<eb>���<9d> 변경하�<a0>, 그래<ed>��<ec>�� <ec>��목을 추�<b0>�<ed>��<eb>��.
> 
> 
> ~~~{.r}
> ggplot(data = yearly.sex.counts, aes(x = year, y = n, color = sex, group = sex)) +
>   geom_line() +
>   facet_wrap(~ species_id) +
>   labs(title = 'Observed species in time',
>        x = 'Year of observation',
>        y = 'Number of species') + theme_bw()
> ~~~
> 
> 
> 
> ~~~{.output}
> Error in ggplot(data = yearly.sex.counts, aes(x = year, y = n, color = sex, : object 'yearly.sex.counts' not found
> 
> ~~~
> 
> <ec>��<ec>�� 좀<eb>�� <eb>��<ec>��<ec>��<ec>�� <ed>��<ec>�� <eb>�� 많�<9d>� <ec>��보�<a5><bc> 주는 `x`, `y` �<95> 명칭<ec>���<9c> 바꿨지�<8c>, 가<eb>��<ec>��<ec>�� <eb>��<ec>��지�<a0> <ec>��<eb>��.
> 글<ec>�� <ed>��기�<a5><bc> 변경하�<a0> 글<ec>��체도 변경한<eb>��.
> 
> 
> ~~~{.r}
> ggplot(data = yearly.sex.counts, aes(x = year, y = n, color = sex, group = sex)) +
>   geom_line() +
>   facet_wrap(~ species_id) +
>   labs(title = 'Observed species in time',
>        x = 'Year of observation',
>        y = 'Number of species') +
>   theme(text=element_text(size=16, family="Arial")) + theme_bw()
> ~~~
> 
> 
> 
> ~~~{.output}
> Error in ggplot(data = yearly.sex.counts, aes(x = year, y = n, color = sex, : object 'yearly.sex.counts' not found
> 
> ~~~
> 
> 조작<ec>�� <ed>�� <eb>��<ec>��<ec>��, `x` 축이 <ec>��<ec>��<ed>�� <ec>��<ec>��<ed>�� 가<eb>��<ec>��<ec>�� <ec>��<eb>��<ed>���<a0> <ec>��지 <ec>��<ec>��<ec>�� �<bc> <ec>�� <ec>��<eb>��.
> <eb>���<a8> 방향<ec>�� 변경해<ec>�� <ec>���<9c> 겹쳐지지 <ec>��<eb>���<9d> <ec>��<ed>�� <ed>��<ec><9d>� <ec>��직방<ed>��<ec>���<9c> 바꾼<eb>��.
> 90<eb>�� 각도�<bc> <ec>��<ec>��<ed>��거나, <eb><8c>�각선 방향<ec>���<9c> <eb>��벨방<ed>��<ec>�� 변경하<eb>���<9d> <ec>��<ec>��<ed>�� 각도�<9c> 바꾸<eb>�� <ec>��<ed>��<ec>�� 진행<ed>��<eb>��. 
> 
> 
> ~~~{.r}
> ggplot(data = yearly.sex.counts, aes(x = year, y = n, color = sex, group = sex)) +
>     geom_line() +
>     facet_wrap(~ species_id) +
>     theme_bw() +
>     theme(axis.text.x = element_text(colour="grey20", size=12, angle=90, hjust=.5, vjust=.5),
>           axis.text.y = element_text(colour="grey20", size=12),
>           text=element_text(size=16, family="Arial")) +
>     labs(title = 'Observed species in time',
>          x = 'Year of observation',
>          y = 'Number of species')
> ~~~
> 
> 
> 
> ~~~{.output}
> Error in ggplot(data = yearly.sex.counts, aes(x = year, y = n, color = sex, : object 'yearly.sex.counts' not found
> 
> ~~~
> 
> <ec>��<ec>��, <eb>��벨을 <ed>��<ec>��<ec>�� 가<eb>��<ec>��<ec>�� <eb>�� 좋아졌�<a7>��<8c>, 개선<ed>�� <ec>��지<eb>�� <eb>��<ec>�� <ec>��<eb>��.
> <ec>��간을 5분만 <eb>�� <eb>��<ec>��<ec>�� <eb>�� <eb>��<ec><9d>� <ec>��각화 <ec>��출물<ec>�� 만들<ec>�� <eb>��<eb>���<9d> <ed>��<eb>�� <ed>��<ec><9d>� <eb>��가지 <ec>��<ec>��<ec>�� <ec>��<eb>��<ed>�� 본다.
> `ggplot2` 컨닝 쪽�<a7>��<bc> <ec>��<ec>��<ed>��<ec>��, <ec>���<b0> <ec>��각화 <ec>��출물<ec>�� <ec>��<ec>��<ed>��  <ec>��감을 받아본다.
> 
> <eb>��<ec>��<ec>�� 몇�<b0>�지 <ec>��각난 것이 <ec>��<eb>��:
> 
> - <ec>�� <eb>��께�<a5><bc> 변경할 <ec>�� <ec>��<eb>��지 <ec>��<ed>��본다.
> - 범�<a1>�(legend) 명칭<ec>�� 변경할 방법<ec>�� <ec>��<ed>��본다. 범�<a1>� <eb>��벨�<9d>� <ec>��<eb>��가?
> - <ec>��<ec>��<ec>�� 좋게 <ed>��<eb>��<eb>�� <eb>���<b8> <ec>��<ec>�� <ed>��<eb>��<ed>���<bc> <ec>��<ec>��<ed>��<eb>��. (http://www.cookbook-r.com/Graphs/Colors_(ggplot2)/)
> 
> <ec>��벽한 <ec>��각화 <ec>��출물<ec>�� <eb>��출되�<b4>, <ec>��<ed>��<ed>��<eb>�� 그림<ed>��<ec>�� <ed>��<ec>��<ec>���<9c> <ec><a0>�<ec>��<ed>��<eb>��.
> 그림 <ed>���<bc> <eb>��<ec>���<bc> 지<ec>��<ed>��<ec>�� <ed>��기�<a5><bc> <ec>���<8c> 변경한<eb>��.
> 
> 
> ~~~{.r}
> ggsave("observed_species_in_time.png", width=15, height=10)
> ~~~


> ### `Error in plot.new() : figure margins too large` <ec>��각화 문제 <ed>���<b0> {.callout}
>
> 그림<ec>�� 좌우<ec>��<ed>�� <ec>���<b1>(margin)<ec>�� 맞�<a7>� <ec>��<eb>�� <ec>��류�<b0>� 발생<ed>��<eb>�� 경우 
> 좌우<ec>��<ed>�� <ec>��백을 기본<ec>��<ec>�� `par(mar=c(1,1,1,1))` 명령<ec>���<bc> <ed>��<ed>�� <ed>��결한<eb>��. 
>
> ~~~ {.r}
> plot(x = surveys.complete$weight, y = surveys.complete$hindfoot_length)
> Error in plot.new() : figure margins too large
> ~~~














### 참고<ec>���<8c>

[^figshare-wired]: ["figshare wants to open up scientific data to the world"](http://www.wired.co.uk/news/archive/2014-07/25/figshare)
