<!-- -*- mode: markdown; coding: utf-8; -*- -->

## TimeZone

###  Definiendo un timezone por defecto

Se agregó una nueva opción al método **time\_zone\_select**, ahora ud. puede poner un valor por defecto en caso de el usuario no haya seleccionado ningún **TimeZone**, o cuando la columna en la base de datos es null. Para hacer esto, se creó la opción **:default** que se puede usar de la siguiente manera:

        time_zone_select("user", "time_zone", nil, :include_blank => true)

        time_zone_select("user", "time_zone", nil,
                :default => "Pacific Time (US & Canada)" )

        time_zone_select( "user", 'time_zone', TimeZone.us_zones,
                :default => "Pacific Time (US & Canada)")

En los casos dónde usemos la opción **:default**, debe aparecer con el **TimeZone** especificado ya selecionado.


### El método formatted_offset

Se incluyó el método **formatted\_offset** en las clases **Time** y **DateTime** para retornar con el formato **+HH:MM** la desviación de la hora UTC. Por ejemplo, en nuestro timezone (Hora Brasilia) el valor de desviación retornado por el método sería un string con el valor: **"-03:00"**.


Veamos algunos ejemplos:

Obteniendo la desviación desde un DateTime:

        datetime = DateTime.civil(2000, 1, 1, 0, 0, 0, Rational(-6, 24))
        datetime.formatted_offset         # => "-06:00"
        datetime.formatted_offset(false)  # => "-0600"

Ahora desde Time:

        Time.local(2000).formatted_offset         # => "-06:00"
        Time.local(2000).formatted_offset(false)  # => "-0600"

Note que este método retorna un **string**, el cual puede ser formateado o no dependiendo del valor dado como parámetro.

### El método with\_env\_tz

El método **with\_env\_tz** nos permite hacer tests con diferentes timezones de una manera muy simple:

        def test_local_offset
          with_env_tz 'US/Eastern' do
            assert_equal Rational(-5, 24), DateTime.local_offset
          end
          with_env_tz 'US/Central' do
            assert_equal Rational(-6, 24), DateTime.local_offset
          end
        end

Este helper

This helper was supposed to call **with\_timezone**, but it was renamed for **with\_env\_tz** to avoid confusion with the timezone informed by using **ENV['TZ']** and **Time.zone**.

### Time.zone_reset!

Se eliminó por que ya no se usa más.

### Time#in\_current\_time\_zone

Se modificó para que retorne **self** cuando **Time.zone** es null.

### Time#change\_time\_zone\_to\_current

Se modificó para que retorne **self** cuando **Time.zone** es null.

### TimeZone#now

El método **TimeZone#now** se modificó para que retorne un objeto **ActiveSupport::TimeWithZone** represetando la hora actual en el timezone configurado en **Time.zone**. Por ejemplo:

        Time.zone = 'Hawaii'  # => "Hawaii"
        Time.zone.now         # => Wed, 23 Jan 2008 20:24:27 HST -10:00

### Compare\_with\_coercion

Se creó el método **compare\_with\_coercion** (con un alias para <=>) en las clases **Time** y **DateTime**, posibilitando  la comparación cronológica entre las clases **Time**, **DateTime** y las instancias de **ActiveSupport::TimeWithZone**. Para una mejor comprensión, veamos los siguientes ejemplos:

        Time.utc(2000) <=> Time.utc(1999, 12, 31, 23, 59, 59, 999) # 1
        Time.utc(2000) <=> Time.utc(2000, 1, 1, 0, 0, 0) # 0
        Time.utc(2000) <=> Time.utc(2000, 1, 1, 0, 0, 0, 001)) # -1

        Time.utc(2000) <=> DateTime.civil(1999, 12, 31, 23, 59, 59) # 1
        Time.utc(2000) <=> DateTime.civil(2000, 1, 1, 0, 0, 0) # 0
        Time.utc(2000) <=> DateTime.civil(2000, 1, 1, 0, 0, 1)) # -1

        Time.utc(2000) <=> ActiveSupport::TimeWithZone.new(Time.utc(1999, 12, 31, 23, 59, 59) )
        Time.utc(2000) <=> ActiveSupport::TimeWithZone.new(Time.utc(2000, 1, 1, 0, 0, 0) )
        Time.utc(2000) <=> ActiveSupport::TimeWithZone.new(Time.utc(2000, 1, 1, 0, 0, 1) ))

### TimeWithZone#between?

Se incluyó el método **between?**  en la clase **TimeWithZone** para verificar si una instancia está entre dos fechas. Por ejemplo:

        @twz.between?(Time.utc(1999,12,31,23,59,59),
                      Time.utc(2000,1,1,0,0,1))

### TimeZone#parse

Este método crea una nueva instancia de **ActiveSupport::TimeWithZone** a partir de un string. Por ejemplo:

        Time.zone = "Hawaii"
        # => "Hawaii"
        Time.zone.parse('1999-12-31 14:00:00')
        # => Fri, 31 Dec 1999 14:00:00 HST -10:00


        Time.zone.now
        # => Fri, 31 Dec 1999 14:00:00 HST -10:00
        Time.zone.parse('22:30:00')
        # => Fri, 31 Dec 1999 22:30:00 HST -10:00

### TimeZone#at

Este método crea una nueva instancia de **ActiveSupport::TimeWithZone** a partir del número de segundos desde la fecha Unix epoch. Por ejemplo:

        Time.zone = "Hawaii" # => "Hawaii"
        Time.utc(2000).to_f  # => 946684800.0

        Time.zone.at(946684800.0)
        # => Fri, 31 Dec 1999 14:00:00 HST -10:00

### Más métodos

Los métodos **to\_a**, **to\_f**, **to\_i**, **httpdate**, **rfc2822**, **to\_yaml**, **to\_datetime** y  **eql?** se agregaron a la clase **TImeWithZone**.  Para más información acerca de estos métodos por favor lea la documentación de Rails.

### Se preparó la clase TimeWithZone para Ruby 1.9

En Ruby 1.9 tendremos algunos métodos nuevos en la clase **Time**, como por ejemplo:

        Time.now
        # => Thu Nov 03 18:58:25 CET 2005

        Time.now.sunday?
        # => false

Este mismo método existe para cada día de la semana

Otras cosa interesante es que el método **to\_s** del objeto **Time** tendrá un valor de retorno diferente. Hoy cuando ejecutamos  **Time.new.to\_s**, obtenemos lo siguiente:

        Time.new.to_s
        # => "Thu Oct 12 10:39:27 +0200 2006"

En Ruby 1.9 vamos a tener:

        Time.new.to_s
        # => "2006-10-12 10:39:24 +0200"

¿Que tiene que ver todo esto con Rails 2.1? Todo. Rails se está preparando para proveer estas modificaciones. La clase **TimeWithZone**, por ejemplo, sólo tuvo algunas mejoras para funcionar con los métodos del primer ejemplo.

