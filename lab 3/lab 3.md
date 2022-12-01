





## Цель работы

1. Развить практические навыки использования языка программирования R для обработки данных
2. Закрепить знания базовых типов данных языка R
3. Развить пркатические навыки использования функций обработки данных пакета dplyr – функции
select(), filter(), mutate(), arrange(), group_by()


## Задание

Проанализировать встроенный в пакет dplyr набор данных starwars с помощью языка R и ответить на вопросы(1-11):

## Подготовка

library(dplyr)
starwars
starwars <- starwars

## Задание 1
### Сколько строк в датафрейме?
starwars %>% nrow()




## Задание 2
### Сколько столбцов в датафрейме?
starwars %>% ncol()


## Задание 3
### Как просмотреть примерный вид датафрейма?

starwars %>% glimpse()


## Задание 4
### Сколько уникальных рас персонажей (species) представлено в данных?

length(unique(starwars$species))



## Задание 5
### Найти самого высокого персонажа.

na.omit(starwars$height)
max(starwars$height)
starwars %>% filter(height==max(na.omit(starwars$height)))


## Задание 6
### Найти всех персонажей ниже 170.
na.omit(starwars$height)

starwars %>% filter(height<170)

## Задание 7
### Подсчитать ИМТ (индекс массы тела) для всех персонажей. ИМТ подсчитать по формуле 𝐼 = 𝑚/ℎ2 , где 𝑚– масса (weight), а ℎ – рост (height).

starwars %>%
  mutate(imt = mass / ((height*0.01) ^ 2)) %>%
  select(name,imt)


 
## Задание 8
### Найти 10 самых “вытянутых” персонажей. “Вытянутость” оценить по отношению массы (mass) к росту (height) персонажей.
starwars %>%
  mutate(elongation = mass/(height*0.01)) %>%
  arrange(desc(elongation)) %>%
  head(10) %>%
  select(name,elongation)


 
## Задание 9
### Найти средний возраст персонажей каждой расы вселенной Звездных войн.

starwars %>%
  filter(!(birth_year %in% NA)) %>% 
  filter(!(species %in% NA)) %>%
  group_by(species) %>%
  summarise(mean_age = mean(birth_year))


 
## Задание 10
### Найти самый распространенный цвет глаз персонажей вселенной Звездных войн.

starwars %>%
  filter(!(eye_color %in% NA)) %>%
  count(eye_color, sort = TRUE) %>%
  head(1)


 
## Задание 11
### Подсчитать среднюю длину имени в каждой расе вселенной Звездных войн.

starwars %>%
  filter(!(species %in% NA)) %>%
  group_by(species) %>%
  summarise(mean_len_name = mean(nchar(name)))




  
 
 
 