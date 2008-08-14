## Plugins

### Las Gemas ahora pueden ser plugins

Ahora, cualquier gema que tenga un archivo **rails/init.rb** puede ser instalado dentro del directorio **vendor** de tu proyecto Rails igual que un **plugin**.

### Usando generadores en plugins

Es posible configurar **Rails** para buscar **plugins** en directorios diferentes a **vendor/plugins**, solo incluyendo esta línea de código en el archivo **environment.rb**.

	config.plugin_paths = ['lib/plugins', 'vendor/plugins']

Rails 2.0 tenía un bug en esta configuración que mostraba cuando un plugin tenía generadores. Por ese bug, Rails solo encuentraba generadores en plugins que estuvieran dentro de **vendor/plugins**. En Rails 2.1 ese bug fue corregido.  	
