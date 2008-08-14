## config.gem

Ahora es posible configurar todas las gemas necesarias para obtener un proyecto listo para su ejecución usando una nueva característica llamada **config.gem**. En el archivo **environment.rb** puedes especificar de qué gemas depende tu proyecto para ejecutarse correctamente. Veamos un ejemplo: 

	config.gem "bj" 

	config.gem "hpricot", :version => '0.6',
	                      :source => "http://code.whytheluckystiff.net" 

	config.gem "aws-s3", :lib => "aws/s3"

Para instalar todas las dependencias de una sola vez, utilizamos una tarea Rake: 

	# Instala todas las gemas especificadas
	rake gems:install

También es posible listar cuales gemas están siendo usadas en el proyecto ejecutando: 

	# Listando todas las dependencias
	rake gems

Si una de las gemas tiene un archivo **rails/init.rb** y vos querés llevar la gema con tu aplicación, puedes hacer: 

	# Copia la gema especificada a vendor/gems/nome_do_gem-x.x.x
	rake gems:unpack GEM=gem_name

Entonces, la gema será copiada al directorio **vendor/gems/gem\_name-x.x.x**. En caso de no especificar el nombre de la gema, Rails copiará todas las gemas al directorio **vendor/gem**

## config.gem en plugins

El comando **config.gem** está también disponible para ser utilizado con plugins.

Hasta Rails 2.0, el archivo **init.rb** de un plugin solía lucir de la siguiente forma: 

	# init.rb del plugin open_id_authentication
	require 'yadis' 
	require 'openid' 
	ActionController::Base.send :include, OpenIdAuthentication 

Pero en Rails 2.1 el archivo **init.rb** sería:

	config.gem "ruby-openid", :lib => "openid", :version => "1.1.4"
	config.gem "ruby-yadis",  :lib => "yadis",  :version => "0.3.4" 

	config.after_initialize do
	  ActionController::Base.send :include, OpenIdAuthentication
	end

Así que, cuando ejecute la tarea para instalar todas las gemas necesarias, éstas estarán entre ellas.
