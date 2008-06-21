<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Named_scope

La gema  *has\_finder*  ha sido incluida en Rails pero con un nombre diferente: **named\_scope**.

Para entender lo que significa este agregado en Rails vamos a ver los siguientes ejemplos:

        class Article < ActiveRecord::Base
          named_scope :published, :conditions => {:published => true}
          named_scope :containing_the_letter_a, :conditions => "body LIKE '%a%â€™"
        end

        Article.published.paginate(:page => 1)
        Article.published.containing_the_letter_a.count
        Article.containing_the_letter_a.find(:first)
        Article.containing_the_letter_a.find(:all, :conditions => {â€¦})

En vez de crear un método nuevo llamado **published** para retornar todos los posts publicados, estoy usando un **named\_scope** para que lo haga por mí. Pero puedo ir más allá que esto. Vamos a ver otro ejemplo para ver como se puede usar esto:

        named_scope :written_before, lambda { |time|
          { :conditions => ['written_on < ?', time] }
        }

        named_scope :anonymous_extension do
          def one
            1
          end
        end

        named_scope :named_extension, :extend => NamedExtension

        named_scope :multiple_extensions,
                :extend => [MultipleExtensionTwo, MultipleExtensionOne]

## Testeando named\_scope con proxy\_options


**Named scopes** es una nueva e interesante caraterística de Rails 2.1, pero después de usarlo durante un tiempo quizás sea díficil testear estas estructuras más complejas.

Veamos un ejemplo:

                class Shirt < ActiveRecord::Base
                  named_scope :colored, lambda { |color|
                    { :conditions => { :color => color } }
                  }
                end


¿Cómo creamos un test que valide la generación de este scope ?

Para solucionar esto, se creó el método **proxy\_options**. El cual nos permite examinar las opciones usadas en **named_scope**. Para testear el código de arriba podríamos escribir esto:

                class ShirtTest < Test::Unit
                  def test_colored_scope
                    red_scope = { :conditions => { :colored => 'red' } }
                    blue_scope = { :conditions => { :colored => 'blue' } }
                    assert_equal red_scope, Shirt.colored('red').scope_options
                    assert_equal blue_scope, Shirt.colored('blue').scope_options
                  end
                end
