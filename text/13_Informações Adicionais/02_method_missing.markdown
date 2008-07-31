<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Used method\_missing, then don't leave loose ends

Debido a la naturaleza dinámica de Ruby, el método **respond\_to?** es crucial. ¿Cuantas veces necesitamos verificar si un método existe en el objeto que estamos manipulando, o si un objeto es lo que estamos esperando (**is\_a?**)?

Sin embargo hay algo muy importante que mucha gente olvida. Mire por ejemplo esta clase que usa el método **method\_missing**:

        class Perro
          def method_missing(method, *args, &block)
            if method.to_s =~ /^ladrar/
              puts "woofwoof!"
            else
              super
            end
          end
        end

        rex = Perro.new
        rex.ladrar #=> woofwof!
        rex.ladrar! #=> woofwoof!
        rex.ladrar_y_correr #=> woofwoof!


Creo que ud conoce **method\_missing**, o no? En el ejemplo de arriba estoy creando una instacia de la clase **Perro** y llamando a los métodos **ladrar**, **ladrar!** y **ladrar_y_correr** que no existen. Entonces el método **method\_missing** es invocado, dónde uso una simple expresión regular para retornar "woofwoof!", en caso de que el nombre del m;etodo comience con ladrar.


Pero veamos que pasa cuando intento usar el método **respond\_to?**:

        rex.respond_to? :ladrar #=> false
        rex.ladrar #=> woofwoof!


Retorna false, y tiene mucho sentido dado que el método no existe realmente. Entonces es mi responsabilidad cambiar el método **respond\_to?** para que funcione correctamente con esta regla especial. Voy a cambiar mi clase así:


        class Perro
          METODO_LADRAR = /^ladrar/

          def respond_to?(method)
            return true if method.to_s =~ METODO_LADRAR
            super
          end

          def method_missing(method, *args, &block)
            if method.to_s =~ METODO_LADRAR
              puts "woofwoof!"
            else
              super
            end
          end
        end

        rex = Dog.new
        rex.respond_to?(:ladrar) #=> true
        rex.ladrar #=> woofwoof!

Ahora sí! Este es un error muy común que he visto en algunos códigos, inclusive el propio Rails. Intente ejecutar el método  **respond\_to?** para verificar la existencia de métodos como **find\_by\_name**, por ejemplo.


Ruby es un lenguaje impresionante y altamente flexible, pero si no prestamos atención podemos dejar cabos sueltos como este.

Por supuesto que en Rails 2.1 este problema se solucionó, podemos usar  **respond\_to?** para verificar la existencia de métodos como **find\_by\_algo**.


