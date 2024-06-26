# Web Technologies


###  What is HTTP

HTTP is a protocol for fetching resources such as HTML documents.
It is the foundation of any data exchange on the Web and it is a client-server protocol, 
which means requests are initiated by the recipient, usually the Web browser.

Clients and servers communicate by exchanging individual messages. 
The messages sent by the client, usually a Web browser, are called **requests** and the messages sent by the server as an answer are called **responses.**


###  Difference HTTP / HTTPS

  - HTTP insecure connection  Port: 80
   
  - HTTPS secure connection. SSL level, SSL sertificate  Port: 443


### What is long polling 

long polling is a push-based approach that allows the server to send updates to the client as soon as they are available. 
Here's how it works:

 - The client initiates a request to the server, typically through an HTTP request.

 - Instead of immediately responding, the server holds the request open, keeping the connection active.
   HTTP timeouts are tunable using the Keep-Alive header. Long polling takes advantage of that by setting 
   a very long or indefinite timeout period, so the request stays open even though the server doesn’t have an immediate response.

 - If no new data is available, the server waits until it has something to send back.

 - Once the server has new data or a predefined timeout occurs, it responds to the client with the latest information.

 - Upon receiving the response, the client immediately sends another request to the server to maintain the connection.

This cycle of sending requests and receiving responses continues, ensuring real-time updates.

 **Contra:** Inefficient and slow: Modern realtime protocols, such as WebSocket, incur much less overhead than long polling.

###  Server-sent events (SSE)

Instead of the browser continuously polling the server on the off chance there’s new information, 
Server-Sent Events (SSEs) enable the server to push data to the browser as soon as there’s new information available. 

It’s helpful to remember that while some apps need bidirectional, many do not - most apps out there are mainly read apps. 
For situations like the ones above where you mostly need to send updates one-way from the server to the client only, 
SSEs provide a much more convenient (equally efficient) way to push updates based on HTTP.

###  Open Systems Interconnection model(OSI)

provides a common basis for the coordination of standards development for the purpose of systems interconnection.

Layers:

 - Application level, End user layer(http, ftp, dns, ssh, tls/ssl)

 - Presentation layer, syntax layer(ssl, mpeg, jpeg)

 - Session layer, sync and send to port

 - Transport layer, end to end connections ( tcp, udp)

 - Network layer, packets (ip, icmp)

 - Data Link (ethernet, switch, bridge)

 - Physical (coax, fiber , wireless)


