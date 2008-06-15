<!-- -*- mode: markdown; coding: utf-8; -*- -->

## change\_table

La creación de migraciones (**migrations**) en Rails 2.0 se hizo mucho más sexy que en las versiones previas, pero alterar una tabla usando **migrations** continuaba siendo como antes, nada sexy.

En Rails 2.1, ahora también es sexy alterar una tabla, con el nuevo método **change\_table**. Veamos el ejemplo:

        change_table :videos do |t|
          t.timestamps # esto agrega las columnas created_at y updated_at
          t.belongs_to :goat # esto agrega la columna goat_id (integer)
          t.string :name, :email, :limit => 20 # esto agrega las columnas name y email
          t.remove :name, :email # esto elimina las columnas name y email
        end


El nuevo método **change\_table** funciona como **create\_table** pero en vez de crear un tabla modifica una ya existente agregando o eliminando columnas e índices.

        change_table :table do |t|
          t.column # agrega una columna normal. Ej: t.column(:name, :string)
          t.index # agrega un nuevo índice.
          t.timestamps
          t.change # cambia la definición de una columna. Ej: t.change(:name, :string, :limit => 80)
          t.change_default # cambia el valor por defecto de una columna.
          t.rename # cambia el nombre de una columna.
          t.references
          t.belongs_to
          t.string
          t.text
          t.integer
          t.float
          t.decimal
          t.datetime
          t.timestamp
          t.time
          t.date
          t.binary
          t.boolean
          t.remove
          t.remove_references
          t.remove_belongs_to
          t.remove_index
          t.remove_timestamps
        end
