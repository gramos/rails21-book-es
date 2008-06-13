<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Incremento y decremento

Los métodos de **ActiveRecord** **increment**, **increment!**, **decrement** y **decrement!** ahora toman un nuevo parámetro opcional. En las versiones previas de Rails se podían usar estos métodos para restar 1 a una columna dada.  En rails 2.1 podemos decir que valor restar o sumar. Así:

        player1.increment!(:points, 5)
        player2.decrement!(:points, 2)

En el ejemplo estoy sumando 5 puntos al jugador 1 y restando 2 puntos al jugador 2. Cómo este es un parámetro opcional, el código viejo no se ve afectado.

