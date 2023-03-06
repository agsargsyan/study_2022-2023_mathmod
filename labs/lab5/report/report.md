---
## Front matter
title: "Отчёт по лабораторной работе 5"
subtitle: "Модель хищник-жертва"
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

Изучить модель "Хищник-Жертва" и построить графики функций

# Задание

Для модели «хищник-жертва»:

$$
 \begin{cases}
	\frac{dx}{dt}= -0.23x(t) + 0.053x(t)y(t) 
	\\   
	\frac{dy}{dt}= 0.43y(t) - 0.033x(t)y(t) 
 \end{cases}
$$

Постройте график зависимости численности хищников от численности жертв,
а также графики изменения численности хищников и численности жертв при
следующих начальных условиях: $x_0=8$ и $y_0=14$. Найдите стационарное
состояние системы.
# Теоретическое введение

Простейшая модель взаимодействия двух видов типа «хищник — жертва» -
модель Лотки-Вольтерры. Данная двувидовая модель основывается на
следующих предположениях:

1. Численность популяции жертв x и хищников y зависят только от времени
(модель не учитывает пространственное распределение популяции на
занимаемой территории)
2. В отсутствии взаимодействия численность видов изменяется по модели
Мальтуса, при этом число жертв увеличивается, а число хищников падает
3. Естественная смертность жертвы и естественная рождаемость хищника
считаются несущественными
4. Эффект насыщения численности обеих популяций не учитывается
5. Скорость роста численности жертв уменьшается пропорционально
численности хищников

$$
 \begin{cases}
	\frac{dx}{dt}= -ax(t) + bx(t)y(t) 
	\\   
	\frac{dy}{dt}= cy(t) - dx(t)y(t) 
 \end{cases}
$$

В этой модели $x$ – число жертв, $y$ - число хищников. Коэффициент $a$
описывает скорость естественного прироста числа жертв в отсутствие хищников, $с$ — 
естественное вымирание хищников, лишенных пищи в виде жертв. Вероятность
взаимодействия жертвы и хищника считается пропорциональной как количеству
жертв, так и числу самих хищников ($xy$). Каждый акт взаимодействия уменьшает
популяцию жертв, но способствует увеличению популяции хищников (члены $-bxy$
и $dxy$ в правой части уравнения). Стационарное состояние системы (положение равновесия, не зависящее
от времени решение) будет в точке: $x_{0} = \frac{c}{d}$, $y_{0} = \frac{a}{b}$ . 

# Выполнение лабораторной работы

## Расчет стационарного состояния системы

$x_{0} = \frac{c}{d} = \frac{0,23}{0,053} = 4,34$

$y_{0} = \frac{a}{b} = \frac{0,43}{0,033} = 13,03$

## Решение на языке julia

```
using Plots
using DifferentialEquations

a = 0.23  #коэффициент естественной смертности хищников
b = 0.053 #коэффициент естественного прироста жертв
c = 0.43  #коэффициент увеличения числа хищников
d = 0.033 #коэффициент смертности жертв

function syst2(dx, x, p, t)
  dx[1] = -a*x[1] + b*x[1]*x[2]
  dx[2] = c*x[2] - d*x[1]*x[2]
end

t0 = 0
tmax=400
tspan=(t0, tmax)
x0 = [8, 14] # начальное значение x и у (популяция хищников и популяция жертв)
t = collect(LinRange(t0, tmax, 8000)) 
prob = ODEProblem(syst2, x0, tspan)
sol = solve(prob, saveat=t)

y1 = [sol[i][1] for i in 1:length(sol)]
y2 = [sol[i][2] for i in 1:length(sol)]

plot(#построение графика колебаний изменения числа популяции хищников  
	t, 
	y1, 
	xlabel="Популяция хищников", 
	label="Хищники", 
	color=:yellow)
savefig("D:\\julia\\lab5_1j.png")

plot(#построение графика колебаний изменения числа популяции жертв  
	t, 
	y2,  
	xlabel="Популяция жертв", 
	label="Жертвы", 
	color=:blue
)
savefig("D:\\julia\\lab5_2j.png")

plot(# построение графика зависимости изменения численности хищников от изменения численности жертв	
	y1, 
     	y2, 
	xlabel="Популяция жертв", 
	ylabel="Популяция хищников", 
	label="Хищник против Жертвы", 
	color=:red, 
	xlim=[0,40], 
	ylim=[0,20]
) 
savefig("D:\\julia\\lab5_3j.png")
```

## Решение на OpenModelica

```
model lab05
 parameter Real a=0.23;
 parameter Real b=0.053;
 parameter Real c=0.43;
 parameter Real d=0.033;
 parameter Real x0=8;
 parameter Real y0=14;
 Real x(start=x0);
 Real y(start=y0);
equation
 der(x)=-a*x+b*x*y;
 der(y)=c*y-d*x*y;
end lab05;
```

# Результаты

## Результаты, получение с помощью julia

График колебания изменения численности хищников (рис. @fig:001).

![Колебания изменения численности хищников](image/lab5_1j.png){#fig:001 width=70%}

График колебания изменения численности жертв (рис. @fig:002).

![Колебания изменения численности жертв](image/lab5_2j.png){#fig:002 width=70%}

График зависимости изменения численности хищников от изменения численности жертв (рис. @fig:003).

![Зависимости изменения численности хищников от изменения численности жертв](image/lab5_3j.png){#fig:003 width=70%}

## Результаты, получение с помощью OpenModelica

График колебания изменения численности хищников и численности жертв (рис. @fig:004).

![Колебания изменения численности хищников и жертв](image/lab5om1.png){#fig:004 width=70%}

График зависимости изменения численности хищников от изменения численности жертв (рис. @fig:005).

![Зависимости изменения численности хищников от изменения численности жертв](image/lab5om2.png){#fig:005 width=70%}

# Выводы

Я изучил «хищник-жертва» и построил график зависимости количества хищников от количества жертв, а также графики колебаний изменений данных популяций.

# Список литературы
1. [Система «хищник — жертва»](https://ru.wikipedia.org/wiki/Система_«хищник_—_жертва»)
2. [Модель Хищник-Жертва](https://esystem.rudn.ru/pluginfile.php/1971733/mod_resource/content/2/%D0%9B%D0%B0%D0%B1%D0%BE%D1%80%D0%B0%D1%82%D0%BE%D1%80%D0%BD%D0%B0%D1%8F%20%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0%20%E2%84%96%204.pdf) 

