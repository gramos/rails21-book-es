<!-- -*- mode: markdown; coding: utf-8; -*- -->

## ActionController::Routing

### Map.root

Ahora, podemos usar un alias con  **map.root** para que sea mucho más **DRY**.

En las primeras versiones de rails ud. hacia esto:

        map.new_session :controller => 'sessions', :action => 'new'
        map.root :controller => 'sessions', :action => 'new'


Ahora puede hacer lo mismo de la siguiente manera:

        map.new_session :controller => 'sessions', :action => 'new'
        map.root :new_session

### Reconocimiento de Rutas

La vieja implementación del reconocimiento de rutas recorría todas la rutas una a una, lo que hacía que terminara consumiendo mucho tiempo. Se desarrolló una nueva y más inteligente implementación. Esta crea un árbol para las rutas y el reconocimiento de rutas se hace mediante un prefijo, dejando de lado las rutas similares. Esta aproximación baja el tiempo de reconocimiento en aproximadamente 2.7 veces.

Todas las nuevas implementaciones están en el archivo **recognition\_optimisation.rb** y los detalles de su funcionamiento están en los comentarios. Vea la documentación dentro del código fuente para más información.

### Assert_routing

Ahora es posible testear una ruta con un método HTTP. Vea el siguiente ejempo:

        assert_routing({ :method => 'put',
                         :path => '/product/321' },
                       { :controller => "product",
                         :action => "update",
                         :id => "321" })

### Map.resources

Image que tiene un sitio escrito en español, y quiere remodelar todas las rutas para que también para que se correspondan con el idioma. En otras palabras, en vez de tener:

        http://www.mysite.com.br/products/1234/reviews

quisiera tener algo así:

        http://www.mysite.com.br/productos/1234/comentarios



Esto era posible, pero no en de una forma simple y sin comprometer algunas de las convenciones de rails.

Ahora tenemos la opción **:as** dentro de **map.resources** para personalizar nuestras rutas. Mire el ejemplo para obtener la URL de arriba en español:

        map.resources :products, :as => 'productos' do |product|
          # product_reviews_path(product) ==
          # '/productos/1234/comentarios
          product.resources :product_reviews, :as => 'comentarios'
        end