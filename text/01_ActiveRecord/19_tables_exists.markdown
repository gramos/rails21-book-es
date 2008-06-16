<!-- -*- mode: markdown; coding: utf-8; -*- -->

## El método table_exists?

Se agregó un nuevo método para la clase **AbstractAdapter**: **table\_exists**. Es muy simple de usar:

        >> ActiveRecord::Base.connection.table_exists?("users")
        => true
