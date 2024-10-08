# PalmerPenguins
Trabajo realizado en R para la visualizacion de palmerpenguins.


---
title: "Razas de Pinguinos"
author: "Cristian Escamilla"
date: "2024-10-08"
output: html_document
---
Se importa la libreria de (tidyverse) y los datos (palmerpenguins)
```{r loading packages}
library(tidyverse)
library(palmerpenguins)
```



### Taller: Módulo de Software para el manejo de datos

Cargue a RStudio el conjunto de datos "Pingüinos" del paquete datos. Pinguinos incluye medidas de especies de las islas del Archipelago de Palmer, incluye tamaño(largo de aleta, masa corporal, dimensiones de pico) y sexo de los pinguinos. Muestro la siguiente tabla donde se visualizan las 5 primeras observaciones del conjunto de datos.

![image](https://github.com/user-attachments/assets/affd8ba6-fbc7-4b72-a040-de1c6938c48e)


```{r encabezado de datos}
head(penguins)
```
#### Se muestra parte de los datos.

#### Revisé la estructura del conjunto de datos penguins
```{r}
str(penguins)
```

Identifique las especies de pinguinos, las islas y los años de la información que contiene "penguins"

```{r species}
unique(penguins$species)
```

```{r islad}
unique(penguins$island)
```

```{r}
unique(penguins$year)
```

Se instala la libreria modelsummary y con la función datasummary_skim() se genera el siguiente resumen de datos

```{r}
library(modelsummary)
datasummary_skim(penguins)
```

**¿Cuánto miden en promedio el largo y alto de los picos de los pinguinos de la muestra?**

Promedio de largo es = 43.9 mm

**¿Cuál es el peso corporal máximo de los pinguinos de la muestra?**

Promedio de alto es = 17.2 mm

#### Recree el código en R para generar la siguiente tabla que muestra el minimo, el máximo y la media aritmética de las medidas del largo de las aletas de los pinguinos, clasificada por especie.
```{r}
penguins%>%
  group_by(species)%>%
  summarise("minimo" = min(flipper_length_mm, na.rm = TRUE),
            "maximo" = max(flipper_length_mm, na.rm = TRUE),
            "madia" = mean(flipper_length_mm, na.rm = TRUE))
```

### Visualización de datos

Recree el código R para generar la siguiente gráfica que muestra la distribución de los datos sobre la longitud de las aletas de los pinguinos de la muestra clasificado por especie y por isla.

```{r clasificado de especies}
penguins%>%
  ggplot(aes(x=flipper_length_mm, fill = species))+ 
  ggtitle("Grafico 1: Distribución de la longitud de las aletas de los pingunos")+
  facet_grid(rows = var(islands), margins = FALSE)+
  geom_density(alpha = 0.4)+
  labs(subtitle = "(diferenciado por especie e isla)",
       caption = "Datos provenientes de pinguinos dataset",
       x= "Longitud de aleta",
       y= " ",
       color = "Especie de pinguino")
```





Utilizando la ggplot y geom_point muestra un diagrama de dispersion de las especies divididas por colores y simbolos diferentes.



```{r}
	ggplot(data = penguins)+
	  geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g, color=species))+
	  labs(title = "Palmer Penguins: Body mass vd. Flipper Length", subtitle = "Sample of Three Penguins Species", 
	  caption = "Data collect by Dr. Kristen Gorman")
```

Para tener una mejor visualización se agrega al código la función facet_wrap(~)

```{r diagrama separado por facet_grap}
ggplot(data = penguins)+
  geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g, color=species, shape = species))+
  facet_wrap(~species)+
  labs(title = "Palmer Penguins: Body Mass vs Flipper length")
```

### En este ultimo diagrama se muestran las especies separadas por tipo de sexo.

```{r sexo por especies}
ggplot(data = penguins)+
  geom_point(mapping = aes(x=flipper_length_mm, y=body_mass_g, color=species))+
  facet_grid(sex~species) 
```
