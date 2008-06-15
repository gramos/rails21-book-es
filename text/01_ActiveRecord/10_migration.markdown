<!-- -*- mode: markdown; coding: utf-8; -*- -->

## Métodos add\_timestamps y remove\_timestamps

Ahora tenemos 2 métodos nuevos: **add\_timestamps** y **remove\_timestamps**. Los cuales agregan y eliminan, respectivamente, las columnas de **timestamp**. Veamos un ejemplo:

        def self.up
          add_timestamps :feeds
          add_timestamps :urls
        end

        def self.down
          remove_timestamps :urls
          remove_timestamps :feeds
        end
