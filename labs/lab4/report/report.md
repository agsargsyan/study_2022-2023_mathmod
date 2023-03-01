---
## Front matter
title: "Отчёт по лабораторной работе №4"
subtitle: "Модель гармонических колебаний"
author: "Саргсян Арам Грачьяевич"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Изучить уравнение гармонического осцилятора

# Задание

Постройте фазовый портрет гармонического осциллятора и решение уравнения гармонического осциллятора для следующих случаев 

1. Колебания гармонического осциллятора без затуханий и без действий внешней
силы $\ddot{x}+12x=0$
2. Колебания гармонического осциллятора c затуханием и без действий внешней
силы $\ddot{x}+10\dot{x}+5x=0$
3. Колебания гармонического осциллятора c затуханием и под действием внешней
силы $\ddot{x}+7\dot{x}+7x=7\sin{3t}$

На итнтервале $t \in [ 0;60 ]$, шаг 0.05, $x_0=1, y_0=2$


# Теоретическое введение

Движение грузика на пружинке, маятника, заряда в электрическом контуре, а также эволюция во времени многих систем в физике, химии, биологии и других науках при определенных предположениях можно описать одним и тем же дифференциальным уравнением, которое в теории колебаний выступает в качестве основной модели. Эта модель называется линейным гармоническим осциллятором.
Уравнение свободных колебаний гармонического осциллятора имеет следующий вид:
$$\ddot{x}+2\gamma\dot{x}+\omega_0^2=0$$

где $x$ - переменная, описывающая состояние системы (смещение грузика, заряд конденсатора и т.д.), $\gamma$ - параметр, характеризующий потери энергии (трение в механической системе, сопротивление в контуре), $\omega_0$ - собственная частота колебаний.
Это уравнение есть линейное однородное дифференциальное  уравнение второго порядка и оно является примером линейной динамической системы.

При отсутствии потерь в системе ( $\gamma=0$ ) получаем уравнение консервативного осциллятора энергия колебания которого сохраняется во времени.
$$\ddot{x}+\omega_0^2x=0$$

Для однозначной разрешимости уравнения второго порядка необходимо задать два начальных условия вида
 
$$
 \begin{cases}
	x(t_0)=x_0
	\\   
	\dot{x(t_0)}=y_0
 \end{cases}
$$

Уравнение второго порядка можно представить в виде системы двух уравнений первого порядка:

$$
 \begin{cases}
	x=y
	\\   
	y=-\omega_0^2x
 \end{cases}
$$

Начальные условия для системы примут вид:

$$
 \begin{cases}
	x(t_0)=x_0
	\\   
	y(t_0)=y_0
 \end{cases}
$$

Независимые	переменные	$x, y$	определяют	пространство,	в	котором «движется» решение. Это фазовое пространство системы, поскольку оно двумерно будем называть его фазовой плоскостью.
Значение фазовых координат $x, y$ в любой момент времени полностью определяет состояние системы. Решению уравнения движения как функции времени отвечает гладкая кривая в фазовой плоскости. Она называется фазовой траекторией. Если множество различных решений (соответствующих различным 
начальным условиям) изобразить на одной фазовой плоскости, возникает общая картина поведения системы. Такую картину, образованную набором фазовых траекторий, называют фазовым портретом.

# Выполнение лабораторной работы

## Решение задачи

1. В системе с отсутствием потери энергии (колебания без затухания)
Получаем уравнение

$$\ddot{x}+12x=0$$

Переходим к двум дифференциальным уравнениям первого порядка:

$$
 \begin{cases}
	\dot{x}=y
	\\   
	\dot{y}=-12x
 \end{cases}
$$

2.  В системе с потерей энергии (колебания с затуханием)
Получаем уравнение 

$$\ddot{x}+10\dot{x}+5x=0$$

Переходим к двум дифференциальным уравнениям первого порядка:

$$
 \begin{cases}
	\dot{x}=y
	\\   
	\dot{y}=-10y-5x
 \end{cases}
$$

3. На систему действует внешняя сила.
Получаем уравнение

$$\ddot{x}+7\dot{x}+7x=7sin(3t)$$

Переходим к двум дифференциальным уравнениям первого порядка:

$$
 \begin{cases}
	\dot{x}=y
	\\   
	\dot{y}=7sin(3t)-7y-7x
 \end{cases}
