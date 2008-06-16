<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Partial Updates

La implementación de **Dirty Objects** dió punto de partida a otra característica muy interesante.

Dado que ahora podemos rastrear los cambios de los atributos de un objeto, ¿por qué no usar esto para evitar actualizaciones innecesarias en la base de datos?


En las versiones previas de Rails cuando ejecutábamos el método **save** de un objeto **ActiveRecord**, se actualizaban todos los campos en la base de datos. Por más que los mismos no hayan sufrido ningún cambio.

Con **Dirty Objects** esta acción podría mejorarse, y esto es exactamente lo que pasó. Miremos un poco la consulta SQL generada en Rails 2.1 cuando intentamos guardar un objeto que a sufrido un pequeño cambio:

        article = Article.find(:first)
        article.title  #=> "Title"
        article.subject  #=> "Edge Rails"

        # Cambiamos el título (title)
        article.title = "New Title"

        # esto crea el siguiente SQL para persistir el objeto
        article.save
        #=>  "UPDATE articles SET title = 'New Title' WHERE id = 1"

Note como sólo se actualizaron en la base de datos los campos que fueron cambiados en la aplicación. Si ningún campo ha sido actualizado en la aplicación, entonces **ActiveRecord** no ejecutará ninguna actualización.

Para habilitar/deshabilitar esta nueva característica debe cambiar la propiedad **partial\_updates** de sus modelos.

        # Para habilitarla
        MyClass.partial_updates = true


Si desea habilitar/deshabilitar esta característica para todos sus modelos debe editar el archivo *config/initializers/new\_rails\_defaults.rb*:

        # Habilitando para todos los modelos
        ActiveRecord::Base.partial_updates = true

No olvide informarle a Rails a través *config/initializers/new\_rails\_defaults.rb* que va a actualizar un atributo sin usar el método **attr=**, así:

        # Si usa **attr=**,
        # entocnes está bien no informar nada.
        person.name = 'bobby'
        person.name_change    # => ['bob', 'bobby']


        # Pero debe informar que el campo se va actualizar
        # si no va a usar **attr=**
        person.name_will_change!
        person.name << 'by'
        person.name_change    # => ['bob', 'bobby']

Si ud. no informa cambios como estos, no se podrán rastrear los cambios de los atributos del modelo y la tabla no se actualizará correctamente.

