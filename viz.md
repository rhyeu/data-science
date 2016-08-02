---
layout: page
title: <eb>��<ec>��<ed>�� 과학
subtitle: <ec>��각화
output:
  html_document: 
    keep_md: yes
  pdf_document:
    latex_engine: xelatex
mainfont: NanumGothic
---



> ## <ed>��<ec>�� 목표  {.objectives}
>
> * <eb>��<ec>��<ed>�� <ec>��각화<ec>�� 중요<ec>��<ec>�� <ec>��<ed>��<ed>��<eb>��.
> * <ec>��각화 <ec>��개�<a5><bc> <ed>��<ed>�� <ec>��각화�<bc> 목적�<bc> 방향<ec>�� <ec>��<ed>��<ed>��<eb>��.


### Anscombe 4종류 <eb>��<ec>��<ed>��(Anscombe's Quartet) [^anscombe] [^anscombe-jstor]

Anscombe<eb>�� 1973<eb>�� <eb>��<ec>��<ed>�� <ed>��계량<ec>�� 갖는 4종류 <eb>��<ec>��<ed>��<ec>��<ec>�� 만들<ec>��<ec>�� <ec>��각화<ec>�� 중요<ec>��<ec>�� 공개<ed>��<eb>��.

|  <ed>��계량     |   �<92>  |
|-------------|-------|
|  <ed>���<a0>(`x`)  |  9    |
|  분산(`x`)  |  11   |
|  <ed>���<a0>(`y`)  |  7.5  |
|  분산(`y`)  |  4.1  |
|  <ec>��관계수   |  0.82  |
|  <ed>��귀<ec>��     |  y = 3.0 + 0.5*x |



