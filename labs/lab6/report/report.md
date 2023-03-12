---
## Front matter
title: "отчёт по лабораторной работе №6"
subtitle: "Задача об эпидемии"
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

Построить график для задачи об эпидемии.

# Задание

**Вариант 11**  
  Задача: на одном острове вспыхнула эпидемия. Известно, что из всех проживающих
на острове (N=17000) в момент начала эпидемии (t=0) число заболевших людей
(являющихся распространителями инфекции) I(0)=117, А число здоровых людей с
иммунитетом к болезни R(0)=17. Таким образом, число людей восприимчивых к
болезни, но пока здоровых, в начальный момент времени S(0)=N-I(0)-R(0).
Постройте графики изменения числа особей в каждой из трех групп.  
  Рассмотрите, как будет протекать эпидемия в случае:  
  1) если I(0)<=I*  
  2) если I(0)>I* 

# Теоретическое введение

Предположим, что некая популяция, состоящая из N особей, (считаем, что популяция изолирована)
подразделяется на три группы. Первая группа - это восприимчивые к болезни, но
пока здоровые особи, обозначим их через S(t). Вторая группа – это число
инфицированных особей, которые также при этом являются распространителями
инфекции, обозначим их I(t). А третья группа, обозначающаяся через R(t) – это
здоровые особи с иммунитетом к болезни.  
  До того, как число заболевших не превышает критического значения
I*, считаем, что все больные изолированы и не заражают здоровых. Когда I(t) > I*,
тогда инфицирование способны заражать восприимчивых к болезни особей.  
  Таким образом, скорость изменения числа S(t) меняется по следующему
закону: 
$\frac{dS}{dt} = -aS, если I(t) > I*$ и $\frac{dS}{dt} = 0, если I(t) <= I*$

  Поскольку каждая восприимчивая к болезни особь, которая, в конце концов,
заболевает, сама становится инфекционной, то скорость изменения числа
инфекционных особей представляет разность за единицу времени между
заразившимися и теми, кто уже болеет и лечится, т.е.: 
$\frac{dI}{dt} = aS - bI, если I(t) > I*$ и $\frac{dS}{dt} = -bI, если I(t) <= I*$  
  А скорость изменения выздоравливающих особей (при этом приобретающие
иммунитет к болезни): $\frac{dR}{dt} = bI$

  Постоянные пропорциональности a, b — это коэффициенты заболеваемости
и выздоровления соответственно.  
  Для того, чтобы решения соответствующих уравнений определялось
однозначно, необходимо задать начальные условия. Считаем, что на начало
эпидемии в момент времени t = 0 нет особей с иммунитетом к болезни R(0)=0, а
число инфицированных и восприимчивых к болезни особей I(0) и S(0) соответственно.
Для анализа картины протекания эпидемии необходимо
рассмотреть два случая: I(0)<=I* и I(0)>I*.

# Выполнение лабораторной работы

## Программа, написанная на julia

```
using DifferentialEquations
using Plots

a = 0.01 # коэффициент заболеваемости
b = 0.02 # коэффициент выздоровления
const N = 17000 # общая численность популяции
const I0 = 117 # количество инфицированных особей в начальный момент времени
const R0 = 17 # количество здоровых особей с иммунитетом в начальный момент времени
const S0 = N - I0 - R0 # количество восприимчивых к болезни особей в начальный момент времени

# случай, когда I(0)<=I*
function syst(dx, x, p, t)
    dx[1] = 0
    dx[2] = -b*x[2]
    dx[3] = b*x[2]
end

# случай, когда I(0)>I*
function syst2(dx, x, p, t)
    dx[1] = -a*x[1]
    dx[2] = -a*x[1] - b*x[2]
    dx[3] = b*x[2]
end

t0=0.0
tmax=5.0
tspan = (t0, tmax)
t = range(tspan[1], tspan[2], step=0.01)

x0 = [S0, I0, R0]
prob = ODEProblem(syst, x0, tspan)
sol = solve(prob, saveat=t)

plot(sol, label=["S(t)" "I(t)" "R(t)"], ylim=[0,1.1*N])
plot!(title="Изменения числа особей в 1 случае", xlabel="Время t", ylabel="Количество особей")
savefig("D:\\julia\\lab6_1j.png")

prob = ODEProblem(syst2, x0, tspan)
sol = solve(prob,  saveat=t)

plot(sol, label=["S(t)" "I(t)" "R(t)"], ylim=[0,1.1*N])
plot!(title="Изменения числа особей во 2 случае", xlabel="Время t", ylabel="Количество особей")
savefig("D:\\julia\\lab6_2j.png")
```

## Программа, написанная на  OpenModelica
```
model lab06 "Model for simulating epidemics"
  parameter Real a=0.01 "коэффициент заболеваемости";
  parameter Real b=0.02 "коэффициент выздоровления";
  parameter Real N=17000 "общая численность популяции";
  parameter Real I0=117 "количество инфицированных особей в начальный момент времени";
  parameter Real R0=17 "количество здоровых особей с иммунитетом в начальный момент времени";
  parameter Real S0=N-I0-R0 "количество восприимчивых к болезни особей в начальный момент времени";

  Real S(start=S0) "количество восприимчивых к болезни особей";
  Real I(start=I0) "количество инфицированных особей";
  Real R(start=R0) "количество здоровых особей с иммунитетом";

  Real S2(start=S0) "количество восприимчивых к болезни особей";
  Real I2(start=I0) "количество инфицированных особей";
  Real R2(start=R0) "количество здоровых особей с иммунитетом";
  
  
  // случай, когда I(0)<=I*
  equation 
    der(S) = 0;
    der(I) = -b*I;
    der(R) = b*I;
    
  // случай, когда I(0)>I*
  equation 
    der(S2) = -a*S2;
    der(I2) = -a*S2-b*I2;
    der(R2) = b*I2;  
    
end lab06;
```

## Результаты

Описываются проведённые действия, в качестве иллюстрации даётся ссылка на иллюстрацию (рис. @fig:001).

![Название рисунка](image/placeimg_800_600_tech.jpg){#fig:001 width=70%}

# Выводы

Здесь кратко описываются итоги проделанной работы.

# Список литературы{.unnumbered}

::: {#refs}
:::
