<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Usando el email como nombre de usuario.

Algunos servicioes usan el e-mail como nombre de usuario, lo cual nos obliga a usar una URL como la siguiente:

        http://ernesto.jimenez@negonation.com:pass@tractis.com

Pero nos genera un problema. Por que tenemos dos (@), el intérprete se pierde cuando lee algo como esto. Por este motivo, Se exntendió **ActiveResource** un poco más, con el fin de facilitar el uso de e-emails para la autenticación. Ahora ud. puede hacer lo siguiente:

        class Person < ActiveResource::Base
          self.site = "http://tractis.com"
          self.user = "ernesto.jimenez@negonation.com"
          self.password = "pass"
        end
