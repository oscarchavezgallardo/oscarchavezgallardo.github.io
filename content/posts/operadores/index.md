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

### Referencias

- [Tutorial de LaTex](https://manualdelatex.com/tutoriales)
- ...

```yaml
test code:
- test 
```