$$

## Код программы (julia)

```
using Plots
using DifferentialEquations
#Параметры осциллятора
#x'' + g* x' + w^2* x = f(t)
#w - частота
#g - затухание
x0 = 1 #начальные условия
y0 = 2
u0 = [x0; y0]

#интервал решения
t0 = 0
tmax = 60
t = collect(LinRange(t0, tmax, 1200)) 
tspan = (t0, tmax)

#Колебания без затуханий и без действий внешней силы
w = 12
function syst(dy, y, p, t)
    dy[1] = y[2]
    dy[2] = -w*y[1]
end

prob = ODEProblem(syst, u0, tspan)
sol = solve(prob, saveat=t)

plot(sol, idxs=(2), color=:green)
savefig("D:\\julia\\01j.png")
plot(sol, idxs=(1, 2), color=:red)
savefig("D:\\julia\\01fj.png")

#Колебания гармонического осциллятора c затуханием и без действий внешнейсилы
w = 5
g = 10
function syst(dy, y, p, t)
    dy[1] = y[2]
    dy[2] = -g*y[2]-w*y[1]
end

prob = ODEProblem(syst, u0, tspan)
sol = solve(prob, saveat=t)

plot(sol, idxs=(2), color=:green)
savefig("D:\\julia\\02j.png")
plot(sol, idxs=(1, 2), color=:red)
savefig("D:\\julia\\02fj.png")
#Колебания гармонического осциллятора c затуханием и под действием внешней силы
w = 7
g = 7

function F(t)
    return 7*sin(3*t)
end
function syst(dy, y, p, t)
    dy[1] = y[2]
    dy[2] = -g*y[2]-w*y[1] + F(t)
end

prob = ODEProblem(syst, u0, tspan)
sol = solve(prob, saveat=t)

plot(sol, idxs=(2), color=:green)
savefig("D:\\julia\\03j.png")
plot(sol, idxs=(1, 2), color=:red)
savefig("D:\\julia\\03fj.png")
```
## Код программы (OpenModelica, 1 случай)

```
model lab4
parameter Real w = 12;
Real x(start=1);
Real y(start=2);
equation
  der(x) = y;
  der(y) = -w*x;  
end lab4;
```

## Код программы (OpenModelica, 2 случай)

```
model lab4part2
parameter Real w = 5;
parameter Real g = 10;
Real x(start=1);
Real y(start=2);
equation
  der(x) = y;
  der(y) = -g*y - w*x;
end lab4part2;
```

## Код программы (OpenModelica, 3 случай)

```
model lab4part3
parameter Real w = 7;
parameter Real g = 7;
Real x(start=1);
Real y(start=2);
equation
  der(x) = y;
  der(y) = -g*y - w*x + 7*sin(3*time);
end lab4part3;
```

# Результаты

## Колебания без затуханий и без действий внешней силы 

Для первого случая имеем следующие графики  (рис. @fig:001, рис. @fig:002).

![График решения для случая 1](image/01j.png){#fig:001 width=70%}
![Фазовый портрет для случая 1](image/01fj.png){#fig:002 width=70%}

## Колебания без затуханий и без действий внешней силы 

Для первого случая имеем следующие графики  (рис. @fig:003, рис. @fig:004).

![График решения для случая 2](image/02j.png){#fig:003 width=70%}
![Фазовый портрет для случая 2](image/02fj.png){#fig:004 width=70%}

## Колебания без затуханий и без действий внешней силы 

Для первого случая имеем следующие графики  (рис. @fig:005, рис. @fig:006).

![График решения для случая 3](image/03j.png){#fig:005 width=70%}
![Фазовый портрет для случая 3](image/03fj.png){#fig:006 width=70%}

# Выводы

В ходе выполнения лабораторной работы были построены решения уравнения 
гармонического осциллятора и фазовые портреты гармонических колебаний в трех случаях: без затухания, 
с затуханием и при действии внешней силы.

# Список литературы

1. [Гармонический осциллятор](https://ru.wikipedia.org/wiki/Гармонический_осциллятор)
2. [Гармонические колебания](https://esystem.rudn.ru/pluginfile.php/1971729/mod_resource/content/2/%D0%9B%D0%B0%D0%B1%D0%BE%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BD%D0%B0%D1%8F%20%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0%20%E2%84%96%203.pdf) 
