## ActionView::Helpers::DateHelper

Ahora todos estos métodos de módulo para trabajar con fechas (**date\_select**, **time\_select**, **select\_datetime**, etc.) aceptan opciones  **HTML**. Mira un ejemplo usando **date\_select**

	<%= date_select 'item','happening', :order => [:day], :class => 'foobar'%>
	
### date\_helper

El método **date\_helper** fue actualizado para que use **Date.current** en orden de definir su valor predeterminado.