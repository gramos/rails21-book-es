<!-- -*- mode: markdown; coding: utf-8; -*- -->

##Eliminando los espacios en blanco con el método squish

Se agregaron dos métodos al objeto **String**, **squish** y **squish!**.

Estos métodos hacen lo mismo que el método **strip**. Elimina los espacios en blanco del principio y del fina de un texto. También elimina los espacios en blanco no utilizados (espacios en blanco consecutivos) en el medio de un texto.
Veamos un ejemplo:


        “    A    text    full    of     spaces    “.strip
        #=> “A    text    full    of     spaces”

        “    A    text    full    of     spaces    “.squish
        #=> “A text full of spaces”