[^anscombe]: [Anscombe quartet](https://en.wikipedia.org/wiki/Anscombe%27s_quartet)
[^anscombe-jstor]: Anscombe, F. J. (1973). "Graphs in Statistical Analysis". American Statistician 27 (1): 17<e2>�<93>21.



~~~{.r}
data(anscombe)
anscombe <- tbl_df(anscombe)
anscombe
~~~



~~~{.output}
# A tibble: 11 x 8
      x1    x2    x3    x4    y1    y2    y3    y4
   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
1     10    10    10     8  8.04  9.14  7.46  6.58
2      8     8     8     8  6.95  8.14  6.77  5.76
3     13    13    13     8  7.58  8.74 12.74  7.71
4      9     9     9     8  8.81  8.77  7.11  8.84
5     11    11    11     8  8.33  9.26  7.81  8.47
6     14    14    14     8  9.96  8.10  8.84  7.04
7      6     6     6     8  7.24  6.13  6.08  5.25
8      4     4     4    19  4.26  3.10  5.39 12.50
9     12    12    12     8 10.84  9.13  8.15  5.56
10     7     7     7     8  4.82  7.26  6.42  7.91
11     5     5     5     8  5.68  4.74  5.73  6.89

~~~

#### Anscombe <eb>��<ec>��<ed>��<ec>�� 4�<85> 기술<ed>��계량


~~~{.r}
# x1, x2, x3, x4 <U+653C><U+3E64>�����<U+3E30>
anscombe %>% select(x1,x2,x3,x4) %>% 
summarize(x1Mean=round(mean(x1),1), y2Mean=round(mean(x2),2), y3Mean=round(mean(x3),1), y4Mean=round(mean(x4),1))
~~~



~~~{.output}
# A tibble: 1 x 4
  x1Mean y2Mean y3Mean y4Mean
   <dbl>  <dbl>  <dbl>  <dbl>
1      9      9      9      9

~~~



~~~{.r}
# x1, x2, x3, x4 분산
anscombe %>% select(x1,x2,x3,x4) %>% 
summarize(x1Var=round(var(x1),1), x2Var=round(var(x2),1), x3Var=round(var(x3),1), x4Var=round(var(x4),1))
~~~



~~~{.output}
# A tibble: 1 x 4
  x1Var x2Var x3Var x4Var
  <dbl> <dbl> <dbl> <dbl>
1    11    11    11    11

~~~



~~~{.r}
# y1, y2, y3, y4 <U+653C><U+3E64>�����<U+3E30>
anscombe %>% select(y1,y2,y3,y4) %>% 
summarize(y1Mean=round(mean(y1),1), y2Mean=round(mean(y2),2), y3Mean=round(mean(y3),1), y4Mean=round(mean(y4),1))
~~~



~~~{.output}
# A tibble: 1 x 4
  y1Mean y2Mean y3Mean y4Mean
   <dbl>  <dbl>  <dbl>  <dbl>
1    7.5    7.5    7.5    7.5

~~~



~~~{.r}
# y1, y2, y3, y4 분산
anscombe %>% select(y1,y2,y3,y4) %>% 
summarize(y1Var=round(var(y1),1), y2Var=round(var(y2),1), y3Var=round(var(y3),1), y4Var=round(var(y4),1))
~~~



~~~{.output}
# A tibble: 1 x 4
  y1Var y2Var y3Var y4Var
  <dbl> <dbl> <dbl> <dbl>
1   4.1   4.1   4.1   4.1

~~~



~~~{.r}
# x1:y1 ~ x4:y4 <U+653C><U+3E63>��관계수
anscombe %>% 
summarise(cor1=round(cor(x1,y1),2), cor2=round(cor(x2,y2),2), cor3=round(cor(x3,y3),2),cor4=round(cor(x4,y4),2))
~~~



~~~{.output}
# A tibble: 1 x 4
   cor1  cor2  cor3  cor4
  <dbl> <dbl> <dbl> <dbl>
1  0.82  0.82  0.82  0.82

~~~



~~~{.r}
# y1:x1-x4 ~ y1:x1-x4 <U+653C><U+3E64>��귀분석
lm_fit <- function(y1, x1, dat) {
  the_fit <- lm(y1 ~ x1, dat)
  setNames(data.frame(t(coef(the_fit))), c("intercept", "slope"))
}
gfits <- anscombe %>%
  do(reg1 = lm_fit(y1, x1, .), reg2=lm_fit(y2, x2, .), 
     reg3=lm_fit(y3, x3, .), reg4=lm_fit(y4, x4, .))

unlist(gfits$reg1)
~~~



~~~{.output}
intercept     slope 
3.0000909 0.5000909 

~~~



~~~{.r}
unlist(gfits$reg2)
~~~



~~~{.output}
intercept     slope 
3.0000909 0.5000909 

~~~



~~~{.r}
unlist(gfits$reg3)
~~~



~~~{.output}
intercept     slope 
3.0000909 0.5000909 

~~~



~~~{.r}
unlist(gfits$reg4)
~~~



~~~{.output}
intercept     slope 
3.0000909 0.5000909 

~~~


#### Anscombe <eb>��<ec>��<ed>��<ec>�� 4�<85> <ec>��각화


~~~{.r}
p1 <- ggplot(anscombe) + geom_point(aes(x1, y1), color = "darkorange", size = 3) + theme_bw() + scale_x_continuous(breaks = seq(0, 20, 2)) + scale_y_continuous(breaks = seq(0, 12, 2)) + geom_abline(intercept = 3, slope = 0.5, color = "cornflowerblue") + expand_limits(x = 0, y = 0) + labs(title = "dataset 1")
p2 <- ggplot(anscombe) + geom_point(aes(x2, y2), color = "darkorange", size = 3) + theme_bw() + scale_x_continuous(breaks = seq(0, 20, 2)) + scale_y_continuous(breaks = seq(0, 12, 2)) + geom_abline(intercept = 3, slope = 0.5, color = "cornflowerblue") + expand_limits(x = 0, y = 0) + labs(title = "dataset 2")
p3 <- ggplot(anscombe) + geom_point(aes(x3, y3), color = "darkorange", size = 3) + theme_bw() + scale_x_continuous(breaks = seq(0, 20, 2)) + scale_y_continuous(breaks = seq(0, 12, 2)) + geom_abline(intercept = 3, slope = 0.5, color = "cornflowerblue") + expand_limits(x = 0, y = 0) + labs(title = "dataset 3")
p4 <- ggplot(anscombe) + geom_point(aes(x4, y4), color = "darkorange", size = 3) + theme_bw() + scale_x_continuous(breaks = seq(0, 20, 2)) + scale_y_continuous(breaks = seq(0, 12, 2)) + geom_abline(intercept = 3, slope = 0.5, color = "cornflowerblue") + expand_limits(x = 0, y = 0) + labs(title = "dataset 4")

multiplot(p1, p2, p3, p4, cols=2, main="Anscombe's Quartet")
~~~

<img src="fig/unnamed-chunk-4-1.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" style="display: block; margin: auto;" />

~~~{.output}
[1] "Anscombe's Quartet"

~~~

### <ec>��각화 [^tamara] 

컴퓨<ed>���<bc> 기반<ec>���<9c> <ed>�� <ec>��각화 <ec>��<ec>��<ed>��<ec><9d>� <ec>��각적<ec>���<9c> <eb>��<ec>��<ed>���<bc> <ed>��<ed>��<ed>��<ec>���<9c> <ec>��<ed>��<ec>�� 
<ec>��<eb>��<eb>��<ec>�� <ec>��<ec>��<ec>�� <eb>��<ec>�� <ed>��<ec>��<ec>��<ec>���<9c> <ec>��<ed>��<ed>�� <ec>�� <ec>��<eb>���<9d> <eb>��<eb>��<eb>��.

<ec>��기서 <ec>��각화가 <ec>��<ed>��<ed>�� <ec>��<ed>��<ec><9d>� <ec>��공�<a7>�<eb>�� �<8f> <ec>��<ec>��<ed>���<bc> <ed>��<ed>�� <ec>��<eb>��<ec>�� <eb><8c>�체하�<b0> 보다<eb>�� <ec>��간능<eb>��<ec>�� 증강<ec>��<ed>��<eb>��<eb>�� <ec>��<ec>��<ed>��<eb>��.
<eb>��<eb>��<ec>��, <ec>��<ec>�� <ec>��<eb>��<ed>�� <ed>��결책<ec>�� 존재<ed>���<a0> <ec>��뢰성<ec>�� <ec>��<eb>�� 경우 <ec>��각화가 그다지 <ed>��<ec>��<ed>��지<eb>�� <ec>��<eb>��<eb>��.
<eb>��<ed>��, 많�<9d>� 분석문제<ec>��<eb>�� <ec>��<eb>�� 질문<ec>�� <eb>��<ec>��<ec>�� <eb>��<eb>��지 <ec>��<ec>��<ec>�� <ec>���<a0> <ec>��<eb>�� 경우가 <ec>��<ec>��, 명세가 분명<ed>��지 <ec>��<eb>�� 경우가 <ec>��<eb>��<eb>��,
<ec>��<eb>�� 목적<ec>�� <ec>��<ec>��<ed>��<eb>��.

> ### <ec>��각화 {.callout}
> 
> "Computer-based visualization systems provide visual representations of datasets
 designed to help people carry out tasks more effectively" -- Tamara Munzner


[^tamara]: [Tamara Munzner. Visualization Analysis and Design. A K Peters Visualization Series, CRC Press, 2014](http://www.cs.ubc.ca/~tmm/vadbook/)

#### <ec>��각화가 <ec>�� <ed>��<ec>��<ed>��가?

**<ec>��지부<ed>��(cognitive load)**�<bc> **<ec>��각적 지�<81>(perception)**<ec>���<9c> 바꿔 <ed>��<eb>�� <ec>��<ec>��<ec>�� <eb>��<ec>�� <ed>��과적<ec>���<9c> 처리<ed>��<eb>��<eb>�� <ec>��각화�<bc> <ec>��<ec>��<ed>��<eb>��.


~~~{.r}
library(datasets)
women
~~~



~~~{.output}
   height weight
1      58    115
2      59    117
3      60    120
4      61    123
5      62    126
6      63    129
7      64    132
8      65    135
9      66    139
10     67    142
11     68    146
12     69    150
13     70    154
14     71    159
15     72    164

~~~

`women` <eb>��<ec>��<ed>��가 <ec>��<eb>��<ec>�� <eb>��<ec>�� <ec>��<ec>��<ec>��, <ec>��<ec>��<ec>�� 커짐<ec>�� <eb>��<eb>�� 체중<ec>�� 증�<b0>�<ed>��<eb>�� 것을 <ec>�� <ec>�� <ec>��지�<8c>, <eb>��<ec>��<ed>���<8c> 보고 <ec>��<ed>��<ed>��<eb>���<b4>
<ec>��지<ec>��<ec>���<9c> <eb>��<ec>��<ed>�� <ed>��줄을 <ec>���<a0> 머리<ec>��<ec>���<9c> <ec>��각하�<a0>, <eb>��번째 줄을 <ec>���<a0> <ec>��각하�<a0>, ... <ec>��<eb>�� 과정<ec>�� 반복<ed>��면서 <ec>��지<ec>�� 부<ed>��가 증�<b0>�<ed>���<8c> <eb>��<eb>��.
<ed>��지�<8c>, <ec>��각적<ec>���<9c> <ed>��<ed>��<ed>���<8c> <eb>���<b4> <ed>��<eb>��<ec>�� <ec>��<ec>���<bc> 체중 관계�<a5><bc> �<bc> <ec>�� <ec>��<eb>��.


~~~{.r}
women %>% ggplot(aes(y=weight, x=height)) + geom_point(color='blue', size=2) +
  geom_smooth(color='pink')
~~~

<img src="fig/unnamed-chunk-6-1.png" title="plot of chunk unnamed-chunk-6" alt="plot of chunk unnamed-chunk-6" style="display: block; margin: auto;" />

#### <ec>��각화 분석 <ec>���<9c> 구성<ec>��<ec>��

<ec>��각화 분석 <ec>��개는 4가지 부분으�<9c> 구성<eb>��<eb>��. 

- <ec>��문영<ec>�� : 최종 <ec>��<ec>��<ec>�� 고객<ec>�� <eb>��군인가?
- 추상<ed>��
    + <ec>��문영<ec>��<ec>�� 구체<ec>��<ec>�� <ec>��<ec>�� <ec>��각화 <ec>��<ec>���<9c> 번역
        * **<eb>��<ec>��<ed>�� 추상<ed>��** : <ec>��각화<ed>��<eb>�� 것이 무엇(what)<ec>��가?
        * **<ec>��<ec>�� 추상<ed>��** : <ec>��(why) <ec>��<ec>��<ec>��가 <eb>��<ec>�� <eb>��리는가?
- <ed>��<ed>��<ec>��<ec>��(idiom)
    + <eb>��<ec>��<ed>��가 <ec>��<eb>���<8c>(How) <ec>��각화<eb>��<eb>��가?
    	* **<ec>��각적 <ec>��코딩 <ed>��<ed>��<ec>��<ec>��** : <ec>��각화<ed>��<eb>�� 방법
    	* **<ec>��<ed>��<ec>��<ec>�� <ed>��<ed>��<ec>��<ec>��** : 조작<ed>��<eb>�� 방법
- <ec>��고리�<98>
	+ <ed>��<ec>��<ec>�� <ec>��<ec>��방법    	

[Munzner, Tamara. "A nested model for visualization design and validation." Visualization and Computer Graphics, IEEE Transactions on 15.6 (2009): 921-928.](http://www.cs.ubc.ca/~tmm/talks/iv09/nestedmodel-4x4.pdf)

<img src="fig/viz-framework.png" alt="RStudio" width="77%" />

#### <ec>��각화 분석 <ec>��근방<ed>��

<ec>��각화 <ec>��<ec>��<ed>�� <ec>��<ed>��<ec>���<84>, 메모�<ac> <ec>��<ec>��<eb>�� <eb>��<ec>�� 측정<ed>���<a0>, <ec>��<ec>�� 복잡<ec>��<ec>�� 분석<ed>��<eb>�� <ec>��고리�<98> <ec>��<ec>��<ec><9d>� 컴퓨<ed>�� 과학<ec>��<ec>�� 몫이<eb>��.
<ec>��<eb>��가지 <eb><8c>�<ec>�� <ec>��<ec>��<ed>�� <ec>��<ed>��<ed>��처�<a5><bc> <ec>��<eb>��<ed>��<ed>���<a0> <ec>��각적 <ec>��코딩 방법�<bc> <ec>��<ed>��<ec>��<ec>��<ed>��<eb>�� <ed>��<ed>��<ec>��<ec>��<ec>�� <ec>��계하<eb>�� 것�<9d>� <ec>��<ec>��<ed>�� <ec>��계자<ec>�� 몫이<eb>��.
<ec>��각화 <ec>��<ec>��<ed>�� 결과물을 <ec>��<eb>��<ec>��<ec>���<9c> 분석<ed>���<a0>, <ec>��<ec>��<ec>�� <ec>��간에 <eb><8c>�<ed>�� <ec>��<ed>��<ec>�� 추진<ed>��<eb>�� 것�<9d>� <ec>��지<ec>��리학<ec>��<ec>�� 몫이<eb>��.
<ec>���<bc> 감싸�<a0> <ec>��<eb>�� <eb>��<ec>��<ed>�� 추상<ed>��<ec><99>� <ec>��<ec>��추상<ed>��가 <ec>��<eb>��<eb>��, <ec>��<ec>��<ed>�� <ec>��계자가 <ec>��<eb>��<ec>��<ec>�� <ec>��계하�<b4> <ed>��<ed>��<eb>��<ec>��<ec>�� <ec>��지<ec>��리학<ec>��가 검증하�<a0>,
컴퓨<ed>�� 과학<ec>��가 개발<ed>��<eb>�� 구조�<bc> 갖는<eb>��.

<ec>�� 모든 <ec>��<ec>��<ec><9d>� <ec>��문영<ec>��<ec>��<ec>�� 문제<ec>��<ec>�� <ec>��<ec>��<ed>���<a0> 기존<ec>�� <eb>��구�<a5><bc> <ec>��<ec>��<ed>��<eb>�� 목표 <ec>��<ec>��<ec>���<bc> 관측하<eb>�� 것에<ec>�� <ec>��<ec>��<eb>��<eb>��<eb>�� <ec>��<eb>�� <ec>��류학<ec>��, 민족지<eb>��<eb>�� 분야<ec><99>� <ec>��관<eb>��<eb>��.
<eb>��<eb>��<ec>��, 기술중심<ec>���<9c> 밖으�<9c> <ed>��<ec>��<eb>���<88> <ec>��<eb>�� <ec>��지�<8c>, 문제<ed>��결작<ec>��<ec>���<9c> <ec>��각화�<bc> <ed>��<ec>��<ed>��<eb>�� 것도 가<eb>��<ed>�� <ec>��근법<ec>��<eb>��.

> ### <ec>��각화 <eb>���<ac>{.callout}
> 
> - **명령<ed>��(imperative)**: "방법(how)"<ec>�� 초점, Processing, OpenGL, prefuse
> - **<ec>��<ec>��<ed>��(declarative)**: "무엇(what)"<ec>�� 초점, D3, ggplot2, Protovis 

