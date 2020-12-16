# Tarea2_FOR_LOOP

##COMANDOS PARA CONOCER EL ORIGEN DE LOS DATOS QUE VAMOS A UTILIZAR EN R Y PODER CAMBIAR##
##DESDE DONDE VIENEN LOS DATOS##
getwd() 
setwd("C:/Users/samon/Desktop/universidad/2020/Segundo semestre/Big data")

install.packages("tidyr")

##Pregunta uno##
##CARGAR BASES DE DATOS Y ADEMÁS AGREGAMOS LA VARIABLE TAMANIO##

pequenaperu <- data.frame(read.csv2("pequena_peru.csv"), "tamanio" = as.character(c("pequena"))) 
pequenacolombia <- data.frame(read.csv2("pequena_colombia.csv"), "tamanio" = as.character(c("pequena")))
pequenachile <- data.frame(read.csv2("pequena_chile.csv"), "tamanio" = as.character(c("pequena"))) 
microperu <- data.frame(read.csv2("micro_peru.csv"), "tamanio" = as.character(c("micro"))) 
microcolombia <- data.frame(read.csv2("micro_colombia.csv"), "tamanio" = as.character(c("micro"))) 
microchile <- data.frame(read.csv2("micro_chile.csv"), "tamanio" = as.character(c("micro"))) 
medianaperu <- data.frame(read.csv2("medianas_peru.csv"), "tamanio" = as.character(c("mediana"))) 
medianacolombia <- data.frame(read.csv2("medianas_colombia.csv"), "tamanio" = as.character(c("mediana")))
medianachile <- data.frame(read.csv2("medianas_chile.csv"), "tamanio" = as.character(c("mediana"))) 
grandeperu <- data.frame(read.csv2("grandes_peru.csv"), "tamanio" = as.character(c("grande"))) 
grandecolombia <- data.frame(read.csv2("grandes_colombia.csv"), "tamanio" = as.character(c("grande"))) 
grandechile <- data.frame(read.csv2("grandes_chile.csv"), "tamanio" = as.character(c("grande")))

##Pregunta 2##
##UNIR TODAS LAS BASES DE DATOS EN UNA SOLA##

##LAS BASES DE DATOS POSEEN UNA VARIABLE CON NOMBRES DIFERENTES POR LO TANTO HAREMOS QUE##
##TODAS LAS BASES TENGAN EL MISMO NOMBRE EN LA VARIABLE PORCENTAJE MUJERES##

pequena_peru <- pequenaperu %>%
  rename(porcentaje.mujeres = procentaje_mujeres)
pequena_colombia <- pequenacolombia %>%
  rename(porcentaje.mujeres = porcentaje_mujeres)
pequena_chile <- pequenachile %>%
  rename(porcentaje.mujeres = porcentaje_mujeres)
micro_peru <- microperu %>%
  rename(porcentaje.mujeres = porcentaje_mujeres)
micro_colombia <- microcolombia %>%
  rename(porcentaje.mujeres = porcentaje_mujeres)
micro_chile <- microchile %>%
  rename(porcentaje.mujeres = procentaje_muejeres)
mediana_peru <- medianaperu %>%
  rename(porcentaje.mujeres = procentaje_muejeres)
mediana_colombia <- medianacolombia %>%
  rename(porcentaje.mujeres = porcentaje_mujeres)
mediana_chile <- medianachile %>%
  rename(porcentaje.mujeres = procentaje_mujeres)
grande_peru <- grandeperu %>%
  rename(porcentaje.mujeres = procentaje_muejeres)
grande_colombia <- grandecolombia %>%
  rename(porcentaje.mujeres = procentaje_mujeres)
grande_chile <- grandechile %>%
  rename(porcentaje.mujeres = procentaje_mujeres)


##AL ARREGLAR LA VARIABLE PODEMOS UNIR TODAS LAS BASES DE DATOS EN UNA##

pequena_peru %>% union_all(pequena_colombia) %>%
union_all(pequena_chile) %>%
union_all(micro_peru) %>%
union_all(micro_colombia) %>%
union_all(micro_chile) %>%
union_all(mediana_peru) %>%
union_all(mediana_colombia) %>%
union_all(mediana_chile) %>%
union_all(grande_peru) %>%
union_all(grande_colombia) %>%
union_all(grande_chile) -> latam.empresas

##TIPOLOGIA DE CADA UNA DE LAS VARIABLES QUE SE ENCUENTRAN EN LA BASE DE DATOS##

names(latam.empresas) ##nombre de cada una de las variables que hay en la data##

##INSTALAMOS LOS PAQUETES Y LUEGO PODREMOS CONOCER LA TIPOLOGIA DE CADA UNO DE LOS DATOS##
library(dplyr)
library(janitor)

tipologia.datos <- as_tibble(latam.empresas) %>% clean_names()
tipologia.datos ##chr = character, dbl = numeric##

##PREGUNTA 3##
##OBSERVACIONES QUE TIENE CHILE VS PERU##

library(rmarkdown)

pais <- dplyr::select(latam.empresas, pais)

observaciones.PeChi <- "peru.chile"

