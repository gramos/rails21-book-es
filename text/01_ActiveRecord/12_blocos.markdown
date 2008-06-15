<!-- -*- mode: markdown; coding: utf-8; -*- -->

## ActiveRecord::Base.create acepta bloques

Estamos acostumbrados al método **ActiveRecord::Base.new** que acepta el uso de bloques. Ahora podemos hacer lo mismo con el método  **create**:

        # Creación de un nuevo objeto pasándole un bloque con la descripción de sus atributos
        User.create(:first_name => 'Jamie') do |u|
          u.is_admin = false
        end

Podemos usar este mismo método para crear muchos objetos de una sola vez:

        # Creación de un array de objetos nuevos usando un bloque.
        # El bloque se ejecuta una vez por cada nuevo objeto creado.
        User.create([{:first_name => 'Jamie'}, {:first_name => 'Jeremy'}]) do |u|
          u.is_admin = false
        end

Esto también funciona para las asociaciones:

        author.posts.create!(:title => "New on Edge") {|p| p.body = "More cool stuff!"}

        # o

        author.posts.create!(:title => "New on Edge") do |p|
          p.body = "More cool stuff!"
        end
