<!-- -*- mode: markdown; coding: utf-8; -*- -->

## ¿UTC o GMT?

Una pregunta simple, pero interesante. Hasta ahora Rails estuvo usando mucho la sigla UTC, pero cuando se ejecuta el método **to\_s** de **TimeZone**, este muestra GMT, no UTC. Esto es debido al hecho de que el acrónimo GMT es más común entre los usuarios finales.

Si ud. mira en el panel de control de Windows, dónde se puede seleccioar el timezone, verá el que el acrónimo utilizado es GMT. Google y Yahoo también están usando GMT dentro de sus productos.

        TimeZone['Moscow'].to_s #=> "(GMT+03:00) Moscow"
