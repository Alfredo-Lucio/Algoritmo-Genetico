# Algoritmo-Genetico
El presente repositorio cuenta con toda la documentación necesaria para la ejecución de los Algoritmos Genéticos que buscan darle solución a un Multidimesional Knapsack Problem (MKP), un Multidimesional Bounded Knapsack Problem (MBKP), o un Multidimesional Unbounded Knapsack Problem (MUKP). Además, se presenta un código para la generación de KP aleatorios, utilizados con el fin de probar la eficiencia de los AG. De igual manera, se anexa una carpeta de las instancias (creadas con el generador de problemas), utilizadas en las pruebas desarrolladas en "".

Únicamente un conjunto reducido de las funciones presentadas (de las cuales se hace mención en su respectiva descripción) requieren interacción directa con el usuario; sin embargo el resto de ellas son vitales para el correcto desarrollo de los métodos desarrollados.

A continuación se describe el funcionamiento de cada uno de los códigos para su utilización y/o replicación.

*Nota: Para la correcta ejecución de todos los programas se recomienda importar las bibliotecas necesarias de la siguiente manera:
 * import numpy as Np
 * import math as M
 * import random
 * import matplotlib.pyplot as Plt
-----------------------------------------------------------------------------------
**Generador de KP**

El código se encuentra en la sección *Generar KP*, y se encarga de crear instancias aleatorias con *n* artículos y *m* restricciones. Dentro de este, se encuentran las siguientes funciones que si bien, no requieren interacción directa con el usuario/a, de así requerirlo, permiten la modificación (interna) de sus parámetros con el fin de crear problemas con caracteríticas particulares:
* La función *Peso* genera las distintas *m* magnitudes correspondientes a un mismo artículo, cuyos valores pueden comprender entre 3 y 60. 
* La función *Valor* determinar el beneficio por unidad de magnitud de un artículo (en caso de contar con diversas magnitudes, se elige una aleatoriamente), cuyos valores se extienden entre 0.5 y 3.
* Por su parte, *Unidades* genera la cantidad máxima de unidades disponibles por artículo, (valor de *b* en una instancia del tipo MBKP). Dicho límite puede estar entre 1 y 20.

Finalmente, la función *kp(n,m)* es justamente la encargada de generar la instancia y la que requiere que sus parámetros sean definidos por el usuario/a. Dichos valores de entrada son: *n* correspondiente al número de artículos; y *m* como el número de restricciones. El vector de retorno contiene:
* El arreglo *V*, correspondiente al vector de beneficios de los artículos, es decir:
     $$[V_{1},V_{2},V_{3},\dots,V_{n}]$$
* El vector *R*, el cual contiene los coeficientes de las restricciones de capacidad, es decir, los valores de magnitudes de los articulos correspondientes a cada una de las capacidades:
     $$[[w_{11},w_{12},w_{13},\dots,w_{1n}],
      [w_{21},w_{22},w_{23},\dots,w_{2n}],
      \dots ,
      [w_{m1},w_{m2},w_{m3},\dots,w_{mn}]]$$
* El vector *W* que cuenta con las capacidades máximas de cada conjunto de magnitudes, es decir: $$[W_{1},W_{2},W_{2},\dots ,W_{m}]$$
* Aún si no se pretende generar un MBKP, el programa siempre regresa al vector correspondiente a las unidades máximas disponibles ($b$) por artículo: $$[b_{1},b_{2},b_{3},\dots ,b_{n}]$$. 
---------------------------------------------------------------------------------
**Programación Dinámica para resolver un KP**

Se trata de tres funciones descritas en la sección *Resolver un KP con una restricción*, y tal y como se puede suponer, se trata de los códigos para resolver un 0-1 *KP*, un *BKP* o un *UKP* mediante las ecuaciones de recursión descritas en "". 

