# Algoritmo-Genetico
El presente repositorio cuenta con toda la documentación necesaria para el uso y entendimiento de los Algoritmos Genéticos que buscan darle solución al Multidimesional Knapsack Problem (MKP), al Multidimesional Bounded Knapsack Problem (MBKP), o al Multidimesional Unbounded Knapsack Problem (MUKP). Además, se presenta un código para la generación de KP aleatorios, utilizados con el fin de probar la eficiencia de los AG. De igual manera, se anexa una carpeta de las instancias (creadas con el generador de problemas), utilizadas en las pruebas desarrolladas en "".

Únicamente un conjunto reducido de las funciones presentadas (de las cuales se hace mención en su respectiva descripción) requieren interacción directa con el usuario; pues el resto están diseñadas para el funcionamiento interno de los métodos desarrollados.

*Nota: Para la correcta ejecución de todos los programas se recomienda importar las bibliotecas necesarias de la siguiente manera:
 * import numpy as Np
 * import math as M
 * import random
 * import matplotlib.pyplot as Plt
-----------------------------------------------------------------------------------
**Generador de KP**

El código se encuentra en la sección *Generar KP*, y se encarga de crear instancias aleatorias con *n* artículos y *m* restricciones. Dentro de este se encuentran las siguientes funciones que si bien, no requieren interacción directa con el usuario, de así desearse se permite la modificación (interna) de sus parámetros con el fin de crear problemas con caracteríticas particulares:
* La función *Peso* genera las distintas *m* magnitudes correspondientes a un mismo artículo, cuyos valores pueden comprender entre 3 y 60. 
* La función *Valor* determinar el beneficio producido por unidad de magnitud de un artículo (en caso de contar con diversas magnitudes, se elige una aleatoriamente), cuyos valores se extienden entre 0.5 y 3.
* Para el caso de la función *Unidades*, esta se encarga del límite máximo de unidades disponibles para un mismo artículo, (valor de *b* en una instancia del tipo MBKP). Dicho límite puede estar entre 1 y 20.

Por su parte, la función *kp(n,m)* es la encargada de generar las instancias y la que requiere que sus parámetros sean definidos por el usuario. Tales valores de entrada son: *n* correspondiente al número de artículos; y *m* como el número de restricciones. Al terminar su ejecución, el vector de retorno contendrá:
* El arreglo *V*, correspondiente al vector de beneficios de los artículos, es decir:
     $$[V_{1},V_{2},V_{3},\dots,V_{n}]$$
* El vector *R*, que contiene los coeficientes de las restricciones de capacidad, es decir, los valores de magnitudes de los articulos correspondientes a cada una de las capacidades:
     $$[[w_{11},w_{12},w_{13},\dots,w_{1n}],
      [w_{21},w_{22},w_{23},\dots,w_{2n}],
      \dots ,
      [w_{m1},w_{m2},w_{m3},\dots,w_{mn}]]$$
* El vector *W* que cuenta con las capacidades máximas de cada conjunto de magnitudes, es decir: $$[W_{1},W_{2},W_{2},\dots ,W_{m}]$$
* Finalmente y aún si no se pretende generar una instancia del tipo MBKP, el programa siempre regresará al vector correspondiente a las unidades máximas disponibles ($b$) por artículo: $$[b_{1},b_{2},b_{3},\dots ,b_{n}]$$. 
---------------------------------------------------------------------------------
**Programación Dinámica para resolver un KP**

Se trata de tres funciones descritas en la sección *Resolver un KP con una restricción*, se trata de tres funciones a para resolver un 0-1 *KP*, un *BKP* o un *UKP* haciendo uso de las ecuaciones de recursión presentadas en "La Programación Dinámica". 

Si así se desea, es posible usar estos programas para resolver problemas de la mochila con una restricción ingresando sus datos de la forma en la que se describirá más adelante; sin embargo, su intención principal es servir de apoyo para la aplicación del método de solución a problemas multidimensionales, por lo que si fuera caso, no requiere interacción directa con el usuario.

