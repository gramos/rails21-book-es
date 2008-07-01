## ActionView::Helpers::TextHelper

### excerpt

El método **excerpt** nos ayuda a encontrar una palabra dentro de una frase y nos devuelve la abreviatura de esa frase con el número de caracteres que se hayan especificado como parámetro antes y después de la palabra agregando "…" cuando sea necesario. Veamos un ejemplo:

	excerpt('This is an example', 'an', 5)
	# => "…s is an examp…"
	
Pero había un problema. Si cuentas, vas a notar que el método retorna 6 caracteres y no 5. Esto era un bug y fue corregido. Mira el ejemplo de la salida correcta de este método:

	excerpt('This is an example', 'an', 5)
	# => "…s is an exam…"
	
###simple\_format

El método **simple\_format** básicamente recibe como parámetro cualquier texto y le da formato de una manera muy simple a **HTML**. Toma el texto y reemplaza los saltos de línea (\n) por el tag **HTML** "< br />". Y cuando tenemos dos saltos de línea, uno atrás del otro, separa el texto con tags "< p>".

En Rails 2.1 este método recibe un parámetros adicional. Además del texto, podemos informarle que atributo **HTML** nos gustaria que el tag "< p>" incluyera. Veamos el ejemplo: 

	simple_format("Hello Mom!", :class => 'description')
	# => "<p class=’description’>Hello Mom!</p>"

Los atributos **HTML** serán agregados a todos los tags  "< p>" creados por este método.