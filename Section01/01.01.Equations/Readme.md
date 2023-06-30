## Actividad 1 - Ecuaciones fundamentales del flujo de potencia

Keywords: `Equations` `Power flow` `Formulation`

### Requerimientos

* Lectura de referencias a pie de página
* [Admitancia](https://es.wikipedia.org/wiki/Admitancia)
* [Matriz de admitancias](https://es.wikipedia.org/wiki/Admitancia)

### Modelo balanceado en estado estacionario de un sistema de potencia

Los sistemas de potencia contienen una gran cantidad de elementos que permiten conectar a los consumidores de energía eléctrica con las fuentes de generación.

En estado estacionario, estos sistemas se pueden representar por modelos simplificados que permiten conformar circuitos para realizar un análisis de sus condiciones de operación.

El punto de partida para la formulación del problema de flujo de potencia es un diagrama unifilar del sistema que proporciona los datos de entrada. Entre estos datos se requiere: Información de los buses, de las líneas de transmisión y de los transformadores.

<div align="center">
    <br><img alt="Ejemplo de diagrama unifilar de un sistema de potencia." src="Graph\unifilar.svg" title="Diagrama unifilar" width="60%"/>
</div>

Cada uno de los buses $´k´$ se asocia con cuatro variables principales: 
* Magnitud de la tensión $´V_k´$
* Ángulo de fase de la tensión $\delta_k$
* Potencia activa inyectada $P_k$
* Potencia reactiva inyectada $Q_k$

### Potencia Inyectada

### Voltajes 

### Corrientes

### Control de versiones

| Versión    | Descripción        | Autor                                       | Horas |
|------------|:-------------------|---------------------------------------------|:-----:|
| 2023.06.27 | Versión preliminar | [josimardtm](https://github.com/josimardtm) |   2   |

_PowerFlow es de uso libre para fines académicos, conoce nuestra licencia, cláusulas, condiciones de uso y como referenciar los contenidos publicados en este repositorio, dando [clic aquí](../../LICENSE.md)._

_¿Encontraste útil este repositorio? Apoya su difusión marcando este repositorio con una ⭐ o síguenos dando clic en el botón Follow de [Josimardtm](https://github.com/josimardtm) en GitHub._

| [Anterior](../Readme.md) | [:house: Inicio](../../Readme.md) | [:beginner: Ayuda / Colabora](https://github.com/josimardtm/PowerFlow/discussions) | [Siguiente](../01.02.Classification/Readme.md) |
|--------------------------|-----------------------------------|------------------------------------------------------------------------------------|------------------------------------------------|

[comment]:<> (Referencias [^1]: Tomado y/o adaptado de https://www.scielo.org.mx/scielo.php?pid=S2007-78902020000800028&script=sci_arttext#:~:text=El%20desarrollo%20colaborativo%20se%20refiere,inform%C3%A1tico%20funcional%20y%20de%20calidad.)
[comment]:<> ([Línea de transmisión](Screenshot\electricity-3158345_1280.jpg "Torre de línea de transmisión"))
[comment]:<> (Enlace a video, imagen de cabecera, alcance, objetivos, requerimientos, diagrama general de procesos, conceptos)
[comment]:<> (Procedimiento, Actividades complementarias, Preguntas y respuestas, referencias, control de versiones)
