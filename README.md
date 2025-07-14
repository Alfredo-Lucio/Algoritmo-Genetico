# Algoritmo-Genetico
El presente repositorio cuenta con toda la documentación necesaria para la ejecución de los Algoritmos Genéticos que buscan darle solución a un Multidimesional Knapsack Problem (MKP), un Multidimesional Bounded Knapsack Problem (MBKP), o un Multidimesional Unbounded Knapsack Problem (MUKP). Además, se presenta un código para la generación de KP aleatorios, utilizados con el fin de probar la eficiencia de los AG. De igual manera, se anexa una carpeta de las instancias (creadas con el generador de problemas), utilizadas en las pruebas desarrolladas en "".

A continuación se describe el funcionamiento de cada uno de los códigos para su utilización y/o replicación.

*Nota: Para la correcta ejecución de todos los programas se recomienda importar las bibliotecas necesarias de la siguiente manera:
 * import numpy as Np
 * import math as M
 * import random
 * import matplotlib.pyplot as Plt
-----------------------------------------------------------------------------------
**Generador de KP**

El código se encuentra en la sección *Generar KP*, y se encarga de crear instancias aleatorias con *n* artículos y *m* restricciones. Dentro de este, se encuentran las siguientes funciones, las cuales permiten la modificación (interna) de sus parámetros si lo que se busca es generar problemas con caracteríticas particulares:
* La función *Peso* genera las distintas *m* magnitudes correspondientes a un mismo artículo, cuyos valores pueden comprender entre 5 y 60. 
* La función *Valor* determinar el beneficio por unidad de magnitud de un artículo (en caso de contar con diversas magnitudes, se elige una aleatoriamente), cuyos valores se extienden entre 1 y 3.
* Por su parte, *Unidades* genera la cantidad máxima de unidades disponibles por artículo, (valor de *b* en una instancia del tipo MBKP). Dicho límite puede estar entre 1 y 15.

Finalmente, la función *kp(n,m)* es justamente la encargada de generar la instancia. Sus parámetros de entrada son *n* correspondiente al número de artículos y *m*, al número de restricciones. El vector de retorno contiene:
* El arreglo *V*, correspondiente al vector de beneficios de los artículos, es decir:
     $$[V_{1},V_{2},V_{3},\dots,V_{n}]$$
* El vector *R* contiene los coeficientes de las restricciones de capacidad, es decir, los valores de magnitudes de los articulos correspondientes a cada una de las capacidades:
     $$[[w_{11},w_{12},w_{13},\dots,w_{1n}],
      [w_{21},w_{22},w_{23},\dots,w_{2n}],
      \dots ,
      [w_{m1},w_{m2},w_{m3},\dots,w_{mn}]]$$
* El vector *W* cuenta con las capacidades máximas de cada conjunto de magnitudes, es decir: $$[W_{1},W_{2},W_{2},\dots ,W_{m}]$$
* Aún si no se pretende generar un MBKP, el programa siempre regresa al vector correspondiente a las unidades máximas disponibles ($b$) por artículo: $$[b_{1},b_{2},b_{3},\dots ,b_{n}]$$
---------------------------------------------------------------------------------
**Programación Dinámica para resolver un KP**
Se trata de tres funciones descritas en la sección *Resolver un KP con una restricción*, y tal y como se puede suponer, se trata de los códigos para resolver un 0-1 *KP*, un *BKP* o un *UKP* mediante las ecuaciones de recursión descritas en "". 

Sus parámetros de entrada para los tres casos son *W* correspondiente al valor de capacidad máxima; *w* para el vector de pesos; y *V* el vector de beneficios. Además, para el caso de un *BKP*, también se requiere al vector *b* que contenga las unidades disponibles por artículo.

Las tres funciones regresaran al valor óptimo alcanzado y su vector solución.

---------------------------------------------------------------------------------
**Resolver los subproblemas que conforman a un KP**
La sección *Solución de los subproblemas KP mediante PD* contiene el código de las funciones que reciben un KP con varias restricciones, lo dividen en sus respectivos subproblemas y los resuelven individualemente.

En la sección se definen dos funciones, la primera sirve para resolver problemas del tipo *MKP* y *MUKP* y sus parámetros de entrada son:
* *V*: vector de beneficios
* *R*: el arreglo que contiene a los vectores de magnitud
* *W*: el vector que contiene a las capacidades máximas del problema
* *KP*: que refiere al tipo de problema que se quiere resolver, siendo necesario ingresar *OIKP* si el problema es del tipo *MKP*, o *UKP* si es un *MUKP*

Por otro lado, la segunda función es exclusiva para un *MBKP*; y recibe los mismos parámetros ya descritos a excepción el último (el *KP*), el cual se cambia por el vector de unidades disponibles por artículo *b*.

Ambas funciones regresan el valor óptimo más pequeño generado por los subproblemas, el vector solución que lo genera y *True* si dicha solución cumple con todas las restricciones de capacidad, o *False* si viola al menos una restricción.

---------------------------------------------------------------------------------
