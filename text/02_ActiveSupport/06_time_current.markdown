<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Time.current

Un nuevo método para la clase **Time**. El método **current** retorna dependiendo de si fue especificado antes **config.time\_zone**, **Time.zone.now**, de otra manera retorna **Time.now**.

        # retorna un valor que depende de config.time_zone
        Time.current


los métodos **since** y **ago** también cambiaron sus valores de retorno, retornando un **TimeWithZone** en caso de que se especifique **config.time\_zone**.

Esto convierte al método **Time.current** en el nuevo método por defecto para obtener la hora actual, reemplazando a **Time.now** (el cual sigue existiendo, pero no tiene en cuenta el timezone especificado).

Los métodos **datetime\_select**, **select\_datetime** y **select\_time** se actualizaron para que tengan como valor de retorno **Time.current**.

