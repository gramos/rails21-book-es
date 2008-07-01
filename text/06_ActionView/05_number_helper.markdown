## ActionView::Helpers::NumberHelper

### number\_to\_currency

El método **number\_to\_currency** ahora acepta la opción **:format** como parámetro, permitiéndonos dar formato al valor retornado. En versiones anteriores, cuando teníamos que dar formato a monedas locales, debíamos incluir un espacio antes de la opción **:unit** para que el formato retornado sea el correcto. Veamos un ejemplo: 
	
	# R$ es el símbolo de la moneda de Brasil.
	number_to_currency(9.99, :separator => ",", :delimiter => ".", :unit => "R$")
	# => "R$9,99″

	number_to_currency(9.99, :format => "%u %n", :separator => ",", 
		:delimiter => ".", :unit => "R$")
	# => "R$ 9,99″

Por otro lado, podemos personalizar de otras formas, por ejemplo:	

	number_to_currency(9.99, :format => "%n en reales brasileros", :separator => ",", 
		:delimiter => ".", :unit => "R$")
	# => "9,99 em reais"

Cuando creas tu cadena de formateo, se puedes especificar el siguiente parámetro: 

	%u Para la moneda
	%n Para el número