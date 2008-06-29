<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Una nueva forma de usar partials

El uso de partials es algo muy común para eliminar la duplicación de código en el desarrollo de software con Rails. Aquí hay un ejemplo:

        <% form_for :user, :url => users_path do %>
                <%= render :partial => 'form' %>
                <%= submit_tag 'Create' %>
        <% end %>

Un **Partial** es un fragmento de código (una plantilla). La ventaja de usar un **partial** es eliminar la duplicación innecesaria de código. Usar un **partial** es muy simple, puede comenzar con algo como esto: **render :partial => "name"**. Y debe crear un archivo con el mismo nombre que su **partial**, pero anteponiéndole un guión bajo

En el código de arriba vimos como podemos usar un patial, en Rails 2.1 ud. va a poder hacer lo mismo pero una forma un poco diferente:

        <% form_for(@user) do |f| %>
                <%= render :partial => f %>
                <%= submit_tag 'Create' %>
        <% end %>

En este ejemplo vamos a renderizar el partial "users/\_form", el cual va a recibir una variable llamada "form" con las referencias creadas por **FormBuilder**.

La vieja forma continúa funcionando en Rails 2.1

