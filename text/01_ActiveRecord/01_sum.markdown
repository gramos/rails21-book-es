<!-- -*- coding: utf-8; -*- -->

## El método **sum**

### Expresiones en el método **sum**

Ahora podemos usar expresiones en los métodos de cálculo de **ActiveRecord**, **sum**, por ejemplo:

        Person.sum("2 * age")

### Cambiando el valor de retorno por defecto del método sum

En las versiones previas, cuando usábamos el método **sum** de **ActiveRecord** para calcular la suma de una determinada columna para todos los registros de una tabla, si ningún registro correspondía con las condiciones expresadas en el método de invocación, entonces el valor de retorno por defecto era **nil**.

En Rails 2.1 el valor de retorno por defecto (cuando no se encuentra ningún registro) es 0. Vea el ejemplo:

        Account.sum(:balance, :conditions => '1 = 2') #=> 0
