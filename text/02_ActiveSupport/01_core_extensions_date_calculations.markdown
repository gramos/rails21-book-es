<!-- -*- mode: markdown; coding: utf-8; -*- -->

## ActiveSupport::CoreExtensions::Date::Calculations

### Time#end\_of\_day

Retorna la fecha actual con la hora fijada en 11:59:59 PM.

### Time#end\_of\_week

Retorna el fin de semana (Sunday 11:59:59 PM).

### Time#end\_of\_quarter

Retorna un objeto date representando el fin del trimestre. En otras palabras, retorna el último día de algunos de los siguientes meses: marzo, junio, septiembre o diciembre, dependiendo de la fecha actual.

### Time#end\_of\_year

Retorna 31 de Diciembre a las 11:59:59 PM.

### Time#in\_time\_zone

Este método es similar a  **Time#localtime**, excepto por el hecho de que usa **Time.zone** en vez de basarse en el timezone del sistema operativo. Se le puede pasar como parámetro tanto un objeto **TimeZone** como un **String**. Veamos algunos ejemplos:

        Time.zone = 'Hawaii'
        Time.utc(2000).in_time_zone
        # => Fri, 31 Dec 1999 14:00:00 HST -10:00

        Time.utc(2000).in_time_zone('Alaska')
        # => Fri, 31 Dec 1999 15:00:00 AKST -09:00

### Time#days\_in\_month

Se arregló un bug en el método **days\_in\_month**, el cual retornaba un número incorrecto de días en febrero cuando no se le especificaba el año.

El cambio consiste en usar el año actual como valor por defecto cuando no se le especifica el año en la llamada al método. Supongamos que estamos en un año bisiesto, veamos:

        Loading development environment (Rails 2.0.2)
        >> Time.days_in_month(2)
        => 28

        Loading development environment (Rails 2.1.0)
        >> Time.days_in_month(2)
        => 29

### DateTime#to_f

La clase **DateTime** tiene un nuevo método llamado **to_f** que retorna la fecha como un flotante representando el número de segundos desde  el Unix epoch (época unix, número de segundos desde el 1 de Enero de 1970 a la medianoche).

### Date.current

La clase **Date** tiene un nuevo método llamado **current** el cual se usa en vez de **Date.today**, por que este considera el timezone especificado en **config.time\_zone**, que en caso de que estar especificado retorna  **Time.zone.today**, de no ser así, entonces retorna **Date.today**.

