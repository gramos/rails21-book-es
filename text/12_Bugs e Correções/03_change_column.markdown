<!-- -*- mode: markdown; coding: utf-8; -*- -->

##Bug fixes en change\_column

Se arregló un bug en el uso del método **change\_column** con **:null => true** en una columna creada usando **:null => false**. Debido a este bug no se realizó ningún cambio al usar este método.

