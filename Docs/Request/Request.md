Class: Request {#Request}
=========================

An XMLHttpRequest Wrapper.

### Implements:

[Chain](/Class/Class.Extras#Chain), [Events](/Class/Class.Extras#Events), [Options](/Class/Class.Extras#Options)

### Syntax:

	var myRequest = new Request([options]);

### Arguments:

2. options - (*object*, optional) See below.

###	Options:

* url        - (*string*: defaults to null) The URL to request.
* method     - (*string*: defaults to 'post') The HTTP method for the request, can be either 'post' or 'get'.
* data       - (*string*: defaults to '') The default data for [Request:send][], used when no data is given.
* async      - (*boolean*: defaults to true) If set to false, the requests will be synchronous and freeze the browser during request.
* encoding   - (*string*: defaults to "utf-8") The encoding to be set in the request header.
* autoCancel - (*boolean*: defaults to false) When set to true, automatically cancels the already running request if another one is sent. Otherwise, ignores any new calls while a request is in progress.
* headers    - (*object*) An object to use in order to set the request headers.
* isSuccess  - (*function*) Overrides the built-in isSuccess function.

Request Events: events {#Request:events}
----------------------------------------

### request

(*function*) Function to execute when the Request is sent.

#### Signature:

	onRequest(instance)

#### Arguments:

1. instance - (Request) The transport instance.

### success

(*function*) Function to execute when the Request completes.

#### Signature:

	onSuccess(responseText, responseXML)

#### Arguments:

1. responseText - (*string*) The returned text from the request.
2. responseXML  - (*mixed*) The response XML from the request.

### failure

(*function*) Function to execute when the request fails (error status code).

#### Signature:

	onFailure(instance)

#### Arguments:

instance - (Request) The transport instance.

### exception

(*function*) Function to execute when setting a request header fails.

#### Signature:

	onException(headerName, value)

#### Arguments:

1. headerName - (*string*) The name of the failing header.
2. value      - (*string*) The value of the failing header.

###	cancel

(*function*) Function to execute when a request has been cancelled.

#### Signature:

	onCancel()

### Properties:

* running  - (*boolean*) True if the request is running.
* response - (*object*) Object with text and XML as keys. You can access this property in the 'success' event.

### Returns:

* (*object*) A new Request instance.

### Example:

	var myRequest = new Request({method: 'get', url: 'http://site.com/requestHandler.php'}).send('name=john&lastname=dorian');

### See Also:

 - [Wikipedia: XMLHttpRequest](http://en.wikipedia.org/wiki/XMLHttpRequest)

Request Method: setHeader {#Request:setHeader}
--------------------------------------

Add or modify a header for the request. It will not override headers from the options.

###	Syntax:

	myRequest.setHeader(name, value);

###	Arguments:

1. name  - (*string*) The name for the header.
2. value - (*string*) The value to be assigned.

###	Returns:

* (*object*) This Request instance.

###	Example:

	var myRequest = new Request({url: 'getData.php', method: 'get', headers: {'X-Request': 'JSON'}});
	myRequest.setHeader('Last-Modified','Sat, 1 Jan 2005 05:00:00 GMT');

Request Method: getHeader {#Request:getHeader}
--------------------------------------

Returns the given response header or null if not found.

###	Syntax:

	myRequest.getHeader(name);

###	Arguments:

1. name - (*string*) The name of the header to retrieve the value of.

### Returns:

* (*string*) The value of the retrieved header.
* (*null*) `null` if the header is not found.

### Example:

	var myRequest = new Request(url, {method: 'get', headers: {'X-Request': 'JSON'}});
	var headers = myRequest.getHeader('X-Request'); //Returns 'JSON'.

Request Method: send {#Request:send}
----------------------------

Opens the Request connection and sends the provided data with the specified options.

###	Syntax:

	myRequest.send([options]);

###	Arguments:

1. options - (*object*, optional) The options for the sent Request.  Will also accept data as a query string for compatibility reasons.

###	Returns:

* (*object*) This Request instance.

###	Examples:

	var myRequest = new Request({url: 'http://localhost/some_url'}).send("save=username&name=John");

Request Method: cancel {#Request:cancel}
--------------------------------

Cancels the currently running request, if any.

###	Syntax:

	myRequest.cancel();

###	Returns:

* (*object*) This Request instance.

###	Example:

	var myRequest = new Request({url: 'mypage.html', method: 'get'}).send('some=data');
	myRequest.cancel();



Hash: Element.Properties {#Element-Properties}
==============================================

see [Element.Properties](/Element/Element/#Element-Properties)

Element Property: send {#Element-Properties:send}
-------------------------------------------------

### Setter

Sets a default Request instance for an Element.  This is useful when handling forms.

#### Syntax:

	el.set('send'[, options]);

#### Arguments:

1. options - (*object*) The Request options.

#### Returns:

* (*element*) The original element. 

#### Example:

	myForm.set('send', {url: 'contact.php', method: 'get'});
	myForm.send(); //Sends the form.

### Getter

Returns the previously set Request instance (or a new one with default options).

#### Syntax:

	el.get('send'[, options]);

#### Arguments:

1. options - (*object*, optional) The Request options.  If passed, this method will generate a new instance of the Request class.

### Returns:

* (*object*) The Request instance.

#### Example:

	el.get('send', {method: 'get'});
	el.send();
	el.get('send'); //Returns the Request instance.
	
Native: Element {#Element}
==========================

Custom Native to allow all of its methods to be used with any DOM element via the dollar function [$][].


Element Method: send {#Element:send}
------------------------------------

Sends a form or a container of inputs with an HTML request.

### Syntax:

	myElement.send(url);

### Arguments:

1. url - (*string*, optional) The url you want to send the form or the "container of inputs" to. If url is omitted, the action of the form will be used. url cannot be omitted for "container of inputs".

### Returns:

* (element) This Element.

### Example:

##### HTML

	<form id="myForm" action="submit.php">
		<p>
			<input name="email" value="bob@bob.com">
			<input name="zipCode" value="90210">
		</p>
	</form>

##### JavaScript

	$('myForm').send();

### Note:

* The URL is taken from the action attribute of the form.



[$]: /Element/Element/#dollar
[Request:send]: #Request:send