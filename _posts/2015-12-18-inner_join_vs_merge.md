---
layout: post
comments: true
title: left_join vs merge(x, y, by='', all.x=TRUE)
subtitle: ¿A quién prefieres, a papá o a mamá?
---

Quien trabaje con datos... con grandes volúmenes y tenga que cruzar dos datasets sabrá que a veces es una tarea ardua y dura. Además, existen varias combinaciones posibles de JOINS: *left*, *right*, *inner*... En la siguiente imagen podemos ver un ejemplo visual que ayudará a comprender cada uno de ellos:

![alt text](http://2.bp.blogspot.com/-alqVLVQGXp0/USYCyI-s_GI/AAAAAAAAAcM/wiar-fDptAY/s640/Visual_SQL_JOINS_orig.jpg "Fuente: http://www.pvilas.com/")


**left_join vs merge**

## ¿Qué tenemos disponibles en R?

En R tenemos disponibles las funciones *left_join()* y *merge(,,,all.x=TRUE)* para realizar JOINS de tipo **LEFT**.

*left_join* es una función del paquete **dplyr** [link](https://cran.r-project.org/web/packages/dplyr/vignettes/two-table.html). Su sintaxis es:

~~~
left_join(x=df1, y=df2, by="Column")
~~~

*merge* es una función del paquete **base** [link](https://stat.ethz.ch/R-manual/R-devel/library/base/html/merge.html). Su sintaxis es:

~~~
merge(x=df1, y=df2, by="Column", all.x=TRUE)
~~~

Entonces, si son iguales ¿por qué elegir una u otra? En mi experiencia con estas dos funciones me he encontrado en dos situaciones: la primera, dataframes manejables en términos de filas donde el tiempo de ejecución de cada una de las funciones era similar. La segunda, y más interesante, dataframes enormes en donde la utilización de left_join mejoró el tiempo de procesado de la información.

Veamos un ejemplo:

Vamos a trabajar con el fichero [Netflix Prize Data Set](http://academictorrents.com/details/9b13183dc4d60676b773c9e2cd6de5e5542cee9a)
Su descripción: *This is the official data set used in the Netflix Prize competition. The data consists of about 100 million movie ratings, and the goal is to predict missing entries in the movie-user rating matrix.*

- Tamaño comprimido: 697,6 MB
- Tamaño descomprimido: 2,1 GB
- Número de filas importadas: 18339174 [limitado a los primeros 3500 archivos]
- Columnas: 3

{% highlight r linenos %}
files <- list.files(path="./download/training_set/")
files <- files[1:3500]
datos.brutos <- do.call("rbind", 
                       lapply(paste("./download/training_set/",
                     				files,sep=""), 
                        read.table, header = FALSE,
                        skip = 2, sep=","))
head(datos.brutos)
 	V1 V2         V3
822109  5 2005-05-13
885013  4 2005-10-19
 30878  4 2005-12-26
823519  3 2004-05-03
893988  3 2005-11-17
124105  4 2004-08-05

datos.brutos.b = datos.brutos.a

time.start <- Sys.time()
merge <- merge(datos.brutos.a, datos.brutos.b, by="V3", all.x=TRUE)
time.end <- Sys.time()
tiempo <- time.end - time.start

print(paste("tiempo total:", 
			round(as.numeric(tiempo)/60,2), "minutos"))
"tiempo total: 21.03 minutos"

library(dplyr)
time.start <- Sys.time()
merge <- left_join(datos.brutos.a, datos.brutos.b, by="V3")
time.end <- Sys.time()
tiempo <- time.end - time.start

print(paste("tiempo total:", 
			round(as.numeric(tiempo)/60,2), "minutos"))
"tiempo total: 13.42 minutos"

{% endhighlight %}
