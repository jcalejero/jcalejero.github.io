---
layout: post
comments: true
title: ANECUP un empate para nada imposible
subtitle: ya lo dicen... impossible is nothing
---

**¡Empate!** 

El pasado domingo en Catalunya la [CUP](http://cup.cat/) organizó su asamblea para decidir sobre 4 escenarios posibles frente a la negociación que está teniendo con JxSÍ. No, no es un post político. Podéis seguir leyendo :)

Estos escenarios eran:

<blockquote class="twitter-tweet" lang="es"><p lang="und" dir="ltr">Escenari 1: Mas ✅ - Acord ✅&#10;Escenari 2: Mas ❌ - Acord ❌ negociar&#10;Escenari 3: Mas ✅ - Acord ❌&#10;Escenari 4: Mas ❌ - Acord ❌ eleccions&#10;<a href="https://twitter.com/hashtag/ANECUP?src=hash">#ANECUP</a></p>&mdash; Marc Ustrell (@marcustrell) <a href="https://twitter.com/marcustrell/status/681063895205830656">diciembre 27, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>


Se realizaban votaciones eliminatorias siempre y cuando ninguna opción llegase al 50% de los sufragios emitidos. Después de dos votaciones los escenarios que quedaron en la carrera fueron el 1 y el 2. En la tercera votación (y definitiva) los votos nulos y en blanco quedaban eliminados dentro del total de sufragios. Este punto es importante, ya lo veremos más adelante.

Y... ¿cuál fue el resultado de esta tercera votación? **¡Empate!**

Y aquí empieza todo...

**Cuál era la probabilidad de que sucediera eso?** Mucha gente ya ha escrito sobre ello y, como siempre, ninguna cifra es común. Por ejemplo:

<blockquote class="twitter-tweet" lang="es"><p lang="und" dir="ltr">El problema de <a href="https://twitter.com/hashtag/combinat%C3%B2ria?src=hash">#combinatòria</a> d&#39;aquest nadal. <a href="https://twitter.com/hashtag/anecup?src=hash">#anecup</a> <a href="https://twitter.com/hashtag/anecup27d?src=hash">#anecup27d</a> <a href="https://twitter.com/hashtag/empat?src=hash">#empat</a> <a href="https://t.co/Fj7QpkWVem">pic.twitter.com/Fj7QpkWVem</a></p>&mdash; Shinnosuke (@shinnoshanno) <a href="https://twitter.com/shinnoshanno/status/681214344839966723">diciembre 27, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

O el siguiente artículo de [La Vanguardia](http://www.lavanguardia.com/politica/20151229/301089471510/empate-asamblea-cup-debate-matematico.html)

Yo ofrezco la mía:

*Supuestos*

- Probabilidades de voto emitido: Voto válido (3022/3042); Voto nulo ( 6/3042) y voto en blanco (14/3042). Estos valores son fruto de la segunda votación. 
- Electores posibles: 3042 (votantes en la segunda votación).
- Probabilidad opción 1 = opción 2 = 50%.
- Se simuló para cada uno de los posibles electores si su voto fue válido, nulo o en blanco y, si fue válido a qué escenario votó.

Realicé un pequeño [código en R](github.com/jcalejero/jcalejero.github.io/blob/master/codes/anecup.R) para esta simulación. Los resultados:

| Simulacions  | Escenari 2  | Escenari 1  | Empat  |  Empat (a 1515) |
|---|---|---|---|---|
|100000| 49614  |  49666 | 720  | 34  |

El **empate** se dio en el **0.72% de los casos** y en el 0.03% (del total de simulaciones) fue con empate a 1515. 

Nos encontramos con que en la mayoría de los casos que estoy leyendo se omiten los votos en blanco / nulos que se pudieron emitir y que podrían haber sido válidos y ofrecer otro tipo de empates a 1515.

Además, viendo los resultados de los escenarios 1 y 2, es cierto que la expectativa de un empate era bastante plausible. 