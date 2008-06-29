<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Nuevos espacios de nombres en Atom Feed

¿Conoce el método **atom\_feed**? Es una de las nuevas características de Rails 2.0, que facilita la creación de Feeds de Atom. Veamos un ejemplo de como se usa:

En el archivo *index.atom.builder*:

        atom_feed do |feed|
          feed.title("Nome do Jogo")
          feed.updated((@posts.first.created_at))

          for post in @posts
            feed.entry(post) do |entry|
              entry.title(post.title)
              entry.content(post.body, :type => 'html')

              entry.author do |author|
                author.name("Carlos Brando")
              end
            end
          end
        end

¿Qué es un Atom feed? Atom es el nombre de estilos y metadatos en formato XML. En otras palabras es un protocolo para publicar contenidos en Internet que son actualizados con frecuencia, como un blog por ejemplo. Los Feeds se publican siempre en XML y en Atom son identificados como tipo de medios application/atom+xml.

En las primeras versiones de Rails 2.0 este método aceptaba parámetros como: **:language**, **:root_url** and **:url**, puede obtener más información acerca de estos métodos en la documentación de Rails. pero con la nueva modificación, ahora podemos incluir nuevos espacios de nombre en el elemento raíz del feed. Por ejemplo:


        atom_feed('xmlns:app' => 'http://www.w3.org/2007/app') do |feed|

Va a retornar:

        <feed xml:lang="en-US" xmlns="http://www.w3.org/2005/Atom"
                xmlns:app="http://www.w3.org/2007/app">

Modificando el ejemplo usado antes, podríamos hacer esto:

        atom_feed({'xmlns:app' => 'http://www.w3.org/2007/app',
                'xmlns:openSearch' => 'http://a9.com/-/spec/opensearch/1.1/'}) do |feed|

          feed.title("Nome do Jogo")
          feed.updated((@posts.first.created_at))
          feed.tag!(openSearch:totalResults, 10)

          for post in @posts
            feed.entry(post) do |entry|
              entry.title(post.title)
              entry.content(post.body, :type => 'html')
              entry.tag!('app:edited', Time.now)

              entry.author do |author|
                author.name("Carlos Brando")
              end
            end
          end
        end
