## Цель работы
1. Зекрепить практические навыки использования языка программирования R для обработки данных
2. Закрепить знания основных функций обработки данных экосистемы tidyverse языка R
3. Развить пркатические навыки использования функций обработки данных пакета dplyr – функции
select(), filter(), mutate(), arrange(), group_by()

## Задание
Проанализировать встроенные в пакет nycflights13 наборы данных с помощью языка R и ответить на вопросы

##Подготовка
library(dplyr)
library(nycflights13)

## Задание 1 
### Сколько встроенных в пакет nycflights13 датафреймов?
kolvo <- ls("package:nycflights13")
length(kolvo)

## Задание 2
### Сколько строк в каждом датафрейме?
airlines <- nycflights13::airlines
nrow(airlines)

airports <- nycflights13::airports
nrow(airports)

flights <- nycflights13::flights
nrow(flights)

planes <- nycflights13::planes
nrow(planes)

weather <- nycflights13::weather
nrow(weather)

## Задание 3 
### Сколько столбцов в каждом датафрейме?
ncol(airlines)
ncol(airports)
ncol(flights)
ncol(planes)
ncol(weather)

## Задание 4
### Как просмотреть примерный вид датафрейма?
glimpse(airlines)
glimpse(airports)
glimpse(flights)
glimpse(planes)
glimpse(weather)

## Задание 5
### Сколько компаний-перевозчиков (carrier) учитывают эти наборы данных (представлено в наборах данных)?
count(distinct(select(airlines,carrier)))

## Задание 6
### Сколько рейсов принял аэропорт John F Kennedy Intl в мае?
airport<-filter(airports,name=='John F Kennedy Intl')%>% select(faa)%>% paste(sep='')
count(filter(flights,origin==airport, month == 5))


## Задание 7
### Какой самый северный аэропорт?
filter(airports,lat==max(lat))

## Задание 8
### Какой аэропорт самый высокогорный (находится выше всех над уровнем моря)?
filter(airports,alt==max(alt))  

## Задание 9
### Какие бортовые номера у самых старых самолетов?
filter(planes,year == min(year,na.rm = TRUE)) %>% select (tailnum)

## Задание 10
### Какая средняя температура воздуха была в сентябре в аэропорту John F Kennedy Intl (в градусах Цельсия
a<-filter(airports,name=='John F Kennedy Intl')%>% select(faa)%>% paste(sep='')
aa<-filter(weather,origin == a ,month == 9) 
(5/9)*(mean(aa$temp, na.rm=TRUE)-32)

## Задание 11
### Самолеты какой авиакомпании совершили больше всего вылетов в июне?
a <-filter(flights,month == 6) %>%
  group_by(carrier) %>% 
  summarise(aa=n()) %>% 
  arrange(desc(aa)) %>%
  head(1) %>% select(carrier) %>% paste(sep='')
 filter(airlines,carrier == a)

## Задание 12
### Самолеты какой авиакомпании задерживались чаще других в 2013 году?
a <-filter(flights,year == 2013) %>%
  group_by(carrier) %>%
  summarise(n_flights=n()) %>%
  arrange(desc(n_flights)) %>%
  head(1) %>%
  select(carrier) %>% paste(sep='')
filter(airlines,carrier==a)
