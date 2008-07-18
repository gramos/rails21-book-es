<!-- -*- mode: markdown; coding: utf-8; -*- -->

##Mime Types

Se arregló un bug que no permitía definir el atributo para **request.format** usando un símbolo. Ahora podemos usar el siguiente código:

        request.format = :iphone
        assert_equal :iphone, request.format
