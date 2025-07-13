# Algoritmo-Genetico
El presente repositorio cuenta con toda la documentación necesaria para la ejecución de los Algoritmos Genéticos que buscan darle solución a un Multidimesional Knapsack Problem (MKP), un Multidimesional Bounded Knapsack Problem (MBKP), o un Multidimesional Unbounded Knapsack Problem (MUKP). Además, se presenta un código para la generación de KP aleatorios, utilizados con el fin de probar la eficiencia de los AG. De igual manera, se anexa una carpeta de las instancias (creadas con el generador de problemas), utilizadas en las pruebas desarrolladas en "".

A continuación se describe el funcionamiento de cada uno de los códigos para su utilización y/o replicación.

*Nota: Para la correcta ejecución de todos los programas se recomienda importar las bibliotecas necesarias de la siguiente manera:
 * import numpy as Np
 * import math as M
 * import random
 * import matplotlib.pyplot as Plt
-----------------------------------------------------------------------------------
*Generador de KP*

El código se encuentra en la sección "Generar KP", y se encarga de crear instancias aleatorias con *n* artículos y *m* restricciones. Dentro de este, se encuentran las siguientes funciones, las cuales permiten la modificación (interna) de sus parámetros si lo que se busca es generar problemas con caracteríticas particulares:
* La función *Peso* genera las distintas *m* magnitudes correspondientes a un mismo artículo, cuyos valores pueden comprender entre 5 y 60. 
* La función *Valor* determinar el beneficio por unidad de magnitud de un artículo (en caso de contar con diversas magnitudes, se elige una aleatoriamente), cuyos valores se extienden entre 1 y 3.
* Por su parte, *Unidades* genera la cantidad máxima de unidades disponibles por artículo, (valor de *b* en una instancia del tipo MBKP). Dicho límite puede estar entre 1 y 15.

Finalmente, la función *kp(n,m)* es justamente la encargada de generar la instancia. Sus parámetros de entrada son *n* correspondiente al número de artículos y *m*, al número de restricciones. El vector de retorno contiene:
* El vector *V*, correspondiente al vector de beneficios de los artículos, es decir:
     $$[V_{1},V_{2},V_{3},...,V_{n}]$$
* El vector *R*, contiene los coeficientes de las restricciones de capacidad, es decir, los valores de magnitudes de los articulos correspondientes a cada una de las capacidades:
     $$[[w_{11},w_{21},w_{31},\dots,w_{n1}],
      [w_{12},w_{22},w_{32},\dots,w_{n2}],
      \dots ,
      [w_{1m},w_{2m},w_{3m},\dots,w_{nm}]]$$
* 
