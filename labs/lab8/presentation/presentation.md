---
## Front matter
lang: ru-RU
title: Презентация по лабораторной работе №8
subtitle: Модель конкуренции двух фирм
author:
  - Саргсян А. Г.
institute:
  - Российский университет дружбы народов, Москва, Россия
date: 28 марта 2003

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
---

# Цели и задачи работы

## Цель лабораторной работы

Изучить модель конкуренции 

## Задание к лабораторной работе

1.	Изучить модель конкуренции двух фирм
2.	Построить соответствующие графики в двух случаях

# Процесс выполнения лабораторной работы

## Теоретический материал 

Обозначения:

$N$ - число потребителей производимого продукта. 

$S$ – доходы потребителей данного продукта.

$M$ – оборотные средства предприятия 

$\tau$ - длительность производственного цикла

$p$ - рыночная цена товара 

$\widetilde{p}$ - себестоимость продукта

$\delta$ - доля оборотных средств, идущая на покрытие переменных издержек

$k$ - постоянные издержки, которые не зависят от количества выпускаемой продукции

## Теоретический материал 

Функция спроса: 

$$Q = q - k\frac{p}{S} = q(1 - \frac{p}{p_{cr}})$$

Уравнения динамики оборотных средств:

$$ \frac{dM}{dt} = -\frac{M \delta}{\tau} + NQp - k = -\frac{M\delta}{\tau} + Nq(1 - \frac{p}{p_{cr}})p - k $$

Уравнение для рыночной цены $p$ :

$$ \frac{dp}{dt} = \gamma (-\frac{M\delta}{\tau \widetilde{p}} + Nq(1-\frac{p}{p_{cr}}) ) $$

## Теоретический материал 

При заданном M уравнение описывает быстрое стремление цены к равновесному значению цены, которое устойчиво.
В этом случае уравнение можно заменить алгебраическим соотношением

$$ -\frac{M\delta}{\tau \widetilde{p}} + Nq(1-\frac{p}{p_{cr}}) = 0$$

Равновесное значение цены $p$ равно

$$ p = p_{cr}(1 - \frac{M\delta}{\tau \widetilde{p} Nq})$$

## Теоретический материал

Уравнения динамики оборотных средств

$$\frac{dM}{dt} = -\frac{M \delta}{\tau}(\frac{p}{p_{cr}}-1) - M^2 ( \frac{\delta}{\tau \widetilde{p} })^2 \frac{p_{cr}}{Nq} - k$$

Стационарное состояние

$$ \widetilde{M_{1,2}} = \frac{1}{2} a \pm \sqrt{\frac{a^2}{4} - b}$$

где 

$$ a = Nq(1 - \frac{\widetilde{p}}{p_{cr}} \widetilde{p} \frac{\tau}{\delta}), b = kNq \frac{(\tau \widetilde{p})^2}{p_{cr}\delta ^2} $$

## Теоретический материал

При больших постоянных издержках (в случае $a^2 < 4b$) стационарных состояний нет.

При $b << a$ стационарные значения $M$ равны

$$ \widetilde{M_{+}} = Nq \frac{\tau}{\delta}(1 - \frac{\widetilde{p}}{p_{cr}})\widetilde{p}, \widetilde{M_{-}} = k\widetilde{p} \frac{\tau}{\delta(p_{cr} - \widetilde{p})} $$


# Условие задачи

## Случай 1

Рассмотрим две фирмы, производящие взаимозаменяемые товары одинакового качества и находящиеся в одной рыночной нише. Будем считать, что постоянные издержки пренебрежимо малы.

$$ \frac{dM_1}{d\Theta} = M_1 - \frac{b}{c_1}M_1 M_2 - \frac{a1}{c1} M_1^2 $$

$$ \frac{dM_2}{d\Theta} = \frac{c_2}{c_1} M_2 - \frac{b}{c_1} M_1 M_2 - \frac{a_2}{c_1} M_2^2 $$


## Случай 2

Рассмотрим модель, когда, помимо экономического фактора влияния  используются еще и социально-психологические факторы.

$$\frac{dM_1}{d\Theta} = M_1 - (\frac{b}{c_1} + 0.0002)M_1 M_2 - \frac{a1}{c1} M_1^2 $$

$$ \frac{dM_2}{d\Theta} = \frac{c_2}{c_1} M_2 - \frac{b}{c_1} M_1 M_2 - \frac{a_2}{c_1} M_2^2 $$


## Данные

$$ a_1 = \frac{p_{cr}}{\tau_1^2 \widetilde{p}_1^2 Nq } $$
$$ a_2 = \frac{p_{cr}}{\tau_2^2 \widetilde{p}_2^2 Nq } $$ 
$$ b = \frac{p_{cr}}{\tau_1^2 \widetilde{p}_1^2 \tau_2^2 \widetilde{p}_2^2 Nq} $$
$$ c_1 = \frac{p_{cr} - \widetilde{p}_1}{\tau_1 \widetilde{p}_1} $$
$$ c_2 = \frac{p_{cr} - \widetilde{p}_2}{\tau_2 \widetilde{p}_2} $$

## Числовые данные

$$ M_0^1=5 \: M_0^2=4.5 $$
$$ p_{cr}=12 \: N=40 \: q=1 $$
$$ \tau_1=20 \: \tau_2=30 $$
$$ \widetilde{p}_1=8 \: \widetilde{p}_2=5 $$

## График в первом случае

![График для случая 1](image/lab8jl1.png){ #fig:001 width=70% height=70% }

## График во втором случае

![График для случая 2](image/lab8jl2.png){ #fig:002 width=70% height=70% }

# Выводы по проделанной работе

## Вывод

В ходе выполнения лабораторной работы мы изучили модель конкуренции двух фирм и построили соответствующие графики.
