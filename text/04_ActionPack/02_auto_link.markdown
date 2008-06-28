<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Auto Link

El método  **auto\_link** recibe cualquier texto como parámetro, y si el texto contiene alguna dirección de email o website, retorna el mismo texto, pero con hyperlinks.

Por ejemplo:

        auto_link("Go to this website now: http://www.rubyonrails.com")
        # => Go to this website now: http://www.rubyonrails.com

Algunos sites, como Amazon, usan el símbolo "=" en sus URL. Este método no reconoce este símbolo. Veamos como se comporta este método en tal caso:

        auto_link("http://www.amazon.com/Testing/ref=pd_bbs_sr_1")
        # => http://www.amazon.com/Testing/ref

Note que el método corta el hyperlink exactamente antes del símbolo "=", antes de Rails 2.1 este símbolo estaba soportado.

El mismo método se actualizó para permitir el uso de URL con paréntesis.

Un ejemplo de URL coc paréntesis:

        http://en.wikipedia.org/wiki/Sprite_(computer_graphics)
