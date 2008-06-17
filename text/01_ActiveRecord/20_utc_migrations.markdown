<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Timestamped Migrations

Cuando se está estudiando Rails o cuando estamos desarrolando algo sólos, las **migraciones** parecen ser la mejor solución a todos nuestros problemas. Pero cuando estamos trabajando en un proyecto con un equipo de desarrolladores de distintas partes del mundo, ud. descurbrirá (si aún no lo hizo) que las migrations no funcionan bien. Las nuevas migraciones (timestamped migrations) de Rails 2.1 vienen al rescate.

Antes de la llegada de **timestamped migrations**, cada nueva migración tenía un número antepuesto al nombre de la migración. Si dos migraciones eran generadas por distintos desarrolladores y no se comiteaba de inmediato, entonces podían terminar teniendo el mismo número de migración pero con diferente información. En este punto su esquema_info está desactualizado y ud. tiene un conflicto.

Hay varias formas de "intentar" resolver este problema. Se crearon muchos plugins con diferentes maneras de resolver esto. Más allá de los plugins disponibles, una cosa era clara: la antigua forma simplemente no funcionaba.

Si ud. estuviese usando Git, entonces se podría complicar mucho más, su equipo probablemente tenga algunas ramas (branches) con **migraciones** desactualizadas en tdoas ellas. Probablemente tenga serios conflictos a la ahora de hacer un merge de esas ramas (branches).

Para resolver este gran problema, el core team de Rails cambió el funcionanmiento de las migraciones. En vez de anteponer cada archivo de migración con un número, ahora se le antepone con un string basado en la hora **UTC** con el siguiente formato  YYYYMMDDHHMMSS.

Así mismo se creó una nueva tabla llamada **schema_migrations**, esta almacena las **migraciones** ejecutadas hasta el momento. De esta manera, si alguien crea una migración con un número bajo, rails hará un  **rollback** de las migraciones hasta la versión previa y luego se correrán todo de nuevo hasta la versión actual.


Esto aparentemente, resuelve el problema de las **migraciones**.

Hay una opción para deshabilitar esta caraterística, agregando esta línea en el archivo **envronment.rb**:

        config.active_record.timestamped_migrations = false

También hay algunas tareas de rake nuevas para "navegar" a través de las **migraciones**:


        rake db:migrate:up
        rake db:migrate:down

