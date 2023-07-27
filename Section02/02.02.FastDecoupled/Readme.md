## Solución del problema de flujo de potencia con el método Desacoplado Rápido

Keywords: `Power flow` `Fast-Decoupled`

### Requerimientos

* Lectura de referencias a pie de página

### Acoplamiento en sistemas de transmisión

Comúnmente, en un sistema de transmisión en régimen permanente existe una fuerte dependencia de la potencia activa con los ángulos de la tensión y la potencia reactiva con las magnitudes de la tensión. Esto ocurre porque se busca que las pérdidas en las líneas de transmisión y los transformadores de potencia sean muy bajas.

Los métodos desacoplados toman ventaja de esta condición para resolver dos problemas de flujo de potencia separados más simples.

<img src="Graph\acoplamiento.svg"/>

### Simplificación del método de Newton-Raphson

En ocasiones el método de Newton-Raphson puede tener tiempos de ejecución inaceptables, sobre todo para grandes sistemas y múltiples casos. 

Para hacer este método un poco más rápido, se buscan dos simplificaciones: evitar el cálculo del Jacobiano en cada iteración y desacoplar los problemas $P-\delta$ y $Q-V$.

Aunque estas premisas permiten obtener una solución aproximada para los flujos de potencia. Ellas tienen implicaciones:
* No recalcular el Jacobiano: introduce errores en la solución.
* Desacoplar las variables: no se recomienda para sistemas altamente cargados o con bajos niveles de tensión.

> **Ventaja:** es un algoritmo rápido, lo que es útil cuando se requiere una gran cantidad de soluciones de flujos de potencia.
> **Desventaja:** en sistemas donde la relación R/X es alta, este método puede comportarse de forma oscilatoria y no encontrar una solución precisa.

## Formulación del método desacoplado rápido

Del [método de Newton-Raphson](../02.01.NewtonRaphson) aplicado al problema de flujos de potencia se tiene: 

$$\begin{bmatrix} 
\mathbf{\Delta P} \\
--\\
\mathbf{\Delta Q} \\
\end{bmatrix} = \begin{bmatrix}
H | N \\
--\\
M | L \\
\end{bmatrix} \begin{bmatrix}
\Delta \delta_i\\
--\\
\frac{\Delta V_j}{V_j}
\end{bmatrix}$$

Con este sistema, se asume que:
* $V_k \approx 1$ para todos los nodos, es decir que las tensiones no se alejan significativamente de su valor nominal.
* $G_{km} \ll B_{km}$ para cualquier par de nodos, es decir que las líneas y transformadores tienen bajos niveles de componente resistivo.
* $\cos (\delta_k-\delta_m) \approx 1$ y $\sin (\delta_k-\delta_m) \approx 0$, esto indica que la diferencia entre los ángulos no debe ser significativa.
* $Q_k \ll B_kk$ la inyección de potencia reactiva es baja. 

Con estos supuestos se obtiene que:
* $[H]=[B_1]$, donde los elementos de la matriz $[B_1]$ son $-B_km=-Imag(Y_km)$
* $[L]=[B_2]$, donde los elementos de la matriz $[B_2]$ son $-B_km=-Imag(Y_km)$
* $[N]=[M]=0$

Entonces, el sistema de ecuaciones a solucionar es:

$$\begin{bmatrix} 
\mathbf{\Delta P} \\
--\\
\mathbf{\Delta Q} \\
\end{bmatrix} = \begin{bmatrix}
H | 0 \\
--\\
0 | L \\
\end{bmatrix} \begin{bmatrix}
\Delta \delta\\
--\\
\frac{\Delta V}{V}
\end{bmatrix}$$

Esto representa dos sistemas de ecuaciones desacoplados:

$$ \mathbf{[\Delta P]} = \mathbf{[B_1]} \mathbf{[\Delta \delta]} $$

$$ \mathbf{[\Delta Q]} = \mathbf{[B_2]} \mathbf{[\frac{\Delta V}{V}]} $$

### Control de versiones

| Versión    | Descripción        | Autor                                       | Horas |
|------------|:-------------------|---------------------------------------------|:-----:|
| 2023.06.27 | Versión preliminar | [josimardtm](https://github.com/josimardtm) |   2   |

_PowerFlow es de uso libre para fines académicos, conoce nuestra licencia, cláusulas, condiciones de uso y como referenciar los contenidos publicados en este repositorio, dando [clic aquí](../../LICENSE.md)._

_¿Encontraste útil este repositorio? Apoya su difusión marcando este repositorio con una ⭐ o síguenos dando clic en el botón Follow de [Josimardtm](https://github.com/josimardtm) en GitHub._

| [Anterior](../Readme.md) | [:house: Inicio](../../README.md) | [:beginner: Ayuda / Colabora](https://github.com/josimardtm/PowerFlow/discussions) | [Siguiente](../01.02.Classification/Readme.md) |
|--------------------------|-----------------------------------|------------------------------------------------------------------------------------|------------------------------------------------|

<div align="center">
    <a href="https://enlace-academico.escuelaing.edu.co/psc/FORMULARIO/EMPLOYEE/SA/c/EC_LOCALIZACION_RE.LC_FRM_ADMEDCO_FL.GBL" target="_blank"><img src="../../.icons/banner-pie-de-pagina.jpg" alt="Certificado" width="100%" border="0" /></a>
</div>