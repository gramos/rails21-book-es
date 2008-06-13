<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Find

### Conditions

A partir de ahora, se va a poder pasar un objeto como parámetro al método  **find** de  **ActiveRecord**, Vea este caso como ejemplo:

        class Account < ActiveRecord::Base
          composed_of :balance, :class_name => "Money", :mapping => %w(balance amount)
        end

En este caso, ud. puede pasar una instancia de **Money** cómo parámetro al método **find** de la clase  **Account**, de la siguiente manera:

        amount = 500
        currency = "USD"
        Account.find(:all, :conditions => { :balance => Money.new(amount, currency) })

### Last

Hasta ahora sólo podíamos usar tres operadores para buscar datos usando el método **find** de **ActiveRecord**: **:first**, **:all** o el propio id del objeto (en este caso no pasamos ningún operador específico más que el id en sí mismo)

En Rails 2.1 hay un cuarto operador llamado  **:last**. Vea algunos ejemplos:

        Person.find(:last)
        Person.find(:last, :conditions => [ "user_name = ?", user_name])
        Person.find(:last, :order => "created_on DESC", :offset => 5)

Para entender como funciona este nuevo operador, veamos el siguiente test:

        def test_find_last
          last  = Developer.find :last
          assert_equal last, Developer.find(:first, :order => 'id desc')
        end

### All

El método estático **all** es un alias al método estático **find(:all)**. Por ejemplo:

        Topic.all es lo mismo que Topic.find(:all)

### First

El método estático **first** es un alias al método estático **find(:first)**. Por ejemplo:

        Topic.first es lo mismo que Topic.find(:first)

### Last

El método estático **last** es un alias al método estático **find(:last)**. Por ejemplo:

        Topic.last es lo mismo que Topic.find(:last)


## Usando **first** y **last** con named\_scope

Todo los métodos mencionados anteriormente funcionan con **named\_scope**. Supongamos que creamos un **named\_scope** llamado **recent**. Entonces podríamos hacer esto:

                post.comments.recent.last
