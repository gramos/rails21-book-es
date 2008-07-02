## Tareas

### rails:update

De ahora en más, cada vez que ejecutes la tarea **rake rails:freeze:edge**, esta también ejecutará  **rails:update**, actualizando los archivos de configuración y los *JavaScripts*.

### Base de datos en 127.0.0.1

Un cambio fue realizado en el archivo database.rake que solía buscar unicamente en localhost bases de datos locales. Ahora considerará **127.0.0.1**. Esto funciona para las tareas **create** y **drop**. El archivo database.rake también fue refactorizado para hacer el codigo menos repetitivo. 

### Congelando a una versión de Rails específica.

Hasta Rails 2.1 no era posible congelar a una versión de Rails específica dentro de un proyecto. Solo podías utilizar la Revisión como parámetro. En Rails 2.1, podemos congelar a una versión específica con el siguiente comando: 

	rake rails:freeze:edge RELEASE=1.2.0

## TimeZone

#### rake time:zones:all

Devuelve todas las zonas horarias conocidas para Rails, agrupadas por uso horario. También podés filtar los valores retornados usando el parámetro óptico OFFSET, por ejemplo: OFFSET=-6.

#### rake time:zones:us

Muestra lista con todas las zonas horarias de Estados Unidos. La opción OFFSET también es valida en este contexto.

#### rake time:zones:local

Retorna todas las zonas horarias conocidas por Rails que están en el mismo uso horario que tu sistema operativo. 

