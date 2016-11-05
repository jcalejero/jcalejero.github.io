--- 
layout: post 
section-type: post 
comments: true 
title: Proyecto Pepper Pot Parte I
category: Data 
tags: [ 'RCode' ] 
---

# Proyecto Pepper pot

Hace ya bastantes semanas decidí dedicar tiempo a un pequeño proyecto que me ayudara a practicar algunas técnicas de predicción, modelado o _web_ _scraping_. El tema: NHL. Sí, debo reconocerlo. Me encanta el hockey sobre hielo y casi todos los años compro el gamepass (aprovechando siempre alguna oferta). Me gusta por que es un deporte (y una liga) donde a partir de la jornada 20-25 ya empiezan a aparecer ciertos patrones que, una vez detectados, es fácil explotarlos para... sí, ganar dinero apostando. 

_Si a alguien le interesa el dato, tengo un 87% de acierto en partidos de NHL_.

### Objetivo del proyecto
  - Resultado **victoria / derrota**
  - Resultado **+/- goles en el partido**
  - **OT en el partido sí/no**

### Listado de tareas en trello
[![N|Solid](https://pbs.twimg.com/media/CuGWe9XXgAAFJaf.jpg:large)](https://twitter.com/InsideAlgorithm/status/784073279648702464)

### Código en R
* Paquetes necesarios

```R
library(XML)
library(stringr)
```

* _Web_ _scraping_ y construcción del _dataset_ 

```R
GetGamesStatsByYear <- function(year = 2011) {
  url <- BuildURLStrings(year)
  tables <- readHTMLTable(url)
  return(tables)
}
```

```R
BuildURLStrings <- function(year) {
  url <- paste0("http://www.hockey-reference.com/leagues/NHL_", year, "_games.html")
  return(url)
}
```

```R
BuildNHLMatchDataFrame <- function(data, PO) {
  if (PO == FALSE) {
    n.rows <- unlist(lapply(data, function(t) dim(t)[1]))
  } else {
    n.rows <- unlist(lapply(data, function(t) dim(t)[2]))
  }
  table.games <- data[[which.max(n.rows)]]
  colnames(table.games) <- c("Date", "Visitor", "VisGoals", "Home", "HomeGoals", "OTCat", 
                   "Attendance", "LengthOfGame", "Notes")
  table.games <- table.games[table.games$OTCat!="Get Tickets",]
  table.games$OT <- table.games$OTCat=="OT"|table.games$OTCat=="SO"
  return(table.games)
}
```

```R
GenerateRawDataNHLGames <- function(years = c(2011, 2012), PO = FALSE) {
  raw.data <- NULL
  for (year in years) {
    year.data <- GetGamesStatsByYear(year)
    year.data.processed <- BuildNHLMatchDataFrame(year.data, PO)
    raw.data <- rbind(raw.data, year.data.processed)
  }  
  return(raw.data)
}
```

Para generar los datos para la temporada 2017 basta con ejecutar:

```R
data <- GenerateRawDataNHLGames(2017)
```

![N|Solid](https://jcalejero.github.io/jcalejero.github.io/img/nhl_dataset.png)
