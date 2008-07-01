## ActionView::Helpers::FormHelper

### fields\_for form\_for con la opción index.

Los métodos **#fields\_for** y **form\_for** recibían la opción **:index**, eliminando la necesidad de utilizar **:index => nil** en cada objeto form. Mira los ejemplos:

Así es como solía ser el código antes:

	<% fields_for "project[task_attributes][]", task do |f| %>
	  <%= f.text_field :name, :index => nil %>
	  <%= f.hidden_field :id, :index => nil %>
	  <%= f.hidden_field :should_destroy, :index => nil %>
	<% end %>

Ahora luce de la siguiente forma:

	<% fields_for "project[task_attributes][]", task,
	              :index => nil do |f| %>
	  <%= f.text_field :name %>
	  <%= f.hidden_field :id %>
	  <%= f.hidden_field :should_destroy %>
	<% end %>