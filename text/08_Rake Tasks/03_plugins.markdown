## Plugins

### Gemas ahora pueden ser plugins

Ahora, cualqioer gema que tenga un archivo **rails/init.rb** puede ser instalado dentro del directorio **vendor** de tu proyecto Rails igual que un **plugin**.

### Usando generadores en plugins

Es posible configurar **Rails** para buscar **plugins** en directorios diferentes a **vendor/plugins**, solo incluyendo esta línea de código en el archivo **environment.rb**.

	config.plugin_paths = ['lib/plugins', 'vendor/plugins']

Rails 2.0 tenía un bug en esta configuración que muestraba cuando un plugin tenía generadores. Por ese bug, Rails solo encuentra generadores en plugins que estén dentro de **vendor/plugins**. En Rails 2.1 ese bug fue corregido.  	
