<!-- -*- mode: markdown; coding: utf-8; -*- -->

## action\_name

Para saber cual vista fue invocada durante la ejecución de su vista, podemos usar  el método **action\_name**:

        <%= action_name %>

El valor de retorno va a ser el mismo que usando **params[:action]**, pero de una forma más elegante.

