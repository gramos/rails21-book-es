##Obteniendo información acerca de un plugin

Esta es una de las nuevas características de Rails 2.1 que probablemente nunca use. Digo "probablemente", porque en algunos casos específicos puede ser útil, por ejemplo, para saber la versión de un plugin. 

Para probarlo, necesitamos crear un archivo que se llame *about.yml* en el directorio del plugin, con algo como lo siguiente:

	author: Carlos Brando
	version: 1.2.0
	description: Una descripción acerca del plugin
	url: http://www.nomedojogo.com

Podemos obtener esta información luego de esta manera:

	plugin = Rails::Plugin.new(plugin_directory)
	plugin.about["author"] # => “Carlos Brando”
	plugin.about["url"] # => “http://www.nomedojogo.com”

Si encuentras algún buen uso de esta carácterística y la quieres compartir conmigo, tal vez cambie mi opinión acerca de su real necesidad. 

