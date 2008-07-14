<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Cache

Ahora todos los métodos de **fragment\_cache\_key** retornan por defecto el namespace 'view/' como prefijo.

Se eliminaron todos los caching store de **ActionController::Caching::Fragments::*** y ahora están en **ActiveSupport::Cache::***. En este caso, si ud. a hecho una referencia a store, como por ejemplo: **ActionController::Caching::Fragments::MemoryStore**, va a tener que cambiarla por: **ActiveSupport::Cache::MemoryStore**.

**ActionController::Base.fragment\_cache\_store* no va más, y **ActionController::Base.cache\_store** toma su lugar.

Se incluyó en  **ActiveRecord::Base** el método **cache\_key** que facilita el modo de almacenamiento de cache de Active Records mediante la nueva biblioteca **ActiveSupport::Cache::***. Funciona así:

        >> Product.new.cache_key
        => "products/new"

        >> Product.find(5).cache_key
        => "products/5"

        >> Person.find(5).cache_key
        => "people/5-20071224150000"

Se incluyó **ActiveSupport::Gzip.decompress/compress** para facilitar el uso de como mapeo para **Zlib**.

Ahora ud. puede usar las opciones de ambiente (environment) **config.cache\_store** para especificar el valor por defecto del tipo de almacenamiento de cache. Como hemos mencionado si existe el directorio **tmp/cache**, el valor por defecto es **FileStore**, en otro caso se usará **MemoryStore**, puede configurarlo de la siguiente manera:

        config.cache_store = :memory_store
        config.cache_store = :file_store, "/path/to/cache/directory"
        config.cache_store = :drb_store, "druby://localhost:9192"
        config.cache_store = :mem_cache_store, "localhost"
        config.cache_store = MyOwnStore.new("parameter")


Para hace las cosas más fáciles aún, el comentario de abajo se incluye en *environments/production.rb*, en favor de recordarle estas opciones.


        # Use a different cache store in production
        # config.cache_store = :mem_cache_store
