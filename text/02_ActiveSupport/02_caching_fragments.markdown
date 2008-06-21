<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Fragment\_exist?

Se agregaron dos nuevos métodos a  **cache\_store**: **fragment\_exist?** y **exist?**.

El método **fragment\_exist?** hace exactamente lo que ud. esperaría, verifica si un fragmento cacheado, informado a través de una clave existe. Básicamente sustituyendo al famoso:

        read_fragment(path).nil?

El método **exist?** se agregó a **cache\_store**, mientras que **fragment\_exist?** es un helper el cual ud. podría usar dentro de su controlador.