Los parámetros de entrada para los tres casos son: *W* correspondiente al valor de capacidad máxima; *w* para el vector de magnitudes; y *V* el vector de beneficios. Además, si se tratara de un *BKP*, también se requiere el ingreso del vector *b* que contenga la cantidad máxima de unidades disponibles por artículo.

Las tres funciones regresarán al valor óptimo alcanzado y su vector solución.

---------------------------------------------------------------------------------
**Resolver los subproblemas que conforman a un KP**

La sección *Solución de los subproblemas KP mediante PD* contiene el código de las funciones que reciben un KP con múltiples restricciones, lo dividen en sus respectivos subproblemas y los resuelven individualmente.

Se presentan dos funciones para tal fin, la primera sirve para resolver problemas del tipo *MKP* y *MUKP*, donde sus parámetros de entrada son:
* *V*: vector de beneficios.
* *R*: el arreglo que contiene a los vectores de magnitud.
* *W*: el vector que contiene a las capacidades máximas del contenedor.
* *KP*: refiriéndose al tipo de problema que se quiere resolver, siendo necesario ingresar *OIKP* si el problema es del tipo *MKP*, o *UKP* si es un *MUKP*.

Por su parte, la segunda función está diseñada para el mismo fin que la anterior, con la diferencie de que esta es exclusiva para resolver un *MBKP*; en consecuencia, la función recibirá los mismos parámetros descritos a excepción el último (el *KP*), el cual se sustituye por el vector *b*.

Ambas funciones regresan el valor óptimo más pequeño generado por los subproblemas, el vector solución que lo genera y *True* si dicha solución cumple con todas las restricciones de capacidad, o *False* si viola al menos una de ellas.

El uso de estas funciones corre a cargo del usuario, quien deberá ingresar los parámetros manualmente

---------------------------------------------------------------------------------
**Funciones de apoyo**

En la sección *Operadores* se encuentran todas las funciones necesarias para la correcta ejecución de los Algoritmos genéticos, además, debido a que funcionan de manera interna dentro de estos, no requieren manipulación directa del usuario. 

Para facilitar su comprensión, estas se encuentran clasificadas según su utilidad para los distintos AG:
1. Universales: Sirven para todos los modelos de *KP*
     * *Grafica*: Se trata de una función que muestra visualmente la evolución de la mejor solución a través de las generaciones.
     * *EvCapacidad*: Evalua si un candidato a solución o cromosoma cumple con todas las restricciones de capacidad.
     * *Aptitud*: Calcula la aptitud de un cromosoma.
     * *Torneo*: Aplica el operador genético del mismo nombre a los cromosomas de una población.
     * *Cruce*: Aplica el cruce uniforme a dos cromosomas padre
2. Exclusivos del *MKP*: Su uso es único para resolver un *MKP*.
     * *Población_InicialOI*: genera la población inicial para un AG, donde se asigna una pequeña parte a cromosomas creados alrededor de una solución de partida. Por defecto, esta porción está configurada en un 10%.
     * *Población_InicialOI2*: genera la población inicial para la aplicación de un AG sin considerar una solución de partida.
     * *Intercambiar*: función diseñada para generar soluciones factibles a partir de una solución de partida, su labor consiste en hacer intercambios al azar de pares aleatorios de genes en un mismo cromosoma.
     * *ApagarOI*: función que toma una solución de partida y transforma aleatoriamente los genes cuyo valor original fuera 1 en 0. Su objetivo es generar cromosomas cercanos a dicha solución.
     * *MutaciónOI*: aplica el operador del mismo nombre a los genes de un cromosoma bajo cierta probabilidad.
3. Generales para el *MBKP* y el *MUKP*.
     * *MutaciónBUKP*: aplica el operador del mismo nombre a los genes de un cromosoma bajo cierta probabilidad.
     * *Truncamientos*: toma una solución de partida y trunca sus valores para asegurarse que cumpla con todas las restricciones de capacidad y de unidades máximas.
