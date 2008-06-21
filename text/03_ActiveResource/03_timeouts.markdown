<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Timeouts

ActiveResource usa **HTTP** para acceder a la API de RESTful y por esto es suceptible a problemas con servidores lentos o servidores no alcanzables. En algunos casos, las llamadas a  ActiveResource pueden expirar (timeout). Ahora ud. puede controlar el tiempo de expiración con la propiedad timeout.

        class Person < ActiveResource::Base
          self.site = "http://api.people.com:3000/"
          self.timeout = 5 # waits 5 seconds before expire
        end

En el ejemplo de arriba configuramos un timeout de 5 segundos. Se recomienda un valor pequeño para permitirle a su sistema una falla rápida, previeniendo que una casacada de fallas deje su servidor fuera de servicio.

Internamente, ActiveResource se basa la biblioteca Net:HTTP para hacer las peticiones HTTP. Cuando ud. define un valor por defecto para la propiedad timeout, el mismo valor es definido para la propiedad **read\_timeout** de la instancia del objeto Net:HTTP que está usando en ese momento.

El valor por defecto es 60 segundos.

