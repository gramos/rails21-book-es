## Timeouts

ActiveResource uses **HTTP** to access RESTful API's and because of that it is susceptible to problems with slow server responses or non-reachable servers. In some cases, calls to ActiveResource can expire (timeout). Now you can control the expiration time with the timeout property.

	class Person < ActiveResource::Base
	  self.site = "http://api.people.com:3000/"
	  self.timeout = 5 # waits 5 seconds before expire
	end

In this example above a timeout of 5 seconds was configured. A low value is recommended to allow your system to fail-fast, 
preventing cascading fails which could incapacitate your server.

Internally, ActiveResource shares resource from the Net:HTTP library to make HTTP requests. When you define a value for the timeout property, the same value is defined for the **read\_timeout** of the Net:HTTP object instance which is being used.

The default value is 60 seconds.
