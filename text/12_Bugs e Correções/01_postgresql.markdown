<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Aregar columnas en PostgreSQL

Había un bug usando  **PostgreSQL**. El bug ocurría cuando creabamos una migración para agregar una columna en una tabla existente. Por ejemplo:


Archivo: *db/migrate/002\_add\_cost.rb*

        class AddCost < ActiveRecord::Migration
          def self.up
            add_column :items, :cost, :decimal, :precision => 6,
           :scale => 2
          end

          def self.down
            remove_column :items, :cost
          end
        end

Note que estamos creadno una columna con **:precision => 6** y  **:scale => 2**. Ahora ejecutamos **rake db:migrate** y vemos como se ve nuestra tabla en la base de datos:

<table border="1" cellspacing="0" cellpadding="5">
        <tr>
                <td><strong>Column</strong></td>
                <td><strong>Type</strong></td>
                <td><strong>Modifiers</strong></td>
        </tr>
        <tr>
                <td>id</td>
                <td>integer</td>
                <td>not null</td>
        </tr>
        <tr>
                <td>descr</td>
                <td>character varying(255)</td>
                <td></td>
        </tr>
        <tr>
                <td>price</td>
                <td>numeric(5,2)</td>
                <td></td>
        </tr>
        <tr>
                <td>cost</td>
                <td>numeric</td>
                <td></td>
        </tr>
</table>

Vea la columna "cost" que acabamos de crear. Es un **numeric** común, pero debería ser como la columna "price" de arriba, más precisamente un **numeric(6,2)**. En Rails 2.1 este error no sucede más y la columan se crea correctamente.

