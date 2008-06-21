<!-- -*- mode: markdown; coding: utf-8; -*- -->

## JSON escape

El método **json\_escape** funciona como **html\_escape**. Es muy útil cuando necesitamos mostrar strings **JSON** en una página **HTML** , por ejemplo, en un proceso de documentación.

        puts json_escape("is a > 0 & a < 10?")
        # => is a \u003E 0 \u0026 a \u003C 10?

Podemos usar el atajo **j** en ERB:

        <%= j @person.to_json %>

Si ud. desea escapar todo el código **JSON** por defecto, incluya la línea siguiente en su *environment.rb*:

        ActiveSupport.escape_html_entities_in_json = true
