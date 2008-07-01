## ActionView::Helpers::FormTagHelper

### submit\_tag

Se agregó la opción **:confirm** a los parámetros del método **#submit\_tag**. Esta opción funciona de la misma forma que el método **link_to**. Veamos un ejemplo: 

	submit_tag('Save changes', :confirm => "Are you sure?")