Si así se desea, es posible usar estos programas para resolver problemas de la mochila con una restricción ingresando sus datos de la forma en la que se describe más adelante; sin embargo, su intención principal es servir de apoyo para la aplicación del método de solución a problemas multidimensionales, por lo que en este caso, no requiere interacción directa con el usuario/a.

Los parámetros de entrada para los tres casos son: *W* correspondiente al valor de capacidad máxima; *w* para el vector de magnitudes; y *V* el vector de beneficios. Además, para el caso de un *BKP*, también se requiere al vector *b* que contenga las unidades disponibles por artículo.

Las tres funciones regresaran al valor óptimo alcanzado y su vector solución.

---------------------------------------------------------------------------------
**Resolver los subproblemas que conforman a un KP**

La sección *Solución de los subproblemas KP mediante PD* contiene el código de las funciones que reciben un KP con varias restricciones, lo dividen en sus respectivos subproblemas y los resuelven individualmente.

Se presentan dos funciones para tal fin, la primera sirve para resolver problemas del tipo *MKP* y *MUKP* donde sus parámetros de entrada son:
* *V*: vector de beneficios.
* *R*: el arreglo que contiene a los vectores de magnitud.
* *W*: el vector que contiene a las capacidades máximas del problema.
* *KP*: que refiere al tipo de problema que se quiere resolver, siendo necesario ingresar *OIKP* si el problema es del tipo *MKP*, o *UKP* si es un *MUKP*.

Por su parte, la segunda función es exclusiva para un *MBKP*; y recibe los mismos parámetros ya descritos a excepción el último (el *KP*), el cual se cambia por el vector de unidades disponibles por artículo, *b*.

Ambas funciones regresan el valor óptimo más pequeño generado por los subproblemas, el vector solución que lo genera y *True* si dicha solución cumple con todas las restricciones de capacidad, o *False* si viola al menos una de ellas.

El uso de estas funciones corre a cargo del usuario/a, quien deberá ingresar los parámetros manualmente

---------------------------------------------------------------------------------
**Funciones de apoyo**

En la sección *Operadores* se encuentran todas las funciones necesarias para la correcta ejecución de los Algoritmos genéticos. Debido a que funcionan de manera interna dentro de estos, no requieren manipulación directa del usuario/a. Para facilitar su comprensión, estas se encuentran clasificadas según su utilidad para los distintos AG:
1. Universales: Sirven para todos los modelos de *KP*
     * *Grafica(Y)*: Se trata de una función que grafica la evolución de la mejor solución a través de las generaciones.
     * *EvCapacidad(R,W,S)*: Evalua si un candidato a solución o cromosoma cumple con todas las restricciones de capacidad.
     * *Aptitud(V,S)*: Calcula la aptitud de un cromosoma.
     * *Torneo(Poblacion,F)*: Aplica el operador genético del mismo nombre a los cromosomas de una población.
     * *Cruce(Padre1,Padre2)*: Aplica el cruce uniforme a dos cromosomas padre
2. Exclusivos del *MKP*: Su uso es único para resolver un *MKP*.
     * *Población_InicialOI(R,W,N,V)*: genera la población inicial para un AG, donde se asigna una parte (miníma) a cromosomas creados alrededor de una solución de partida. 
     * *Población_InicialOI2(R,W,N,X,V)*: genera la población inicial para un AG sin considerar una solución de partida.
     * *Intercambiar(S)*: función diseñada para generar soluciones factibles a partir de una solución de partida, su labor consiste en hacer intercambios aleatorios de los genes de un cromosoma.
     * *ApagarOI(S)*: función que toma una solución de partida y transforma genes aleatorios cuyo valor original fuera 1 en 0. Su objetivo es generar cromosomas cercanos a dicha solución.
     * *MutaciónOI(Hijo,ProbMut)*: aplica el operador del mismo nombre a los genes de un cromosoma bajo cierta probabilidad.
