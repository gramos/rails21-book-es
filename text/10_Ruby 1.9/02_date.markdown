##Nuevos métodos para la clase DateTime

Con el objetivo de mantener compatibilidad (duck-typing) con la clase **Time**, tres nuevos métodos fueron agregados a la clase **DateTime**. Los métodos son **#utc**, **#utc?** y **#utc\_offset**. veamos un ejemplo de cada uno:

	>> date = DateTime.civil(2005, 2, 21, 10, 11, 12, Rational(-6, 24))
	#=> Mon, 21 Feb 2005 10:11:12 -0600

	>> date.utc
	#=> Mon, 21 Feb 2005 16:11:12 +0000

	>> DateTime.civil(2005, 2, 21, 10, 11, 12, Rational(-6, 24)).utc?
	#=> false

	>> DateTime.civil(2005, 2, 21, 10, 11, 12, 0).utc?
	#=> true

	>> DateTime.civil(2005, 2, 21, 10, 11, 12, Rational(-6, 24)).utc_offset
	#=> -21600
