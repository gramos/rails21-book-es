<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Protección contra Cross Site Scripting

En Rails 2.0 el archivo *application.rb* era así:

        class ApplicationController < ActionController::Base
          helper :all

          protect_from_forgery
        end

Vea la llamada al método  **protect\_from\_forgery**.

¿Escuchó hablar sobre Cross Site Scripting? Este es el nombre de una fallo de seguridad que se puede encontrar en la mayoría de los sitios y aplicaciones web que permiten a gente mala (estoy hablando de adolescentes que no tienen nada que hacer y tampoco tienen vida social) alterar el contenido de las páginas web, para llevar acabo 'fishing attacks', tomando el control del navegador a través de código javascript y en la mayoría de las veces forzando el usuario a ejecutar un el comando que ellos quieran. Este último tipo de ataque se llama 'cross-site request forgery'.

Cross Site Request Forgery es un tipo de ataque fuerza al usuario a ejecutar comandos si que este lo sepa. Y con el incremento del uso de ajax, las cosas empeoran.

Actualmente, este método es útil para asegurar que todos los formularios de tu aplicación están recibiendo datos que vienen de la misma aplicación, y no desde un link perdido en otro sitio. Esto se hace inlcuyendo un token basado en la sesión en todos los formularios y peticiones ajax generadas por Rails, y luego verificando la autenticidad de este token en el controlador.

Recuerder que las peticiones GET no están protegidas. Pero esto no es un problema si usamos sólamente para obtener datos, y nunca para alterar o guardar nada en nuestra base de datos.

Si ud. quiere aprender más acerca de CSRF (Cross-Site Request Forgery) vaya a la siguiente dirección:

* [http://www.nomedojogo.com/2008/01/14/como-um-garoto-chamado-samy-pode-derrubar-seu-site/isc.sans.org/diary.html?storyid=1750](http://www.nomedojogo.com/2008/01/14/como-um-garoto-chamado-samy-pode-derrubar-seu-site/isc.sans.org/diary.html?storyid=1750)

* [http://www.nomedojogo.com/2008/01/14/como-um-garoto-chamado-samy-pode-derrubar-seu-site/isc.sans.org/diary.html?storyid=1750](http://www.nomedojogo.com/2008/01/14/como-um-garoto-chamado-samy-pode-derrubar-seu-site/isc.sans.org/diary.html?storyid=1750)

Pero recuerde que esta no es una solución definitiva al problema, o como decimos comunmente, noes una bala de plata.


