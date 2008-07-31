<!-- -*- mode: markdown; coding: utf-8; -*- -->

## ActionController::Caching::Sweeping

En las primeras versiones de Rails, cuando declarábamos un **sweeper**, teníamos que informar la clase usando símbolos:

        class ListsController < ApplicationController
          caches_action :index, :show, :public, :feed
          cache_sweeper :list_sweeper,
                        :only => [ :edit, :destroy, :share ]
        end


Ahora es posible declarar explícitamente una clase en vez de usar un símbolo. Esto es necesario si ud. quiere que el  **sweeper** esté dentro de un módulo. Además de poder seguir usando símbolos para los demás casos, a partir de ahora puede hacer así:

        class ListsController < ApplicationController
          caches_action :index, :show, :public, :feed
          cache_sweeper OpenBar::Sweeper,
                        :only => [ :edit, :destroy, :share ]
        end