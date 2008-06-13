<!-- -*- coding: utf-8; -*- -->

## Has\_one

### Soporte para la opción through

El método **has\_one** ahora tiene la opción **through**. Esta funciona como **has_many :through**, pero en este caso representa la asociación a un objeto simple **ActiveRecord**. Ejemplo:

        class Magazine < ActiveRecord::Base
          has_many :subscriptions
        end

        class Subscription < ActiveRecord::Base
          belongs_to :magazine
          belongs_to :user
        end

        class User < ActiveRecord::Base
          has_many :subscriptions
          has_one :magazine, :through => : subscriptions,
                        :conditions => ['subscriptions.active = ?', true]
        end

### Has\_one con :source\_type

El método **has\_one :through** que acabamos de ver, puede también tomar **:source\_type** como argumento. Voy a intentar explicar esto a través de algunos ejemplos. Vamos comenzar con estas dos clases:

        class Client < ActiveRecord::Base
          has_many :contact_cards

          has_many :contacts, :through => :contact_cards
        end

Lo que estamos viendo hasta aquí es una clase **Client** la cual tiene muchos (**has_many**) tipos de contactos (**contacts**), ya que la clase **ContactCard** tiene una relación polimórfica.

Para seguir con nuestro ejemplo, vamos a crear dos clases que van a representar a **ContactCard**:

        class Person < ActiveRecord::Base
          has_many :contact_cards, :as => :contact
        end

        class Business < ActiveRecord::Base
          has_many :contact_cards, :as => :contact
        end


**Person** y **Business** están relacionadas con mi clase  **Client** a través de la tabla  **ContactCard**. En otras palabras, tengo dos tipos de contactos, personal y de negocios.

Por otro cuando intente recuperar un contacto esto no va a funcionar, veamos:

        >> Client.find(:first).contacts
        # ArgumentError: /.../active_support/core_ext/hash/keys.rb:48:
        # in `assert_valid_keys': Unknown key(s): polymorphic

Para que esto funcione tenemos que usar **:source_type**. Vamos cambiar nuestra clase  **Client**:

        class Client < ActiveRecord::Base
          has_many :people_contacts,
                   :through => :contact_cards,
                   :source => :contacts,
                   :source_type => :person

          has_many :business_contacts,
                   :through => :contact_cards,
                   :source => :contacts,
                   :source_type => :business
        end

Note que ahora tenemos dos maneras diferentes de recuperar nuestros contactos y podemos indicar que tipo de contacto **:source_type** esperamos.


        Client.find(:first).people_contacts
        Client.find(:first).business_contacts
