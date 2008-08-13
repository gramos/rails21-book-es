<!-- -*- mode: markdown; coding: utf-8; -*- -->

##Eager Loading

Para explicar esta nueva funcionalidad, veamos el siguiente código:

        Author.find(:all, :include => [:posts, :comments])

Estoy haciendo una búsqueda en la tabla **authors**  y también incluyendo las tablas **posts** y **comments** en mi consulta a través de la columna **author_id**, el cual es el nombre de columna por defecto de acuerdo a la conveción que rails utiliza para las claves foráneas.
Esta búsqueda genera una consulta como la siguiente:

        SELECT
          authors."id"          AS t0_r0,
          authors."created_at"  AS t0_r1,
          authors."updated_at"  AS t0_r2,
          posts."id"            AS t1_r0,
          posts."author_id"     AS t1_r1,
          posts."created_at"    AS t1_r2,
          posts."updated_at"    AS t1_r3,
          comments."id"         AS t2_r0,
          comments."author_id"  AS t2_r1,
          comments."created_at" AS t2_r2,
          comments."updated_at" AS t2_r3
        FROM
          authors
          LEFT OUTER JOIN posts ON posts.author_id = authors.id
          LEFT OUTER JOIN comments ON comments.author_id = authors.id

Una única consulta SQL con **joins** entre las tablas  **authors**, **posts** y **comments**. A esto lo llamamos **producto cartesiano**.

Este tipo de consultas no siempre tiene una buena performance, entonces esto se cambió en Rails 2.1. La misma consulta para la clase **Author** ahora se hace de una forma diferente para traer la información de las tres tablas. En vez de usar una única consulta SQL con las tres tablas, Rails ahora usa tres consultas diferentes - una por cada tabla - las cuales son más cortas que la anterior. El resultado se puede ver en los logs despues de ejecutar el codigo ruby on rails previo:

        SELECT * FROM "authors"
        SELECT posts.* FROM "posts" WHERE (posts.author_id IN (1))
        SELECT comments.* FROM "comments" WHERE (comments.author_id IN (1))

En la **mayoría de los casos** estas tres simples consultas se ejecutan más rápido que la consulta larga y compleja.

