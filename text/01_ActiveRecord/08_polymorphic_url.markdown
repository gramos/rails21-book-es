<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Polymorphic url

Los métodos helper para las URL polimórficas son usados para resolver de una forma más elegante una ruta nombrada cuando cuando tenemos una modelo de  **ActiveRecord**.

Estos métodos son útiles caundo queremos generar la URL para un recurso **RESTful** sin especificar el tipo de registro en cuestión.

Es muy fácil de usar. Veamos algunos ejemplos (los comentarios explican las llamdas equivalentes para las versiones anteriores a Rails 2.1)

        record = Article.find(:first)
        polymorphic_url(record) #-> article_url(record)

        record = Comment.find(:first)
        polymorphic_url(record)  #->  comment_url(record)

        # it can also identify recently created elements
        record = Comment.new
        polymorphic_url(record)  #->  comments_url()

Note como el método **polymorphic_url** es capáz de indetificar el tipo del objeto dado y generar la ruta correcta. También soporta **Recursos anidados** y **espacios de nombres**:

        polymorphic_url([:admin, @article, @comment])
        #-> this will return:
        admin_article_comment_url(@article, @comment)

También se puede usar **new**, **edit** y **formatted** como prefijos:

        edit_polymorphic_path(@post)
        #=> /posts/1/edit

        formatted_polymorphic_path([@post, :pdf])
        #=> /posts/1.pdf
