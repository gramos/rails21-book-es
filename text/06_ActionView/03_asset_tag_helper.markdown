## ActionView::Helpers::AssetTagHelper

### register\_javascript\_expansion

Este método registra uno o más archivos javascript para su inclusión cuando un símbolo, definido por el programador, es indicado como parámetro del método **javascript\_include\_tag**. La idea es llamar a este método dentro del archivo **init.rb** de tu plugin, en orden de registrar los archivos javascript que tu plugin ubica en la carpeta **public/javascripts**. Veamos como funciona: 

	# En el archivo init.rb
	ActionView::Helpers::AssetTagHelper.register_javascript_expansion 
		:monkey => ["head", "body", "tail"] 

	# En nuestar vista:
	javascript_include_tag :monkey

	# Vamos a obtener:
	<script type="text/javascript" src="/javascripts/head.js"></script>
	<script type="text/javascript" src="/javascripts/body.js"></script>
	<script type="text/javascript" src="/javascripts/tail.js"></script>


### register\_stylesheet\_expansion

Este método hace exactamente lo mismo que que el método **ActionView::Helpers::AssetTagHelper#register\_javascript\_expansion**, pero crea un símbolo para ser usado luego cuando se realicen llamadas al método **stylesheet\_link\_tag**. Veamos un ejemplo: 

	# En el archivo init.rb
	ActionView::Helpers::AssetTagHelper.register_stylesheet_expansion 
		:monkey => ["head", "body", "tail"] 

	# En nuestar vista:
	stylesheet_link_tag :monkey

	# Vamos a obtener:
	<link href="/stylesheets/head.css"  media="screen" rel="stylesheet" 
		type="text/css" />
	<link href="/stylesheets/body.css"  media="screen" rel="stylesheet" 
		type="text/css" />
	<link href="/stylesheets/tail.css"  media="screen" rel="stylesheet" 
		type="text/css" />