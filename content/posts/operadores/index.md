---
title: "Oscilador Armónico Unidimensional"
description: "..."
categories: ["QuantumMechanics"]
tags: ["physics"]
draft: false
date: 2026-04-13T14:45:00-06:00  
---


### Importancia del oscilador armónico en física.
<!-- {{< carousel images="{https://cdn.pixabay.com/photo/2016/12/11/12/02/mountains-1899264_960_720.jpg,gallery/03.jpg,gallery/01.jpg,gallery/02.jpg,gallery/04.jpg}" >}} -->

Este capitulo está dedicado al estudio particular de un sistema físico importante: el oscilador armónico unidimensional.

El ejemplo más simple de este sistema es que una partícula de masa m moviendose en un potencial el cúal depende solo de x y tiene la forma:

{{< katex >}}
\(V(x) = \frac{1}{2}kx^2\)

(k es una constante real positiva). La partícula es atraida hacia el plano  x=0 [el minimo de V(x), correspondiente a la posición de equilibrio estable] por una fuerza restauradora:

{{< katex >}}
\(F_x = - \frac{dV}{dx} = - kx\)

que es proporcional a la distancia x entre  la partícula en el plano x=0 (x es una variable algebraica: x>0). Sabemos que en mecánica clásica , la proyección en {{< katex >}} \( O_{x} \) del movimiento de la partícula es un movimiento sinoidal alrededor de x=0, de frecuencia angular:

{{< katex >}}
\( w= \sqrt{\frac{k}{m}} \)

<div id="fig-oscilador" class="chart-wrapper">
{{< chart >}}
type: 'scatter',
data: {
  datasets: [
    {
      label: 'V(x)',
      data: [
        {x:-3,y:4.5},{x:-2.8,y:3.92},{x:-2.6,y:3.38},{x:-2.4,y:2.88},{x:-2.2,y:2.42},
        {x:-2,y:2},{x:-1.8,y:1.62},{x:-1.6,y:1.28},{x:-1.4,y:0.98},{x:-1.2,y:0.72},
        {x:-1,y:0.5},{x:-0.8,y:0.32},{x:-0.6,y:0.18},{x:-0.4,y:0.08},{x:-0.2,y:0.02},
        {x:0,y:0},{x:0.2,y:0.02},{x:0.4,y:0.08},{x:0.6,y:0.18},{x:0.8,y:0.32},
        {x:1,y:0.5},{x:1.2,y:0.72},{x:1.4,y:0.98},{x:1.6,y:1.28},{x:1.8,y:1.62},
        {x:2,y:2},{x:2.2,y:2.42},{x:2.4,y:2.88},{x:2.6,y:3.38},{x:2.8,y:3.92},{x:3,y:4.5}
      ],
      borderColor: '#ffffff',
      borderWidth: 2,
      pointRadius: 0,
      showLine: true,
      fill: false,
      tension: 0.4
    },
    {
      label: 'E',
      data: [{x:-3,y:2},{x:3,y:2}],
      borderColor: '#ffffff',
      borderWidth: 1,
      borderDash: [5,5],
      pointRadius: 0,
      showLine: true,
      fill: false
    }
  ]
},
options: {
  plugins: {
    legend: { display: false },
    title: {
      display: true,
      text: 'Figure 1: The potential energy V(x) of a one-dimensional harmonic oscillator.',
      font: { style: 'italic', size: 12 },
      color: '#aaa',
      position: 'bottom'
    }
  },
  scales: {
    x: { type: 'linear', title: { display: true, text: 'x', color: '#aaa' }, min: -3.5, max: 3.5 },
    y: { title: { display: true, text: 'V(x)', color: '#aaa' }, min: -0.5, max: 5 }
  }
}
{{< /chart >}}
</div>


De hecho, un gran número de sistemas son gobernados (al menos aproximadamente) por las ecuaciones del oscilador armónico. Donde sea que uno estudie  el comportamiento físico de un sistema en la vecindad de un punto estable de equilibrio, uno llega a la ecuación en el límite de oscilaciones pequeñas, a la de un oscilador armónico.

Los resultados anteriores derivan aplicaciones experimentales, como lo son una serie de fenómenos físicos, como lo son las vibraciones de los átomos de una molécula alrededor de su posición de equilibrio, las oscilaciones de los átomos o iones de una estructura cristalina.

