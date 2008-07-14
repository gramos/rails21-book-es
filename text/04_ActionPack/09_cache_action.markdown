<!-- -*- mode: markdown; coding: utf-8; -*- -->

## caches\_action acepta condicionales

El método **caches\_action** ahora acepta la opción **:if**, permitiendo el uso de condicionales para especificar cuando una acción (**action**) puede ser cacheada (**cached**) Por ejemplo:

        caches_action :index, :if => Proc.new { |c| !c.request.format.json? }

En el ejemplo de arriba, la **acción index** será cacheada únicamente si no es accedida por una petición JSON.

