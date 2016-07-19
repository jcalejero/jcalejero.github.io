---
layout: post
section-type: post
comments: true
title: ¿merge() o left_join()? explorando el paquete dplyr
category: Data
tags: [ 'R' ]
---

Habitualmente suelo utilizar la función *merge()*. Sin embargo, he notado que si el `data.frame` es extremadamente grande, el tiempo de ejecución del código llega a ser realmente un problema.

Hace mucho tiempo hicimos un pequeño experimento ya que había estado leyendo acerca de la función **left_join()** que está disponible en *dplyr*

*inner_join (similar a merge con las opciones all.x=T y all.y=F)*

El experimento que voy a llevar a cabo es comparar 10 ejecuciones usando *merge()* y 10 ejecuciones usando *left_join()*. Las características del experimento son:
-Fichero A con 7 540 043 filas y 7 columnas.
-Fichero B con 20 423 filas y 3 columnas.

**Los resultados:**

Tiempo de ejecución usando *merge()*

!["merge"](https://jcalejero.github.io/jcalejero.github.io/img/merge.png)

Tiempo de ejecución usando *left_join()*
!["left_join"](https://jcalejero.github.io/jcalejero.github.io/img/left_join.png)

Podemos ver cómo usando la función *merge()* el tiempo de ejecución se sitúa próximo al minuto de forma estable. Sin embargo, con la función *left_join()*, el tiempo de ejecución se reduce a un par de segundos. Por lo tanto, podemos reducir el tiempo de ejecución de nuestros _scripts_ con fusiones de tablas grandes de forma brutal.
