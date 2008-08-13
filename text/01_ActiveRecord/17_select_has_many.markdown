<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Opcional :select en has\_one y belongs\_to

Los ya conocidos métodos **has\_one** y **belongs\_to** ahora tienen la opción: **:select**.

El valor por defecto es "*" (como en "SELECT * FROM table"), pero se puede editar para recuperar sólo las columnas que vamos a usar.

No olvide incluir las **claves primarias** y las **claves foráneas**, de lo contrario obtendrá un error.

El método **belongs_to** ya no tiene la opción **:order**. Pero no se preocupe por que realmente no
era muy útil.


