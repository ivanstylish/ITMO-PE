# 离散作业

## 作业1

## 作业2

## 作业3

## 作业4 

### Графо-теоретический подход к синтезу топологии

Для схем с однослойной коммутацией синтез топологии по традиционной схеме размещение-трассировка не оправдан, т.к. при этом учитываются метрические, а не топологические критерии и ограничения. 

При неравномерном использовании коммутационных слоев (например, когда слои изготавливаются на основе алюминия и поликремния) проектирование двухслойных схем оказывается близким к проектированию однослойных схем.

Графо-теоретический подход к синтезу топологии состоит из следующих этапов.

1. Построение графовой модели схемы.
2. Анализ планарности графа.
3. Планаризация графа.
4. Реализация непланарных соединений.
5. Построение плоского чертежа схемы.
6. Синтез геометрии схемы.

Одной из основных топологических задач проектирования коммутации является возможность разложения соединений на плоскости без пересечений. Эта задача связана с определением планарности графа. 

Среди критериев планарности графа наиболее известен критерий **Понтрягина-Куратовского**:

Граф $G(X,U)$ – планарен тогда и только тогда, когда он не содержит подграфов гомеоморфных полному графу $K_5$ или полному двудольному графу $K_{3,3}$.

Однако он неконструктивен (требует перебора). Известны другие критерии, но их также трудно использовать. Разработан ряд алгоритмов определения планарности графа удобных для реализации на ЭВМ.

**Критерий Бадера**. Граф $G(X,U)$ планарен, если его граф пересечений $G'$ является бихроматическим (двудольным) графом. Критерий справедлив для графов, имеющих гамильтонов цикл.

### Разбиение графа на планарные суграфы

При разработке топологии возникает задача выделения из графа, описывающего схему, максимальных планарных суграфов (добавление любого ребра делает его не планарным).

Граф $G(X,U)$ называется m-планарным, если существует m планарных суграфов $L_1(X,Z_1)$, $L_2(X,Z_2)$,…, $L_m(X,Z_m)$, таких, что  
Наименьшее m называется толщиной графа.

$$U=\bigcup^m_{i=1}Z_i$$

### Построение графа пересечений $G’$

Приняты следующие допущения:
1. Граф $G$ имеет гамильтонов цикл;
2. Два ребра пересекаются только один раз;
3. Ребра, инцидентные одной вершине, не пересекаются;
4. Ребра графа не пересекают ребер гамильтонова цикла;
5. Ребра вершины $x_j$ могут пересекать ребра вершины $x_i$ при условии, что  $j>i$.

<div align=center><img src="pic/Homework4-1.png"></div>

$p_i$ – число пересечений ребер i-ой вершины.

Согласно п. 5 принятых допущений $p_1=0$.

Рассмотрим ребро $(x_2x_n)$. Число его пересечений с ребрами вершины $x_1$

$$p_{2n}-2_{2n}\sum^{n-1}_{i=3}r_{1i}$$






## 作业5

## 作业6