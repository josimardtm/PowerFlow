## Ecuaciones fundamentales del flujo de potencia

Keywords: `Equations` `Power flow` `Formulation`

### Requerimientos

* Lectura de referencias a pie de página
* [Admitancia](https://es.wikipedia.org/wiki/Admitancia)
* [Matriz de admitancias](https://es.wikipedia.org/wiki/Admitancia)
* Valores por unidad

### Modelo balanceado en estado estacionario de un sistema de potencia

Los sistemas de potencia contienen una gran cantidad de elementos que permiten conectar a los consumidores de energía eléctrica con las fuentes de generación.

En estado estacionario, estos sistemas se pueden representar por modelos simplificados que permiten conformar circuitos para realizar un análisis de sus condiciones de operación.

El punto de partida para la formulación del problema de flujo de potencia es un diagrama unifilar del sistema que proporciona los datos de entrada. Entre estos datos se requiere: Información de los nodos, de las líneas de transmisión y de los transformadores.
<div align="center">
    <br><img alt="Ejemplo de diagrama unifilar de un sistema de potencia." src="Graph/unifilar.svg" title="Diagrama unifilar" width="70%"/>
</div>

Cada uno de los nodos $k$ se asocia con cuatro variables principales: 
* Magnitud de la tensión $V_k$
* Ángulo de fase de la tensión $\delta_k$
* Potencia activa inyectada $P_k$
* Potencia reactiva inyectada $Q_k$

Las líneas de transmisión se representan por un equivalente $\pi$ balanceado. Se debe tener como dato la impedancia en serie y en derivación (líneas medias y largas).

Todos los valores se representan en el sistema por unidad [^1]. 

Adicionalmente, se debe conocer la matriz de admitancias del sistema, que se obtiene de los datos de las líneas de transmisión y transformadores. Esta matriz cuadrada tiene tantas filas o columnas como nodos hay en el sistema.
* Cantidad de nodos $n$
* Matriz de admitancias de nodos $[Y_{bus}]$
* Los elementos de la matriz de admitancias son: $Y_{kk}=$ suma de las admitancias conectadas al nodo $k$ y $Y_{km}=$ -(suma de los elementos conectados entre los buses $k$ y $m$ con $k \ne m$)

### Corrientes inyectadas a cada nodo

Las corrientes inyectadas a cada uno de los nodos del sistema de potencia se pueden calcular a partir de los voltajes y la matriz de admitancias.

$$\mathbf{[I_{bus}]=[Y_{bus}][V_{bus}]}$$
<div align="center">
    <br><img alt="Diagrama de dos nodos." src="Graph/corrientes.svg" title="Diagrama de admitancias" width="45%"/>
</div>

Por ejemplo, para dos nodos como se muestran en la figura se tiene: 
$$\mathbf{I_1}=\mathbf{V_1}Y_g+(\mathbf{V_1}-\mathbf{V_2})Y_s$$

$$\mathbf{I_2}=\mathbf{V_2}Y_g+(\mathbf{V_2}-\mathbf{V_1})Y_s$$

En este caso, la matriz de admitancias se define como:

$$\left[ Y_{bus} \right]=
\begin{bmatrix}
        Y_{11}&Y_{12}\\
        Y_{21}&Y_{22}
\end{bmatrix}
$$

Donde:

$$ Y_{11}=Y_g+Y_s$$

$$ Y_{22}=Y_g+Y_s$$

$$ Y_{12}=Y_{21}=Y_s$$

### Potencia inyectada a cada nodo

La potencia inyectada a cada nodo por convención es la resta de la potencia generada menos la potencia demandada.

$$S_k=S_{Gk}-S_{Lk}$$

$$P_k=P_{Gk}-P_{Lk}$$ 

$$Q_k=Q_{Gk}-Q_{Lk}$$

<div align="center">
    <br><img alt="Balance de potencia en un nodo." src="Graph/nodok.svg" title="Balance de potencia en un nodo" width="45%"/>
</div>

Para el ejemplo de dos nodos, la potencia compleja inyectada a cada nodo es:

$$ S_1=S_{G1}-S_{L1}=P_1+jQ_1=\mathbf{V_1} \mathbf{I_1}^*$$

$$ S_2=S_{G2}-S_{L2}=P_2+jQ_2=\mathbf{V_2} \mathbf{I_2}^*$$

Sustituyendo las corrientes inyectadas, se tiene:

$$ S_1=\mathbf{V_1} \left[ \mathbf{V_1}Y_g+(\mathbf{V_1}-\mathbf{V_2})Y_s \right]^*$$

$$ S_2=\mathbf{V_2} \left[\mathbf{V_2}Y_g+(\mathbf{V_2}-\mathbf{V_1})Y_s \right]^*$$

Igualmente,

$$ S_1=\mathbf{V_1} \left[ \mathbf{V_1}Y_{11}+\mathbf{V_2}Y_{12} \right]^*$$

$$ S_2=\mathbf{V_2} \left[\mathbf{V_2}Y_{21}+\mathbf{V_1}Y_{22} \right]^*$$

De manera mas resumida:

$$ S_1=\mathbf{V_1} \sum_{k=1}^{2}\mathbf{V_k}^* Y_{1k}^* = V_1 \sum_{k=1}^{2} |y_{1k}| V_k  e^{j(\delta_1-\delta_k-\theta_1k)}$$

$$ S_2=\mathbf{V_2} \sum_{k=1}^{2}\mathbf{V_k}^* Y_{2k}^* = V_2 \sum_{k=1}^{2} |y_{2k}| V_k  e^{j(\delta_2-\delta_k-\theta_2k)}$$

Estas ecuaciones se pueden extender para una cantidad $n$ de nodos, suponiendo que se conoce la matriz de admitancias. 

$$ S_i=\mathbf{V_i} \sum_{k=1}^{n}\mathbf{V_k}^* Y_{ik}^* = V_i \sum_{k=1}^{n} |y_{ik}| V_k e^{j(\delta_i-\delta_k-\theta_ik)}$$

$$ i=1,2,...,n $$

También, se pueden expresar en parte real e imaginaria para poder obtener las potencias activa y reactiva

$$ P_i = V_i \sum_{k=1}^{n} |y_{ik}| V_k cos(\delta_i-\delta_k-\theta_ik)$$

$$ Q_i = V_i \sum_{k=1}^{n} |y_{ik}| V_k sin(\delta_i-\delta_k-\theta_ik)$$

$$ i=1,2,...,n $$

Las admitancias también se pueden mostrar en forma rectangular:

$$ P_i = V_i \sum_{k=1}^{n} V_k [G_{ik} cos(\delta_i-\delta_k) + B_{ik} sen(\delta_i-\delta_k)]$$

$$ Q_i = V_i \sum_{k=1}^{n} V_k [G_{ik} sen(\delta_i-\delta_k) - B_{ik} cos(\delta_i-\delta_k)]$$

$$ i=1,2,...,n $$

La solución del problema de flujo de potencia usando el método de Newton-Raphson se basa en las ecuaciones de potencia inyectada.

Este conjunto de ecuaciones no lineales permite obtener la solución para las variables desconocidas de cada uno de los nodos. Las variables a calcular dependen del [tipo de nodo](../01.02.Classification/Readme.md) en estudio.

### Ejemplo

Se tiene una red de potencia de tres nodos cuyos datos están dados en valores por unidad calculados con base de potencia de $100 MVA$ y tensión igual a $100k V$.

En la siguiente figura se muestra el diagrama unifilar de la red, con las impedancias de las líneas de transmisión.

<div align="center">
        <img src="Graph\unif-ejemplo.svg" title="Diagrama unifilar ejemplo 1" width="50%"/>
</div>

Si se tienen valores conocidos para los voltajes en cada uno de los nodos, se pueden calcular las potencias activa y reactiva inyectadas. Para ello, inicialmente se debe determinar la matriz de admitancias del sistema.

Se calcula la matriz de admitancias:

$$ Y_{11} = \frac{1}{{0,02 + \mathrm{j}0,04}} + \frac{1}{{0,02 + \mathrm{j}0,06}} = 15 - \mathrm{j}35  \text{pu} $$

$$ Y_{22} = \frac{1}{{0,02 + \mathrm{j}0,04}} + \frac{1}{{0,01 + \mathrm{j}0,02}} = 30 - \mathrm{j}60  \text{pu} $$

$$ Y_{33} = \frac{1}{{0,02 + \mathrm{j}0,06}} + \frac{1}{{0,01 + \mathrm{j}0,02}} = 25 - \mathrm{j}55  \text{pu} $$

$$Y_{12}=Y_{21}= -\frac{1}{0,02 + \mathrm{j} 0,04}=-10 + \mathrm{j} 20 \text{pu}$$

$$Y_{13}=Y_{31}= -\frac{1}{0,02 + \mathrm{j} 0,06}=-5 + \mathrm{j} 15 \text{pu}$$

$$Y_{23}=Y_{32}= -\frac{2}{0,02 + \mathrm{j} 0,04}=-20 + \mathrm{j} 40 \text{pu}$$ 

> En el caso de las líneas que conectan los nodos 2 y 3 se debe tener en cuenta que se conectan en paralelo.

La matriz de admitancia del sistema es la siguiente:

$$ [Y_{bus}]=\begin{bmatrix}
15-\mathrm{j}35 & -10+\mathrm{j}20 & -5+\mathrm{j}15 \\
-10+\mathrm{j}20 & 30-\mathrm{j}60 & -20+\mathrm{j}40 \\
-5+\mathrm{j}15 & -20+\mathrm{j}40 & 25-\mathrm{j}55 \\
\end{bmatrix} $$

Si los valores de voltaje para cada nodo son: $ \mathbf{V_1} = 1,0 \angle 0^{\circ}$, $ \mathbf{V_2} = 1,02 \angle 10^{\circ}$ y $\mathbf{V_3} = 1,02 \angle -5^{\circ}$

Las potencias inyectadas se calculan como: 

$$ S_1 = \mathbf{V_1} \mathbf{I_1}^* = \mathbf{V_1} \left[ \mathbf{V_1}Y_{11} + \mathbf{V_2}Y_{12} + \mathbf{V_3}Y_{13} \right]^*$$

$$ S_2 = \mathbf{V_2} \mathbf{I_2}^* = \mathbf{V_2} \left[\mathbf{V_1}Y_{21} + \mathbf{V_2}Y_{22} + \mathbf{V_3}Y_{23} \right]^*$$

$$ S_2 = \mathbf{V_3} \mathbf{I_3}^* = \mathbf{V_3} \left[\mathbf{V_1}Y_{31} + \mathbf{V_2}Y_{32} + \mathbf{V_3}Y_{33} \right]^*$$


[Ejemplo](EjemploEcuaciones.ipynb)



### Control de versiones

| Versión    | Descripción        | Autor                                       | Horas |
|------------|:-------------------|---------------------------------------------|:-----:|
| 2023.07.28 | Versión preliminar | [josimardtm](https://github.com/josimardtm) |   6   |

_PowerFlow es de uso libre para fines académicos, conoce nuestra licencia, cláusulas, condiciones de uso y como referenciar los contenidos publicados en este repositorio, dando [clic aquí](../../LICENSE.md)._

_¿Encontraste útil este repositorio? Apoya su difusión marcando este repositorio con una ⭐ o síguenos dando clic en el botón Follow de [Josimardtm](https://github.com/josimardtm) en GitHub._

| [Anterior](../Readme.md) | [:house: Inicio](../../README.md) | [:beginner: Ayuda / Colabora](https://github.com/josimardtm/PowerFlow/discussions) | [Siguiente](../01.02.Classification/Readme.md) |
|--------------------------|-----------------------------------|------------------------------------------------------------------------------------|------------------------------------------------|

[^1]:[Sistema de valores por unidad](https://es.wikipedia.org/wiki/Sistema_por_unidad)

<div align="center">
    <a href="https://enlace-academico.escuelaing.edu.co/psc/FORMULARIO/EMPLOYEE/SA/c/EC_LOCALIZACION_RE.LC_FRM_ADMEDCO_FL.GBL" target="_blank"><img src="../../.icons/banner-pie-de-pagina.jpg" alt="Certificado" width="100%" border="0" /></a>
</div>

[comment]:<> (Referencias [^1]: Tomado y/o adaptado de https://www.scielo.org.mx/scielo.php?pid=S2007-78902020000800028&script=sci_arttext#:~:text=El%20desarrollo%20colaborativo%20se%20refiere,inform%C3%A1tico%20funcional%20y%20de%20calidad.)
[comment]:<> (Enlace a video, imagen de cabecera, alcance, objetivos, requerimientos, diagrama general de procesos, conceptos)
[comment]:<> (Procedimiento, Actividades complementarias, Preguntas y respuestas, referencias, control de versiones)
