<!-- -*- mode: markdown; coding: utf-8; -*- -->

## ¿Smallint, int o bigint en MySQL?

El adapatador para **MySQL** de **ActiveRecord** es un poco más inteligente en el uso tipos de datos enteros a la hora de crear o alterar columnas en la base de datos. Con la opción **:limit**, podemos definir si la columna va a ser **smallint**, **int** or **bigint**. Veamos el código que hace este trabajo:

        case limit
        when 0..3
          "smallint(#{limit})"
        when 4..8
          "int(#{limit})"
        when 9..20
          "bigint(#{limit})"
        else
          'int(11)'
        end

Para dejar esto más claro vamos a mapear esto en un archivo de migración y ver que tipo de dato se usa para cada columna:

        create_table :table_name, :force => true do |t|

          # 0 - 3: smallint
          t.integer :column_one, :limit => 2 # smallint(2)

          # 4 - 8: int
          t.integer :column_two, :limit => 6 # int(6)

          # 9 - 20: bigint
          t.integer :column_three, :limit => 15 # bigint(15)

          # si no usamos :limit int(11)
          t.integer :column_four # int(11)
        end

El adaptador de **PostgreSQL** tenía esta caraterística y **MySQL** sólo siguió esta tendencia.

