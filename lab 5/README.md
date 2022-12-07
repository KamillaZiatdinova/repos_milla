---
title: "Исследование метаданных DNS трафика"
author: "Kamilla Ziatdinova"
date: "2022-11-02"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```


## Цель работы
1. Зекрепить практические навыки использования языка программирования R для обработки данных
2. Закрепить знания основных функций обработки данных экосистемы tidyverse языка R
3. Закрепить навыки исследования метаданных DNS трафика

## Подготовка данных
``` {r}
data <- read.csv("dns.csv")
print(data)
```
## Задание 4 
###Cколько участников информационного обмена в сети Доброй Организации?
```{r }
Is<-(unique(data$is))
Id<-(unique(data$id))
print(length(unique(union(Is,Id))))
```

## Задание 5 
### Какое соотношение участников обмена внутри сети и участников обращений к внешним ресурсам?
```{r }

```

## Задание 6 
###Найдите топ-10 участников сети, проявляющих наибольшую сетевую активность.
```{r }
w<-rev(sort(table(data$is)))
as.data.frame(w)
split(w,10)


```
## Задание 7 
### Найдите топ-10 доменов, к которым обращаются пользователи сети и соответственное количество обращений
```{r }
w<-rev(sort(table(data$query)))
as.data.frame(w)
split(w,1:10)

```



## Задание 8 
### Oпеределите базовые статистические характеристики (функция summary()) интервала времени между последовательным обращениями к топ-10 доменам.
```{r }
w<-rev(sort(table(data$query)))
as.data.frame(w)


```

## Задание 9 
### Часто вредоносное программное обеспечение использует DNS канал в качестве канала управления, периодически отправляя запросы на подконтрольный злоумышленникам DNS сервер. По периодическим запросам на один и тот же домен можно выявить скрытый DNS канал. Есть ли такие IP адреса в исследуемом датасете?
```{r }

```

## Задание 10 
### Определите местоположение (страну, город) и организацию-провайдера для топ-10 доменов. Для этого можно использовать сторонние сервисы, например https://v4.ifconfig.co/
```{r }

```