<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Relaciones de sólo lectura

Se agregó una nueva caraterística a las relaciones entre modelos. Con el fin de impedir alterar los modelos ahora podemos usar **:readonly** para asociar modelos. Veamos algunos ejemplos:

        has_many :reports, :readonly => true

        has_one :boss, :readonly => :true

        belongs_to :project, :readonly => true

        has_and_belongs_to_many :categories, :readonly => true

De esta manera los registros protegidos no podrán ser alterados desde este modelo. Si intentamos editar algunos de los registros de este modelos entonces obtendríamos la siguiente excepción: **ActiveRecord::ReadOnlyRecord**
