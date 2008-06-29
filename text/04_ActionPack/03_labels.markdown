<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Labels

Cuando creamos un nuevo formulario con **scaffold** será creado con el siguiente código:

        <% form_for(@post) do |f| %>
          <p>
            <%= f.label :title %><br />
            <%= f.text_field :title %>
          </p>
          <p>
            <%= f.label :body %><br />
            <%= f.text_area :body %>
          </p>
          <p>
            <%= f.submit "Update" %>
          </p>
        <% end %>

Se incluyó el método **label**. Este método retorna un *string* con el título de la columna dentro de un tag HTML **\<label\>**.

        >> f.label :title
        => <label for="post_title">Title</label>

        >> f.label :title, "A short title"
        => <label for="post_title">A short title</label>

        >> label :title, "A short title", :class => "title_label"
        => <label for="post_title" class="title_label">A short title</label>

¿Se dió cuenta del parámetro **for** dentro del tag? "post\_title" es el título que contiene nuetro título para el post. El tag **\<label\>** de hecho una etiqueta asociada al objeto **post\_title**. Cuando alguien hace click sobre la etiqueta (que no es un link) el controlador HTML asociado recive el foco.

Robby Russell escribió un post interesante en su blog acerca de este tema. Ud. lo puede leer en: [http://www.robbyonrails.com/articles/2007/12/02/that-checkbox-needs-a-label](http://www.robbyonrails.com/articles/2007/12/02/that-checkbox-needs-a-label)

También se incluyó el método **label\_tag** en **FormTagHelper**. Este método funciona como label, pero de una forma más simple:

        >> label_tag 'name'
        => <label for="name">Name</label>

        >> label_tag 'name', 'Your name'
        => <label for="name">Your name</label>

        >> label_tag 'name', nil, :class => 'small_label'
        => <label for="name" class="small_label">Name</label>


El método acepta la opción **:for**, Veamos un ejemplo:

        label(:post, :title, nil, :for => "my_for")

Esto va retornar algo como lo siguiente:

        <label for="my_for">Title</label>
