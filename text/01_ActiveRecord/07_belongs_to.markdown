<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Belongs_to

El método **belongs\_to** se cambió en pro de permitir el uso de **:dependent => :destroy** y **:delete**
en las asociaciones.

Por ejemplo:

        belongs_to :author_address
        belongs_to :author_address, :dependent => :destroy
        belongs_to :author_address_extra, :dependent => :delete,
                :class_name => "AuthorAddress"
