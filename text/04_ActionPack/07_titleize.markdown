<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Aplicando formato de título en strings.

Había un bug cuando usábamos el método **String#titleize** en un string que contenía 's. El bug hacía que el método returne la 's en mayúsculas. Vea el ejemplo:

        >> "brando's blog".titleize
        => "Brando'S Blog"

Vea el ejemplo que con el bug corregido:

        >> "brando's blog".titleize
        => "Brando's Blog"
