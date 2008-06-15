<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Cálculos

**ActiveRecord::Calculations** ha cambiado un poco para aceptar no sólo el nombre de la columna sino también el nombre de la tabla. Esto es muy útil cuando tenemos una relación entre dos tablas que tienen una columna con el mismo nombre. Los métodos afectados son: **sum** o **maximum** de **ActiveRecord** (entre otros). Para resumir ahora podemos hacer esto de estas dos formas:

        authors.categories.maximum(:id)
        authors.categories.maximum("categories.id")
