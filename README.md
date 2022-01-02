# gRPC

Microservices must exchange information and need to agree on :
	
	API to exchange data
	data format
	error patterns
	Load Balancing
	...

Choices for building api are :REST (HTTP-JSON), SOAP and gRPC!

API : 
	
	At its core, API is a contract 
	
	1. Send me this request (Client)

	2. Will send this response (Server)

What is gRPC?

	At a high level, it allows you to define request and response for the RPC (Remote procedure call) and handles all the rest for you.

	On top of it , it is modern,fast and efficient, 

		build on top of HTTP/2 , 

		low latency , 

		supports streaming, 

		language independent, 

		and makes it super easy to plug in authentication, 

		load balancing, 

		logging and monitoring.

RPC (Remote Procedure Call) : 

	In your client code, it looks like you are just calling a function directly on the server.


Client Code (any language) 																								Server Code (any other language)

{code}																													def createUser(User user){
...															RPC call(over the network)										{code}
Server.createUser(user)										 ------------------------>										...
...																														}
{code}																										



At the core of gRPC , you need to define the messages and service using Protocol Buffers

The rest of the gRPC code will be generated for you and you will have to provide an implementation for it.

one .proto file works for 12 programming languages (server and client) , allows you  to use a framework that scales to milllions of RPC per seconds.


# Protocol Buffers 

	Protocol Buffers are language agnostic

	Code can be generated for pretty much any language

	Data is binary and efficiently serialized (small payload)

	Very convenient for transportation of data

	Protocol Buffers allow for easy API evolution using rules


# Theory

	
	Protocol Buffers role in gRPC :

	 used to 

	 	1. define the messages (data, Request and response)

	 	2. Service (Service name and RPC endpoints)

	 payload size vs JSON :	

	 	JSON : 55 bytes 																						Protocol Buffers : 20 bytes 

	 	{																										{
	 		"age" : 35,																								int32 age = 1;
	 		"first_name" : "Stephane",																				string first_name = 2;
	 		"last_name" : "Maarek"																					string last_name = 3;
	 	}																										}

	 																											we save in network bandwith.

	 parsing JSON is CPU intensive (because format is human readable)											parsing Protocol Buffers (binary format) is less CPU intensive because it is closer to 
	 																											how a machine represents data


	gRPC languages : 

		GRPC-JAVA : Pure implementation in JAVA
		GPRC-GO : Pure implementation in GO
		GPRC-C : Pure implementation in C
			following have implementation in C:
			gRPC C++
			gRPC Python
			gRPC Ruby
			gRPC Objective C
			gRPC PHP
			gRPC C#

	https://grpc.io/


	# HTTP/2

	gRPC leverages HTTP/2 as backbone of communications

	Performance difference between HTTP/2 vs HTTP/1.1 => https://imagekit.io/demo/http2-vs-http1

	HTTP/2 is a new standard  for internet communications that addresses the common pitfall of HTTP/1.1 on modern web pages

	HTTP/1.1

		opens a new TCP connection to a server at each request

		does not compress the headers (plaintext)

		only works with request/response mechanism (no server push)

		HTTP was originally composed of two commands:

			GET : to ask for content 

			POST : to send content

		Nowadays , web pages loads 80 assets on average 

		Headers are sent at every request and are PLAINTEXT (heavy size)

		Each request opens a TCP connection

		These inefficiencies add latency and increase in packet size

	HTTP/2

		was released in 2015, and is battle tested

		supports multiplexing : 

			client and server can push messages in parallel over the same TCP connection

			greatly reduces latency

		supports server push

			servers can push streams (multiple messages) for one request from the client

		supports header compression

		is binary (efficient over the network)
		(Protocol buffer is a binary protocol and makes it a great match for HTTP/2)

		HTTP/2 is secure (SSL is not required but recommended by default)

	# Types of API in gRPC : 

		1. Unary (is what traditional api looks like HTTP REST)
		2. Server Streaming 
		3. Client Streaming
		4. Bi Directional Streaming

	# Scalability in gRPC :

		gRPC Servers are asynchronous by default

		This means they do not block threads by default

		Therefore each gRPC request server can serve millions of requests in parallel

		gRPC Client can be synchronous (blocking) or asynchoronous 

		client decides which model works best for the performance needs

		gRPC clients can perform client side load balancing

	# Security in gRPC

		By default, gRPC strongly advocates for you to use SSL (encryption over the wire) in your API

		This means that gRPC has security as its first class citizen

		Each language will provide an API to load gRPC with the required certificates and provide encryption capability out of the box.

		Additionally using interceptors, we can also provide authentication 

	# REST vs gRPC

		https://husobee.github.io/golang/rest/grpc/2016/05/28/golang-rest-v-grpc.html

		https://www.slideshare.net/borisovalex/grpc-vs-rest-let-the-battle-begin-81800634

		https://docs.microsoft.com/en-us/aspnet/core/grpc/comparison?view=aspnetcore-3.0


		GRPC 																														REST

		Protocol Buffers : smaller,faster																				JSON - text, slower,bigger

		HTTP/2 																											HTTP/1.1

		Bidirectional/async 																							Client=>Server requests only

		Stream Support 																									Request/Response support only

		API Oriented "What"																								CRUD oriented (POST, GET, PUT , DELETE)
		(no constraints -- free design) 


		Code generation through Protocol Buffers																		Code generation through OpenAPI/ Swagger (add-on)- 2nd class citizen
		in any language -- 1st class citizen

		RPC Based : gRPC does the plumbing for us 																		HTTP verbs based -- we have to write the plumbing or use a 3rd party library

		





