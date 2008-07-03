## Scripts

### plugin

El comando script/plugin install ahora provee la opción -e/--export que emite un svn export.  
Se agregó soporte para plugins alojados en repositorios GIT.


### dbconsole

Este script hace lo mismo que script/console, solo que para la base de datos. En otras palabras, te conecta con el cliente por línea de comando de tu base de datos.

Mirando al código, este funcionaría solamente con mysql, postgresql y sqlite(3). Cuando sea especificada otra base de datos en el archivo database.yml, el script mostrará: "not supported for this database type".
