<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Almacenando el nombre completo de una clase cuando usamos STI

Siempre que usemos **models** con **namespace** y **STI**, **ActiveRecord** sólo almacena el nombre de la clase, sin el nombre del **namespace** (*demodulized*). Esto sólo funcionará si todas las clses en el **STI** estan en el mismo **namespace**. Veamos un ejemplo:

        class CollectionItem < ActiveRecord::Base; end
        class ComicCollection::Item < CollectionItem; end

        item = ComicCollection::Item.new
        item.type # => 'Item'

        item2 = CollectionItem.find(item.id)
        # retorna un error, por que no puede encontrar
        # la clase Item

Este cambio agrega una nueva opción que hace que **ActiveRecord** almacene el nombre completo de la clase.

Para habilitar/deshabilita esta característica, ud. debe incluir o editar lo siguiente en su **environment.rb**.

        ActiveRecord::Base.store_full_sti_class = true

El valor por defecto es true.

