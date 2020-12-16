# Tarea2_FOR_LOOP

getwd()
setwd("C:/Users/casa/Desktop/Datos")

##CARGAR DATOS AGREGANDO LA VARIABLE TAMANIO##


pequenaperu <- data.frame(read.csv2("pequena_peru.csv"), "tamanio" = as.character(c('pequena')))
pequenacolombia <- data.frame(read.csv2("pequena_colombia.csv"), "tamanio" = as.character(c('pequena')))
pequenachile <- data.frame(read.csv2("pequena_chile.csv"), "tamanio" = as.character(c('pequena')))
microperu <- data.frame(read.csv2("micro_peru.csv"), "tamanio" = as.character(c('micro')))
microcolombia <- data.frame(read.csv2("micro_colombia.csv"), "tamanio" = as.character(c('micro')))
microchile <- data.frame(read.csv2("micro_chile.csv"), "tamanio" = as.character(c('micro')))
medianaperu <- data.frame(read.csv2("medianas_peru.csv"), "tamanio" = as.character(c('mediana')))
medianacolombia <- data.frame(read.csv2("medianas_colombia.csv"), "tamanio" = as.character(c('mediana')))
medianachile <- data.frame(read.csv2("medianas_chile.csv"), "tamanio" = as.character(c('mediana')))
grandeperu <- data.frame(read.csv2("grandes_peru.csv"), "tamanio" = as.character(c('grande')))
grandecolombia <- data.frame(read.csv2("grandes_colombia.csv"), "tamanio" = as.character(c('grande')))
grandechile <- data.frame(read.csv2("grandes_chile.csv"), "tamanio" = as.character(c('grande')))

##BASE DE DATOS##

Empresasxpaises <- data.frame("empresas peru" = pequenaperu, microperu, medianaperu, grandeperu,
"empresas colombia" = pequenacolombia, microcolombia, medianacolombia, grandecolombia,
"empresas chile" = pequenachile, microchile, medianachile, grandechile)



