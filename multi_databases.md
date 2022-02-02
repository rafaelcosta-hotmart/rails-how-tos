[rails 6 reference](https://guides.rubyonrails.org/v6.0.0/active_record_multiple_databases.html)

model conection example:
```rb
#lib/klickpages/abstract_model

module Klickpages
  class AbstractModel < ActiveRecord::Base
    self.abstract_class = true

    establish_connection "kp_#{Rails.env}".to_sym
  end
end
```

```yml
#config/database.yml

default: &default
  adapter: mysql2
  encoding: utf8
  pool: 5
  username: root
  host: <%= ENV['DATABASE_HOST'] %>

development:
  <<: *default
  database: <%= ENV['DATABASE_NAME'] %>
  password: <%= ENV['DATABASE_PASSWORD'] %>

# Klickpages

kp_default: &kp_default
  adapter: mysql2
  encoding: utf8
  pool: 5
  username: root
  host: <%= ENV['DATABASE_KP_HOST'] %>
  reconnect: true

kp_development:
  <<: *kp_default
  password: <%= ENV['DATABASE_PASSWORD'] %>
  database: <%= ENV['DATABASE_KP_NAME'] %>
```

