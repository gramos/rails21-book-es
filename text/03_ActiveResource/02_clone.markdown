<!-- -*- mode: markdown; coding: utf-8; -*- -->

## El método clone

Ahora podemos clonar un recurso existente:

        ryan = Person.find(1)
        not_ryan = ryan.clone
        not_ryan.new?  # => true

Note que el objeto copiado no ha clonado ningún atributo de la clase, apenas los atributos del recurso.

        ryan = Person.find(1)
        ryan.address = StreetAddress.find(1, :person_id => ryan.id)
        ryan.hash = {:not => "an ARes instance"}

        not_ryan = ryan.clone
        not_ryan.new?            # => true
        not_ryan.address         # => NoMethodError
        not_ryan.hash            # => {:not => "an ARes instance"}