El oscilador armónico también se involucra en las soluciones de las ecuaciones de Maxwell, donde analizando una cavidad, existen una infinidad de ondas estacionarias. El campo electromagnético puede ser expandido en términos de estos modos y se puede demostrar que, cada uno de los coeficientes de esta expansión obedece una ecuación diferencial, es equivalente al oscilador armónico, donde la frecuencia angular {{< katex >}} \( w \) esta asociada al modo normal.

En otras palabras, el campo electromagnético es formalmente equivalente a un conjunto de osciladores armónicos independientes. La cuantización de este campo es obtenida mediante la cuantización de los osciladores armónicos asociados con los varios modos normales de la cavidad.

De hecho particularmente por el estudio de las oscilaciones en el equilibrio térmico (Radiación de Ccuerpo negro) lo cúal es históricamente atribuido a Max Planck, por primera vez en la física, la constante {{< katex >}} \( \hbar \) es a lo que se atribuye su nombre. Además veremos como la energía media de un oscilador armónico en el equilibrio termodinámico a la temperatura T, es diferente para los osciladores mecánicos clásicos y cuánticos.

Posteriormente veremos como los niveles de energía son equidistantes, y el espacio equidistante entre dos niveles es aproximadamente de {{< katex >}} \( \hbar w \). Donde además etiquetando cada nivel con el entero {{< katex >}} \( n \), este puede ser asociado a un número idéntico de {{< katex >}} \( n \) partículas, cada una poseyendo una energía de {{< katex >}} \( \hbar w \). La transición del oscilador desde un nivel {{< katex >}} \( n \) a un nivel {{< katex >}} \( n+1 \) o {{< katex >}} \( n-1 \) corresponde a la creación o aniquilación de un cuanto de energía {{< katex >}} \( \hbar w \). 

El objetivo de este post es introducir los operadores {{< katex >}} \( a^\dag \) y {{< katex >}} \( a \), lo cúal nos permite describir la transición de un nivel  {{< katex >}} \( n \) a un nivel {{< katex >}} \( n+1 \) o {{< katex >}} \( n-1 \). Estos operadores, llamados respectivamente operadores de "creación" y "aniquilación", han sidos usados a través de la mecánica cuántica estadistica y la teoría cuántica de campos. 

### El oscilador armónico en la mecánica clásica


La energía potencial {{< katex >}} \( V(r) \) se muestra en la [Figura 1](#fig-oscilador). El movimiento de la partícula es gobernado por la ecuación dinámica:

{{< katex >}} \( m \frac{d^{2}x}{dt^{2}}=\frac{dV}{dx}= -kx\)

La solución general de esta ecuación es de la forma:


{{< katex >}} \( x = x_{M}cos(wt - \phi) \)

donde {{< katex >}} \( w \) es definido por la ecuación anterior, y la constante de integración {{< katex >}} \( x_{M} \) y {{< katex >}} \( \phi \) están determinadas por las condiciones iniciales del movimiento. La particula por lo tanto oscila sinoudalmente alrededor del punto O, con la amplitud {{< katex >}} \( x_{M} \) y frecuencia angular {{< katex >}} \( w \). La energía cinética de la partícula es:

{{< katex >}} \( T= \frac{1}{2}m(\frac{dx}{dt})^{2}= \frac{p^{2}}{2m} \)

donde {{< katex >}} \( p=m\frac{dx}{dt} \) es el momento de la partícula. La energía total es entonces:

{{< katex >}} \( E=T+V=\frac{p^{2}}{2m} + \frac{1}{2}mw^{2}x^{2} \)

Sustituyendo la solución de x en esta ecuación, encontramos que: 

{{< katex >}} \( E=\frac{1}{2}mw^{2}x^{2}  \).

La energía de la partícula es por lo tanto independiente del tiempo (esto es una propiedad general de los sistemas conservativos) y puede tomar valores positivos o 0, dado que {{< katex >}} \( x_{M} \) es arbitraria. Si fijamos la energía total {{< katex >}} \( E \), los límites de el movimiento clásico {{< katex >}} \( x= \pm x_{M} \) puede ser determinado por la [Figura 1](#fig-oscilador), tomando la intersección de la parábola con el eje paralelo a {{< katex >}} \( O_{x} \) de la coordenada  E. En estos puntos {{< katex >}} \( x= \pm x_{M} \), la energía potencial esta en el máximo y es igual a E, y la energía cinética  es 0. De otro modo, al x=0, la energía potencial es 0 y la energía cinética aqui es máxima.


### Propiedades generales del Hamiltoniano mecánico cuántico


### Referencias

- [Tutorial de LaTex](https://manualdelatex.com/tutoriales)
- ...

```yaml
test code:
- test 
```