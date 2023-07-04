## Actividad 1 - Ecuaciones fundamentales del flujo de potencia

Keywords: `Equations` `Power flow` `Formulation`

### Requerimientos

* Lectura de referencias a pie de página
* [Admitancia](https://es.wikipedia.org/wiki/Admitancia)
* [Matriz de admitancias](https://es.wikipedia.org/wiki/Admitancia)
* Valores por unidad

### Modelo balanceado en estado estacionario de un sistema de potencia

Los sistemas de potencia contienen una gran cantidad de elementos que permiten conectar a los consumidores de energía eléctrica con las fuentes de generación.

En estado estacionario, estos sistemas se pueden representar por modelos simplificados que permiten conformar circuitos para realizar un análisis de sus condiciones de operación.

El punto de partida para la formulación del problema de flujo de potencia es un diagrama unifilar del sistema que proporciona los datos de entrada. Entre estos datos se requiere: Información de los buses, de las líneas de transmisión y de los transformadores.
<div align="center">
    <br><img alt="Ejemplo de diagrama unifilar de un sistema de potencia." src="Graph/unifilar.svg" title="Diagrama unifilar" width="70%"/>
</div>

Cada uno de los buses $k$ se asocia con cuatro variables principales: 
* Magnitud de la tensión $V_k$
* Ángulo de fase de la tensión $\delta_k$
* Potencia activa inyectada $P_k$
* Potencia reactiva inyectada $Q_k$

Las líneas de transmisión se representan por un equivalente $\pi$ balanceado. Se debe tener como dato la impedancia en serie y en derivación (líneas medias y largas).

Todos los valores se representan en el sistema por unidad [^1]. 

Adicionalmente, se debe conocer la matriz de admitancias del sistema, que se obtiene de los datos de las líneas de transmisión y transformadores. Esta matriz cuadrada tiene tantas filas o columnas como nodos hay en el sistema.
* Cantidad de nodos $n$
* Matriz de admitancias de buses $[Y_{bus}]$
* Los elementos de la matriz de admitancias son: $Y_{kk}=$ suma de las admitancias conectadas al nodo $k$ y $Y_{km}=$ -(suma de los elementos conectados entre los buses $k$ y $m$ con $k \ne m$)

### Corrientes Inyectadas a cada bus

Las corrientes inyectadas a cada uno de los buses del sistema de potencia se pueden calcular a partir de los voltajes y la matriz de admitancias.

$$\mathbf{[I_{bus}]=[Y_{bus}][V_{bus}]}$$

Si el fasor de voltaje del bus $k$ es $\mathbf{V_k}=V_k\angle\delta_k$. 


Por ejemplo, para dos buses como se muestran en la figura se tiene: 

$$I_1=V_1Y_g+(V_1-V_2)Y_s$$

$$I_2=V_2Y_g+(V_2-V_1)Y_s$$

$$[Y_{bus}]=
\begin{bmatrix}
        Y_{11}&Y_{12}\\
        Y_{21}&Y_{22}
\end{bmatrix}
$$

### Potencia Inyectada a cada bus

La potencia inyectada a cada bus por convención es la resta de la potencia generada menos la potencia demandada.

$$P_k=P_{Gk}-P_{Lk}$$ 

$$Q_k=Q_{Gk}-Q_{Lk}$$



### Voltajes 



### Control de versiones

| Versión    | Descripción        | Autor                                       | Horas |
|------------|:-------------------|---------------------------------------------|:-----:|
| 2023.06.27 | Versión preliminar | [josimardtm](https://github.com/josimardtm) |   3   |

_PowerFlow es de uso libre para fines académicos, conoce nuestra licencia, cláusulas, condiciones de uso y como referenciar los contenidos publicados en este repositorio, dando [clic aquí](../../LICENSE.md)._

_¿Encontraste útil este repositorio? Apoya su difusión marcando este repositorio con una ⭐ o síguenos dando clic en el botón Follow de [Josimardtm](https://github.com/josimardtm) en GitHub._

| [Anterior](../Readme.md) | [:house: Inicio](../../Readme.md) | [:beginner: Ayuda / Colabora](https://github.com/josimardtm/PowerFlow/discussions) | [Siguiente](../01.02.Classification/Readme.md) |
|--------------------------|-----------------------------------|------------------------------------------------------------------------------------|------------------------------------------------|

[^1]:[Sistema de valores por unidad](https://es.wikipedia.org/wiki/Sistema_por_unidad)

[comment]:<> (Referencias [^1]: Tomado y/o adaptado de https://www.scielo.org.mx/scielo.php?pid=S2007-78902020000800028&script=sci_arttext#:~:text=El%20desarrollo%20colaborativo%20se%20refiere,inform%C3%A1tico%20funcional%20y%20de%20calidad.)
[comment]:<> (Enlace a video, imagen de cabecera, alcance, objetivos, requerimientos, diagrama general de procesos, conceptos)
[comment]:<> (Procedimiento, Actividades complementarias, Preguntas y respuestas, referencias, control de versiones)