3. Generales para el *MBKP* y el *MUKP*: Funciones exclusivas para resolver un *MBKP* o un *MUKP* mediante un Algoritmo Genético.
     * *MutaciónBUKP(Hijo,ProbMut)*: aplica el operador del mismo nombre a los genes de un cromosoma bajo cierta probabilidad.
     * *Truncamientos(S,b)*: toma una solución de partida y trunca sus valores para asegurarse que cumpla con todas las restricciones de capacidad y de unidades máximas.
4. Exclusivos del *MBKP*: su uso es único para los Algoritmos Genéticos que resuelvan un *MBKP*.
     * *CapacidadLimiteBKP(R,W,b)*: crea un nuevo vector $\bar{b}$ que ahora considera a las restricciones de capacidad para limitar el número máximo de unidades que se pueden llevar de un mismo articulo. Si dicho valor es menor al calculado por la función, se mantiene sin cambios.     
     * *ReducirBKP(S,b)*: toma una solución de partida ya truncada y reduce de forma aleatoria los valores de sus genes con el fin de genera cromosomas cercanos a ella.
     * *Poblacion_InicialBKP(R,W,N,X,V,b)*: genera la población inicial para el algortimo genético, considerando una solución de partida.
     * *Poblacion_InicialBKP2(R,W,N,V,b)*: genera la población inicial para el algortimo genético, sin considerar una solución de partida.
5. Exclusivos del *MUKP*: su uso es único para los Algoritmos Genéticos que resuelvan un *MUKP*.
     * *CapacidadLimiteUKP(R,W)*: crea un vector $b$ para limitar el número máximo de unidades que se pueden llevar de un mismo articulo según las restricciones de capacidad.
     * *ReducirUKP(S,b)*: toma una solución de partida ya truncada y reduce de forma aleatoria los valores de sus genes con el fin de genera cromosomas cercanos a ella.
     * *Poblacion_InicialUKP(R,W,N,X,V,b)*: genera la población inicial para el algortimo genético, considerando una solución de partida.
     * *Poblacion_InicialUKP2(R,W,N,V,b)*: genera la población inicial para el algortimo genético, sin considerar una solución de partida.
---------------------------------------------------------------------------------
**Algoritmos Genéticos**

En la sección *AG para un MKP*, se encuentran el cuerpo principal de dos versiones de algoritmo genético para resolver un *MKP*. Dichas funciones requieren que los parámetros sean definidos por el usuario/a.

Tales parámetros y el orden con el que se ingresan en ambos métodos se describen a continuación:

* *P*: Arreglo que contiene a los elementos del problema tal y como ya se han descrito anteriormente, es decir, $$P=[V,R,W]$$.
* *X*: Arreglo que contiene la salida de la función *Evaluación(V,R,W,OIKP)*.
* *N*: Tamaño de la población.
* *G*: Número de generaciones que se quieren ejecutar.
* *ProbMut*: Probabilidad de mutación, la cual debe definirse $0<\mbox{ProbMut}<1$

Como se aprecia, el primero requiere entre sus parámetros al vector salida de la función *Evaluación(V,R,W,OIKP)* para así trabajar con una solución de partida. Para el caso del segundo y al generar toda la población inicial de forma aleatoria, dicho parámetro se omite en su totalidad.

Ambos métodos generan un gráfico de la evolución de la mejor solución por generación de forma automática. Además de devolver al cromosoma con mayor aptitud y el valor que genera, al finalizar todo el proceso.

En la secciones *AG para un MBKP* y *AG para un MUKP* se encuentran los algoritmos para resolver un *MBKP* y un *MUKP* respecitvamente, los cuales operan bajo las condiciones que ya se han mencionado. Con clara excepción del *MBKP*, donde el arreglo *P* debe contener al vector *b* definido al final, es decir, debería estar compuesto de la siguiente forma: $$P=[V,R,W,b]$$

--------------------------------------------------------------------
**Instancias de ejemplo**
