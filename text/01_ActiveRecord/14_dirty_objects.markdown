<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Dirty Objects

Ahora en Rails podemos ratrear los cambios hechos por **ActiveRecord**.. Se puede saber si un objeto ha sido modificado o no. En caso de que haya cambiado, podemos ver que fue lo que cambió exactamente como así también comparar su estado anterior con el actual. Veamos algunos ejemplos:

        article = Article.find(:first)
        article.changed?  #=> false

        article.title  #=> "Title"
        article.title = "New Title"
        article.title_changed? #=> true

        # muestra title antes del cambio
        article.title_was  #=> "Title"

        # antes y despues del cambio
        article.title_change  #=> ["Title", "New Title"]

Como ud. puede ver es muy simple. Puede listar todos los cambios hechos al objeto de una esta dos formas:

        # retorna una lista con todos los atributos que cambiaron
        article.changed  #=> ['title']

        # retorna un hash con los atributos que cambiaron
        # con sus valores antes y después
        article.changes  #=> { 'title' => ["Title", "New Title"] }

Note que cuando el objeto se guarda su estado de alterado cambia:

        article.changed?  #=> true
        article.save  #=> true
        article.changed?  #=> false

En caso de ud. quiera cambiar el estado de un objeto sin usar **attr=**, va a necesitar informar explícitamente que se ha modificado el atributo mediante el método **attr\_name\_will\_change!** (reemplace **attr** con el nombre real del atributo del objeto). Veamos un ejemplo más:

        article = Article.find(:first)
        article.title_will_change!
        article.title.upcase!
        article.title_change  #=> ['Title', 'TITLE']