###  HTTP request consists of
   
 - **Method:** (GET/POST/PUT/DELETE...)
  
 - **Path:** The path of the resource to fetch; the URL of the resource stripped from elements that are obvious from the context, 
 		     for example without the protocol (http://), the domain (developer.mozilla.org), or the TCP port (80).

 - **Version** of the protocol: HTTP 1.1

 - **Headers**
   
 - **Body**


	```
	[Method]    [Path]           [Version]
	POST   /home/user/datafile   HTTP/1.1

	[Headers]
	From: user@linode33
	User-Agent: Mytools/0.8.0
	Content-Type: application/json
	Content-Length: 32
	
	[Body]
	{
		[Json-formatted data pairs]
	}
	```

 
###  HTTP response consists of

 - The **version** of the HTTP protocol they follow

 - A status **code**, indicating if the request was successful or not, and why

 - A status **message**, a non-authoritative short description of the status code

 - **HTTP headers**, like those for requests

 - **body** containing the fetched resource, optionally

	```
	[Version]    [Code]   [Message]
	HTTP/1.1      200         OK

	[Headers]
	Date: Mon, 27 Jul 2009 12:28:53 GMT
	Server: Apache/2.2.14 (Win32)
	Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
	Content-Length: 88
	Content-Type: text/html
	Connection: Closed

	[body]
	<html>
		<body>
			<h1>Hello, World!</h1>
		</body>
	</html>
	```

###  HEAD Method

HEAD is almost identical to GET, but without the response body.

In other words, if GET /users returns a list of users, then HEAD /users will make the same request but will not return the list of users.

A HEAD request is useful for checking what a GET request will return before actually making a GET request - 
a HEAD request can read the Content-Length header to check the size of the file, without actually downloading the file.


###  GET Method

GET is used to **request data** from a specified resource. Note that the query string (name/value pairs) is sent in the URL of a GET request:

	``` /test/demo_form.php?name1=value1&name2=value2 ```

**Some notes on GET requests:**

 - can be cached

 - remain in the browser history

 - can be bookmarked

 - should never be used when dealing with sensitive data

 - have length restrictions (maximum URL length is 2048 characters)

 - are only used to request data (not modify)

 - body only in response


###  POST Method

POST is used to send data to a server to **create/update** a resource. The data sent to the server with POST is stored in the request body of the HTTP request:

	```
	POST /test/demo_form.php HTTP/1.1
	Host: w3schools.com

	name1=value1&name2=value2
	```

**Some notes on POST requests:**

 - are never cached
 
 - do not remain in the browser history

 - cannot be bookmarked

 - have no restrictions on data length

 - type of the content inside body is written in  [Content-Type] header

 - CRUD[create/read/update/delete] is CREATE


###  PUT Method

PUT is used to send data to a server to **create/update** a resource.

The difference between POST and PUT is that **PUT requests are idempotent** => calling the same PUT request multiple times 
will always produce **the same result**. CRUD is UPDATE.

In contrast, calling a POST request repeatedly have side effects of creating the same resource multiple times.


###  DELETE Method

The DELETE method deletes the specified resource:

	```
    DELETE /text.txt HTTP/1.1  
	Host: example.com    
	
	Response: HTTP/1.1 200 OK  
	Content-Type: text/plain; charset=UTF-8

	```

###  PATCH Method

Similar to PUT, is used to apply partial modifications to a resource.


###  CONNECT Method

The CONNECT method is used to start a two-way communications (a tunnel) with the requested resource.
Often used to get access to resource wich is using SSL(HTTPS).


###  TRACE Method

The TRACE method is used to perform a message loop-back test that tests the path for the target resource (useful for debugging purposes).

	```
	Request: TRACE / HTTP/1.1  
	Host: example.com    
	
	Response: HTTP/1.1 200 OK   
	Content-Type: message/http
	```

###  OPTIONS Method 


The OPTIONS method describes the communication options and methods for the target resource.

In response should header [Allow] with all server methods:

	```
    HTTP/1.1 200 OK   
	[header Allow]: OPTIONS, GET, HEAD, POST, PUT, PATCH, DELETE, TRACE
	
	```

###  HTTP Header

The HTTP headers are used to pass additional information between the clients and the server through the request and response header. 

All the headers are case-insensitive, headers fields are separated by colon, key-value pairs in clear-text string format. 

**Categories:**

 - Authorization headers

 - Caching headers

 - Client hints 

 - Conditionals headers

 - Connection management 

 - Cookies 

 - CORS

 - Message body information 

 - Redirects 

 - Security 

 and others...


###  HTTP response status codes

HTTP response status codes indicate whether a specific HTTP request has been successfully completed. 

Responses are grouped in five classes(for ex: most usable):

 - **Informational** responses (100 – 199)

 - **Successful** responses (200 – 299) : 200-OK 

 - **Redirection** messages (300 – 399) : 304-Not Modified
 
 - **Client error** responses (400 – 499) : 400-Bad Request, 401-Unauthorized, 403-Forbidden, 404-Not Found

 - **Server error** responses (500 – 599) : 500-Internal Server Error, 501-Not Implemented, 503-Service Unavailable


###  What is http cookie
  
Store the state on client side. Small data which were send by server and storied on client side.

Later on each server request client(browser) will send these cookies to server.

Each domain has each own cookies. SERVER: send header Set-Cookie (expire, path domain, https only)


###  secure and HttpOnly cookies 

 1. Server send header:  [Set-Cookie]: token=123abc
  
 2. Client(Browser) saves in  Cookie Storage
   
 3. Next browser request to server it will send cookie in header [Cookie]

Parameter [secure]: cookie can be send only via HTTPS. Do NOT add any secure mechanism to it.

Now in most of the browser it do not allowed to send secure cookies via HTTP

Parameter [httpOnly]: cannot read this cookie from JS.  Just only for server.
For session server cookie for example.

https://habr.com/ru/articles/710578/  2024

https://habr.com/ru/companies/avito/articles/710674/  2023


###  Diff between: feature-detection | feature-inference | user-agent

All three needed to determine the user's browser possiblities
  
  - feature-detection: check for browser support of the feature
    
     ```
     if ('geolocation' in navigator) {
         // can use navigator.geolocation
     } else {
         // analog / polyfill
     }
     ```

  - feature-inference (suppose of possibility)
      ```
      if (document.getElementsByTagName) {
            element = document.getElementById(id);
      }
      ```

  - user-agent.  Check via navigator.userAgent


###  What is API

API (Application programming interface) — its contract to know to how to communicate with the app(programm)
 
API — its a set of methods, constants, properties....


###  REST API

REpresentational State Transfer. 

Its approach(or architectical style) to create web application API and how simply and standtartized communicate between client and server, via request and response. 
Or set ot rules how effectively communicate via http protocol between client and server.
Think about which resources server wants to open for clients.


 Main concepts:
  
 - Communication between server and clients. and it should be simple, standtartized API, for ex:

   ```
	Add new product:   POST       =>  ./server/products
	Delete product:    DELETE     =>  ./server/products
	Update product:    PUT/PATCH  =>  ./server/products
	GET all products:  GET        =>  ./server/products
	Get exact product: GET        =>  ./server/products/{id}

   ```

 - System can be multilevel on server side (with load balancing or several nodes etc...) and be Scalable

 - Server should work with high performance 
 
 - Stateless(think that each request from client is its first request), means that **client should send all needed information**

 - Caching.  GET requests should be cached.

 - In most cases format of the data in communication between server-client (json or xml)

 - API should be versioned =>   ./server/v2/newproducts

So, its the set of recomendations.

  https://systems.education/what-is-rest    https://skillbox.ru/media/code/rest-api-chto-eto-takoe-i-kak-rabotaet/ 2022


###  What is Open API and Swagger

API specification: **Open API** (status codes, endpoints, server errors, input query parameters...)

OpenAPI specification (previously known as Swagger specification) describes a standard format for REST APIs. 

This standard is important so that everyone who writes REST APIs is compliant with its best practices such as the versioning, 

safety, and error handling. We can say that OpenAPI is similar to a template with a set of rules and constraints explaining 

how you could describe an API. It is usually written in YAML or JSON file format making it readable for humans and machines.  

Open API - **is a specification**

Swagger - is a set of open-source **tools** built to help programmers develop, design, document, and use REST APIs 
The tool is built around the OpenAPI specification and contains three components: Swagger Editor, Swagger UI, and Swagger Codegen.


###  SOAP

Its a protocol for communication of the structured messages with the XML or SOAP XML.

SOAP can use several protocols to communicate: SMTP, FTP, HTTP.

For describing SOAP services wsdl(web service description language) is used (xml-based)

SOAP message is determined:  
envelope : root element
  header : similar to http headers, additional information
  body   : data  
 [error} : 

SOAP is a protocol with the structure.


### RPC(Remote procedure call)

Client - Client Stub -> Network - Server Stub - Server

 - gRPC: Framework(platform) form Google, invented at 2015. Very popular in Microservice architecture.
	    
	Pro: Http 2.0(binary format)
	     Data streaming
		 Using of binaty format(protobuf) instead of json
		 protoc files from which we can generate files for different program languages


 - TRPC (Typesafe RPC)



###  What is CDN 

CDN(content delivery network) - distributed network of proxy servers and their data centers.

Send data to user from the closiest server. The goal is to provide high availability and performance by distributing 

the service spatially relative to end users. CDN nodes are usually deployed in multiple locations, often over multiple Internet backbones. 

Benefits include reducing bandwidth costs, improving page load times, and increasing the global availability of content.


###  GraphQL 

Is a language of requests. Request from client only needed info.

- in classic approach server determine schema and format of the data which it return to client

- GraphQL: server determne schema, but client requests ONLY needed data


GraphQL has two types of requests:

 - query (get)

 - mutation (post)

 - Subscription (real time data change)


###  Contract First API approach

The contract first approach is a way of designing and **developing API's starting from a contract.** 
Using the openAPI convention you can design your API and share it with your consumers and developers. 

This approach has the following advantages:

- Easy integration: Your developers and your consumers get used to the same contract to build their software so the integration will be very smooth.

- Easy alignment and discussions: All the discussion that happens around the API with the consumers will be based on the contract, using tools like Swagger 
editor will give a nice rendering of the contract and make it easy to enrich it. 

- Versioning: The contract will have a version and this will ensure an easy evolvement of your API. 


###  Code First API approach

A code-first approach typically involves coding an API from business requirements and then generating a machine-readable API definition from that code. 

It can also mean implementing the API in code and then creating an API description using comments or annotations or even manually writing a description from scratch.

Pro:

- Contract can be easely generated from the existing code

Contra: 

- Work cannot be done in parallel between teams


###  Design First In API Approach

API design-first means you describe every API design in an iterative way that both humans and computers can understand—before you write any code. 

With an API design-first approach, every team speaks the same language, and every tool they use leverages the same API design.


###  HATEOAS in REST API

HATEOAS stands for Hypermedia as the Engine of Application State and it is a component of RESTful API architecture and design. 

With the use of HATEOAS, the client-side needs minimal knowledge about how to interact with a server. 

This is made possible by the network application responding to the client’s requests with dynamically generated information through the use of hypermedia.

Server will return the needed data AND actions (links to actions) which can be done to this data.


###  Flash of Unstyled Content
  
Web page appears briefly with the browser's default styles prior to loading an external CSS stylesheet, 
due to the web browser engine rendering the page before all information is retrieved.

Need to change of font styles from default to other one.
  
  - critical.sss
  
  - show preload before data will be loaded

https://uchet-jkh.ru/i/cto-takoe-fout-c-i-kak-ego-ispravit/


### Web Sockets 

Protocol with the constant connection. So called broadcast of the messages.
There is no need to as server peridically('do you something for me?' like in http request-response.)
You only need to open connection and wait for message from server.

    ```
    const myWS = new WebSocket(url, protocols);   ws://just-test.com
    onopen |  onmessage |  onclose | onerror
    
    ````
   
https://habr.com/ru/sandbox/171066/


###  What is Content Security Policy(CSP) 

Mechanism of the secure use of the website and webapps. Decrease risks of XSS attacks or injections.

Add http header "Content-Security-Policy"  with the white list of websites(or single page) who can access current site.

https://blog.skillfactory.ru/glossary/csp/ [2023]
https://habr.com/ru/articles/757332/ [2023]    
https://habr.com/ru/companies/nix/articles/271575/ [2015]


###  What is XSS(Cross-Site Scripting) 

 - hacker injects malicious JS code to your page

 - this code will be called and run each time the user enters your webpage
  
 - maliscious script can pass user data to hacker back

https://habr.com/ru/articles/511318/ [2020] 
https://blog.skillfactory.ru/glossary/xss/ [2023]




### Same Origin Policy

How the document from one origin can communicate with the other origin.
Using headers and CORS.

### What is  CORS ( CROSS Origin requests)
    
API can get resources only from the same domain.
Http headers which allow access to resources from other domain.