# gRPC

Microservices must exchange information and need to agree on :
	
	API to exchange data
	data format
	error patterns
	Load Balancing
	...

Choices for building api are :REST (HTTP-JSON), SOAP and gRPC!

API : 
	
	At its core, API is a contract 
	
	1. Send me this request (Client)

	2. Will send this response (Server)

What is gRPC?

	At a high level, it allows you to define request and response for the RPC (Remote procedure call) and handles all the rest for you.

	On top of it , it is modern,fast and efficient, 

		build on top of HTTP/2 , 

		low latency , 

		supports streaming, 

		language independent, 

		and makes it super easy to plug in authentication, 

		load balancing, 

		logging and monitoring.

RPC (Remote Procedure Call) : 

	In your client code, it looks like you are just calling a function directly on the server.


	Client Code (any language) 																								Server Code (any other language)

	{code}																													def createUser(User user){
	...															RPC call(over the network)										{code}
	Server.createUser(user)										 ------------------------>										...
	...																														}
	{code}																										



At the core of gRPC , you need to define the messages and service using Protocol Buffers

The rest of the gRPC code will be generated for you and you will have to provide an implementation for it.

one .proto file works for 12 programming languages (server and client) , allows you  to use a framework that scales to milllions of RPC per seconds.


# Protocol Buffers 

	Protocol Buffers are language agnostic

	Code can be generated for pretty much any language

	Data is binary and efficiently serialized (small payload)

	Very convenient for transportation of data

	Protocol Buffers allow for easy API evolution using rules


# Theory

	
	Protocol Buffers role in gRPC :

	 used to 

	 	1. define the messages (data, Request and response)

	 	2. Service (Service name and RPC endpoints)

	 payload size vs JSON :	

	 	JSON : 55 bytes 																						Protocol Buffers : 20 bytes 

	 	{																										{
	 		"age" : 35,																								int32 age = 1;
	 		"first_name" : "Stephane",																				string first_name = 2;
	 		"last_name" : "Maarek"																					string last_name = 3;
	 	}																										}

	 																											we save in network bandwith.

	 parsing JSON is CPU intensive (because format is human readable)											parsing Protocol Buffers (binary format) is less CPU intensive because it is closer to 
	 																											how a machine represents data


	gRPC languages : 

		GRPC-JAVA : Pure implementation in JAVA
		GPRC-GO : Pure implementation in GO
		GPRC-C : Pure implementation in C
			following have implementation in C:
			gRPC C++
			gRPC Python
			gRPC Ruby
			gRPC Objective C
			gRPC PHP
			gRPC C#

	https://grpc.io/


	# HTTP/2

	gRPC leverages HTTP/2 as backbone of communications

	Performance difference between HTTP/2 vs HTTP/1.1 => https://imagekit.io/demo/http2-vs-http1

	HTTP/2 is a new standard  for internet communications that addresses the common pitfall of HTTP/1.1 on modern web pages

	HTTP/1.1

		opens a new TCP connection to a server at each request

		does not compress the headers (plaintext)

		only works with request/response mechanism (no server push)

		HTTP was originally composed of two commands:

			GET : to ask for content 

			POST : to send content

		Nowadays , web pages loads 80 assets on average 

		Headers are sent at every request and are PLAINTEXT (heavy size)

		Each request opens a TCP connection

		These inefficiencies add latency and increase in packet size

	HTTP/2

		was released in 2015, and is battle tested

		supports multiplexing : 

			client and server can push messages in parallel over the same TCP connection

			greatly reduces latency

		supports server push

			servers can push streams (multiple messages) for one request from the client

		supports header compression

		is binary (efficient over the network)
		(Protocol buffer is a binary protocol and makes it a great match for HTTP/2)

		HTTP/2 is secure (SSL is not required but recommended by default)

	# Types of API in gRPC : 

		1. Unary (is what traditional api looks like HTTP REST)
		2. Server Streaming 
		3. Client Streaming
		4. Bi Directional Streaming

	# Scalability in gRPC :

		gRPC Servers are asynchronous by default

		This means they do not block threads by default

		Therefore each gRPC request server can serve millions of requests in parallel

		gRPC Client can be synchronous (blocking) or asynchoronous 

		client decides which model works best for the performance needs

		gRPC clients can perform client side load balancing

	# Security in gRPC

		By default, gRPC strongly advocates for you to use SSL (encryption over the wire) in your API

		This means that gRPC has security as its first class citizen

		Each language will provide an API to load gRPC with the required certificates and provide encryption capability out of the box.

		Additionally using interceptors, we can also provide authentication 

	# REST vs gRPC

		https://husobee.github.io/golang/rest/grpc/2016/05/28/golang-rest-v-grpc.html

		https://www.slideshare.net/borisovalex/grpc-vs-rest-let-the-battle-begin-81800634

		https://docs.microsoft.com/en-us/aspnet/core/grpc/comparison?view=aspnetcore-3.0


		GRPC 																														REST

		Protocol Buffers : smaller,faster																				JSON - text, slower,bigger

		HTTP/2 																											HTTP/1.1

		Bidirectional/async 																							Client=>Server requests only

		Stream Support 																									Request/Response support only

		API Oriented "What"																								CRUD oriented (POST, GET, PUT , DELETE)
		(no constraints -- free design) 


		Code generation through Protocol Buffers																		Code generation through OpenAPI/ Swagger (add-on)- 2nd class citizen
		in any language -- 1st class citizen

		RPC Based : gRPC does the plumbing for us 																		HTTP verbs based -- we have to write the plumbing or use a 3rd party library
