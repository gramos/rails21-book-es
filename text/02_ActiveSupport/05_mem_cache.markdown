<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Mem\_cache\_store ahora acepta opciones

La inclusión de **Memcache-Client** dentro de **ActiveSupport::Cache** facilitó mucho las cosas, pero también eliminó la flexibilidad no permitiendo configurar nada más que el número de IP del servidor de **memcached**.

**Jonathan Weiss** hizo un parche que fue incluido en Rails, que permite opciones extras como estas:

        ActiveSupport::Cache.lookup_store :mem_cache_store, "localhost"

        ActiveSupport::Cache.lookup_store :mem_cache_store, "localhost", '192.168.1.1',
                :namespace => 'foo'

o

        config.action_controller.fragment_cache_store = :mem_cache_store, 'localhost',
                {:compression => true, :debug => true, :namespace =>'foo'}