if (observaciones.PeChi == "peru.chile"){
Ob.Peru <- paged_table(latam.empresas %>% 
                       filter(pais == "peru")) %>% count(pais)
Ob.Chile <- paged_table(latam.empresas %>% 
                       filter(pais == "chile")) %>% count(pais)                     
print(paste("Perú tiene",Ob.Peru[-1],"observaciones"))  
print(paste("Chile tiene",Ob.Chile[-1],"observaciones"))
perupequena <- filter(latam.empresas, tamanio %in% c("pequena"), pais %in% c("peru")) %>% count(tamanio)
perumicro <- filter(latam.empresas, tamanio %in% c("micro"), pais %in% c("peru")) %>% count(tamanio)
perumediana <- filter(latam.empresas, tamanio %in% c("mediana"), pais %in% c("peru")) %>% count(tamanio)
perugrande <- filter(latam.empresas, tamanio %in% c("grande"), pais %in% c("peru")) %>% count(tamanio)
chilepequena <- filter(latam.empresas, tamanio %in% c("pequena"), pais %in% c("chile")) %>% count(tamanio)
chilemicro <- filter(latam.empresas, tamanio %in% c("micro"), pais %in% c("chile")) %>% count(tamanio)
chilemediana <- filter(latam.empresas, tamanio %in% c("mediana"), pais %in% c("chile")) %>% count(tamanio)
chilegrande <- filter(latam.empresas, tamanio %in% c("grande"), pais %in% c("chile")) %>% count(tamanio)
  print(paste("Las",Ob.Peru[-1],"observaciones que tiene Peru,",perupequena[-1], "son de empresas tamaño pequeno,", 
              perumicro[-1], "son de tamaño micro,", perumediana[-1], "son de tamaño mediano y", perugrande[-1],"son de tamaño grande")) 
   print(paste("Por otro lado, las",Ob.Chile[-1],"observaciones que tiene Chile,", chilepequena[-1], "son de empresas tamaño pequeño,", chilemicro[-1], "son de tamaño micro,", chilemediana[-1], "son de tamaño mediano y", chilegrande[-1],"son de tamaño grande"))             
}

##PREGUNTA 4##
##DETERMINAR CUAL ES EL PAÍS CON MAYOR INGRESOS DE EXPLOTACIÓN##

ingresoperu <- latam.empresas %>% select(ingresos, pais) %>%
  filter(pais == "peru") 
ingresocolombia <- latam.empresas %>% select(ingresos, pais) %>%
  filter(pais == "colombia")
ingresochile <- latam.empresas %>% select(ingresos, pais) %>%
  filter(pais == "chile") 

ingresos <- c(sum(ingresoperu[1]), sum(ingresocolombia[1]),sum(ingresochile[1]))
ingresos

numeros.de.ingresos <- function(ingresos){
  if(ingresos[1] > ingresos[2]){
    temporal <- ingresos[1]
    ingresos[1] <- ingresos[2]
    ingresos[2] <- temporal
  } 
  if(ingresos[2] > ingresos[3]){
    temporal <- ingresos[2]
    ingresos[2] <- ingresos[3]
    ingresos[3] <- temporal
  } 
  if(ingresos[1] > ingresos[2]){
    temporal <- ingresos[1]
    ingresos[1] <- ingresos[2]
    ingresos[2] <- temporal
  } 
  if(ingresos[2] > ingresos[3]){
    temporal <- ingresos[2]
    ingresos[2] <- ingresos[3]
    ingresos[3] <- temporal
  }
  return(ingresos)
}
ingresos

##RESPUESTA COMPLETA AL EJERCICIO 4##

vector.de.ingresos <- numeros.de.ingresos(ingresos)
print(paste("De acuerdo a los datos recopilados desde el ano 2012 hasta el ano 2017 segun los ingresos de explotacion, el pais que menos tuvo ingresos fue Chile con un",
            ingresos[1], ", luego el paIs que quedo en segundo lugar fue Peru con",ingresos[2],", por ultimo, el pais que obtuvo la mayor cantidad de ingresos fue Colombia con",
            ingresos[3]))
            

##EJERCICIO 5##

##Si la tasa de interes es de chile multiplicar por 0,1##
##Si la tasa de interes es de peru sumar 0,3##
##Si la tasa de interes es de colombia dividir por 10##              

tasa.interes.chile <-  latam.empresas %>% filter(pais == "chile") %>% 
              mutate(tasa.interes.nueva = tasa_interes * 0.1)
tasa.interes.peru <-  latam.empresas %>% filter(pais == "peru") %>% 
              mutate(tasa.interes.nueva = tasa_interes + 0.3)
tasa.interes.colombia <-  latam.empresas %>% filter(pais == "colombia") %>% 
              mutate(tasa.interes.nueva = tasa_interes / 10)
  
  
latam.empresas <- rbind(tasa.interes.chile, tasa.interes.peru , tasa.interes.colombia)

##EJERCICIO 6##
##Reemplazar en la columna exportaciones con 1 cuando es mayor a 2,1, con un 2 cuando es menor 2,1 y un 3 cuando es igual a 2,1, redondee al primer decimal la variable##

library(dplyr)

latam.empresas <- mutate(latam.empresas, exportaciones1 = ifelse(latam.empresas[6] > 2.1,1,0))

latam.empresas <- mutate(latam.empresas, exportaciones2 = ifelse(latam.empresas[6] < 2.1,2,0))

latam.empresas <- mutate(latam.empresas, exportaciones3 = ifelse(latam.empresas[6] == 2.1,3,0))