4. Exclusivos del *MBKP*: su uso es único para los Algoritmos Genéticos que resuelvan un *MBKP*.
     * *CapacidadLimiteBKP*: crea un nuevo vector $\bar{b}$ que ahora considera a las restricciones de capacidad para limitar el número máximo de unidades que se pueden llevar de un mismo articulo.    
     * *ReducirBKP*: toma una solución de partida ya truncada y reduce de forma aleatoria los valores de sus genes con el fin de generar cromosomas cercanos a ella.
     * *Poblacion_InicialBKP*: genera la población inicial para el algortimo genético, considerando una solución de partida.
     * *Poblacion_InicialBKP2*: genera la población inicial para el algortimo genético, sin considerar una solución de partida.
5. Exclusivos del *MUKP*: su uso es único para los Algoritmos Genéticos que resuelvan un *MUKP*.
     * *CapacidadLimiteUKP*: crea un vector $b$ para limitar el número máximo de unidades que se pueden llevar de un mismo articulo según las restricciones de capacidad.
     * *ReducirUKP*: toma una solución de partida ya truncada y reduce de forma aleatoria los valores de sus genes con el fin de generar cromosomas cercanos a ella.
     * *Poblacion_InicialUKP*: genera la población inicial para el algortimo genético, considerando una solución de partida.
     * *Poblacion_InicialUKP2*: genera la población inicial para el algortimo genético, sin considerar una solución de partida.
---------------------------------------------------------------------------------
**Algoritmos Genéticos**

En la sección *AG para un MKP*, se encuentran el cuerpo principal de dos versiones de algoritmo genético para resolver un *MKP*. Dichas funciones requieren que los parámetros sean definidos por el usuario.

Tales parámetros y el orden con el que se ingresan en ambos métodos se describen a continuación:

* *P*: Arreglo que contiene a los elementos del problema ordenados como sigue: $$P=[V,R,W]$$.
* *X*: Arreglo que contiene al vector resultante de ejecutar la función *Evaluacion*.
* *N*: Tamaño de la población.
* *G*: Número de generaciones aejecutar.
* *ProbMut*: Probabilidad de que ocurra una mutación: $0<\mbox{ProbMut}<1$

Como se puede apreciar, el primero método requiere entre sus parámetros al vector salida de la función *Evaluacion* para así trabajar con una solución de partida. Mientras que, para el segundo método, dicho parámetro se omite en su totalidad.

Ambas funciones generan un gráfico de la evolución de la mejor solución por generación de forma automática. Además de devolver al cromosoma con mayor aptitud y al valor que este genera al finalizar todo el proceso.

En la secciones *AG para un MBKP* y *AG para un MUKP* se encuentran los algoritmos para tales problemas; los cuales operan bajo las condiciones ya descritas. Con clara excepción del *MBKP*, donde el arreglo *P* debe contener al vector *b* definido al final, es decir, este debería estar compuesto de la siguiente forma: $$P=[V,R,W,b]$$

--------------------------------------------------------------------
**Algoritmos modificados**

Contiene a una versión alternativa de los Algortimos Genéticos que no requieren el ingreso del parámetro correspondiente a la cantidad de generaciones a realizar, pues en su lugar, el método está diseñado para ejecutarse ininterrumpidamente hasta que la solución encontrada no cambie en al menos 100 generaciones. En consecuencia, sus parámetros de entrada son únicamente:

* *P*: Arreglo que contiene a los elementos del problema ordenados como sigue: $$P=[V,R,W]$$.
* *X*: Arreglo que contiene al vector resultante de ejecutar la función *Evaluacion*.
* *N*: Tamaño de la población.
* *ProbMut*: Probabilidad de que ocurra una mutación: $0<\mbox{ProbMut}<1$

Estos algoritmos son una versión alternativa a los métodos que funcionan a partir de una solución de partida, por lo que para su correcto funcionamiento, tambien requieren de esta. 

--------------------------------------------------------------------
**Instancias de ejemplo**

Es esta carpeta se encuentran todas las instancias de todos los modelos, utilizadas en las pruebas, además de un grupo especial perteneciente al *MKP* donde se cumple el primer punto del Teorema 1.

Cada instancia ya se encuentra escrita para simplemente copiar y pegar los datos del problema en la terminal de trabajo; adicionalmente, en la parte inferior se encuentra el vector correspondiente a la mejor solución encontrada hasta el momento junto con el valor óptimo que genera.
