## Solución del problema de flujo de potencia con el método de Newton-Raphson

Keywords: `Power flow` `Newton-Raphson`

### Requerimientos

* Lectura de referencias a pie de página
* [Método de Newton-Raphson](https://www.geogebra.org/m/XCrwWHzy)

### Método de Newton-Raphson para la solución de sistemas de ecuaciones no lineales

El método de Newton-Raphson para la solución de sistemas de ecuaciones no lineales permite calcular una solución numérica para $\mathbf{f(x)=0}$ con $\mathbf{f(x)}:\mathbb{R}^n \rightarrow \mathbb{R}^n$.

Se parte de valores iniciales de $\mathbf{x}$ con los que $\mathbf{f(x)}\ne 0$ para llegar a un valor $\mathbf{x}$ tal que $\mathbf{f(x+\Delta x)=0}$ .

Se utiliza la serie de Taylor truncada en la primera derivada:

$$\mathbf{f(x+\Delta x)} \approx \mathbf{f(x)}+[J]\mathbf{\Delta x}+... =0$$

Luego, $\mathbf{f(x)}=-[J]\mathbf{\Delta x} \Rigtharrow  \mathbf{\Delta x}=-[J]^{-1}\mathbf{f(x)}$

Donde $[J]$ es la matriz Jacobiana[^1] de $\mathbf{f(x)}$

El cálculo de las variables en una nueva iteración $r$ se hace de la siguiente manera:

$$\mathbf{x}^{(r)}=\mathbf{x}^{(r-1)}+\mathbf{\Delta x}^{(r-1)}=\mathbf{x}^{(r-1)}-[J^{(r-1)}]^{-1}\mathbf{f(x)}^{(r-1)}$$

Donde:

$$\mathbf{x}=\begin{bmatrix} 
x_1\\
x_2\\
\vdots\\
x_n\\
\end{bmatrix}; \mathbf{f(x)}= \begin{bmatrix} 
f_1(x_1,x_2,...,x_n)\\
f_2(x_1,x_2,...,x_n)\\
\vdots\\
f_m((x_1,x_2,...,x_n)\\
\end{bmatrix}; \mathbf{[J]}=\begin{bmatrix} 
\frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} & ... & \frac{\partial f_1}{\partial x_n} \\
\frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2} & ... & \frac{\partial f_2}{\partial x_n} \\
\vdots & \vdots & \ddots & \vdots\\
\frac{\partial f_n}{\partial x_1} & \frac{\partial f_n}{\partial x_2} & ... & \frac{\partial f_n}{\partial x_n} \\ 
\end{bmatrix} $$

### Formulación del método de Newton-Raphson para la solución de flujos de potencia

Recordemos que el problema de flujo de potencia está dado por las ecuaciones de inyección de potencia a cada uno de los nodos del sistema. Para resolver este sistema de ecuaciones simultáneo, se puede aplicar el método de Newton-Raphson teniendo en cuenta que:

$$\mathbf{f(x)}= \begin{bmatrix} 
\mathbf{\Delta P} \\
--\\
\mathbf{\Delta Q} \\
\end{bmatrix}; \begin{matrix}
\Delta P_i=P_{esp,i}-P_i \\
\Delta Q_j=Q_{esp,j}-Q_j \\
\end{matrix} $$

Donde $\Delta P_{esp,i}$ es la potencia activa especificada o conocida para los nodos de generación y de carga, mientras que $\Delta Q_{esp,j}$ es la potencia reactiva especificada o conocida para los nodos de carga. Estas son las variables conocidas de potencia de todos los nodos.

Además, las variables del sistema de ecuaciones son:

$$ \mathbf{x}= \begin{bmatrix}
\mathbf{\delta}\\
--\\
\mathbf{V}\\
\end{bmatrix}$$

Donde $\delta_i$ son los ángulos de los nodos de generación y de carga, mientras $V_j$ son las magnitudes de voltaje de los nodos de carga. Es decir, las variables desconocidas de los voltajes de todos los nodos.

Entonces, las funciones que se resuelven buscan lograr que la diferencia entre los valores de potencia conocidos en los nodos sea prácticamente igual a la potencia calculada en los nodos. Estas diferencias deben ser menores a una tolerancia que se representa por $\Epsilon$. Comúnmente, esta tolerancia es muy pequeña, por debajo de $10^{-4}$.

Aplicando el método de Newton-Raphson, tenemos que $-\mathbf{f(x)}=[J]\mathbf{\Delta x}$, pero con la definición dada para $\mathbf{f(x)}$:

$$\mathbf{-f(x)}= \begin{bmatrix} 
-\mathbf{\Delta P} \\
--\\
-\mathbf{\Delta Q} \\
\end{bmatrix} = \begin{bmatrix}
\frac{\partial Delta P_i}{\partial \delta_i} \frac{\partial \Delta P_i}{\partial V_j} \\
--\\
\frac{\partial Delta Q_j}{\partial \delta_i} \frac{\partial \Delta Q_i}{\partial V_j} \Delta \V_j\\
\end{bmatrix} \begin{bmatrix}
\Delta \delta_i\\
\Delta V_j
\end{bmatrix}$$



### Control de versiones

| Versión    | Descripción        | Autor                                       | Horas |
|------------|:-------------------|---------------------------------------------|:-----:|
| 2023.06.27 | Versión preliminar | [josimardtm](https://github.com/josimardtm) |   5   |

_PowerFlow es de uso libre para fines académicos, conoce nuestra licencia, cláusulas, condiciones de uso y como referenciar los contenidos publicados en este repositorio, dando [clic aquí](../../LICENSE.md)._

_¿Encontraste útil este repositorio? Apoya su difusión marcando este repositorio con una ⭐ o síguenos dando clic en el botón Follow de [Josimardtm](https://github.com/josimardtm) en GitHub._

| [Anterior](../Readme.md) | [:house: Inicio](../../README.md) | [:beginner: Ayuda / Colabora](https://github.com/josimardtm/PowerFlow/discussions) | [Siguiente](../01.02.Classification/Readme.md) |
|--------------------------|-----------------------------------|------------------------------------------------------------------------------------|------------------------------------------------|

[^1]:[Matriz Jacobiana](https://es.khanacademy.org/math/multivariable-calculus/multivariable-derivatives/jacobian/v/the-jacobian-matrix)