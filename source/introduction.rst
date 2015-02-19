Introduction
===============

Overview
---------

Shelloid is an open source IoT-ready real-time big data web application platform built using Node.js and Clojure that contains integrated stream query capability. Shelloid allows developers to easily integrate events from IoT sources such as the Nest thermostat by annotating functions with simple stream query specifications.

The following code illustrates this point

.. code-block:: javascript

	/**
	@stream.sdl select: ambient_temperature_f, name_long;
	            from: nest.thermostat;
	            where: ambient_temperature_f >= %threshold%
	@stream.init highTemperatureInit
	*/
	exports.highTemperature = function(data, stream, user){
	 console.log("highTemperature Data: ", data, 
				  " for user id ", user);
	}
	exports.highTemperatureInit = function(stream, done){
	 stream.setParams({threshold:80});
	 done();
	}


In the above code snippet the "highTemperature" function defines a real-time IoT data stream owing to its associated stream annotations. The "stream.sdl" (sdl stands for stream definition language) defines the stream characteristics in a syntax remindful of the SQL. The "stream.init" specifies an initialization function that is used to set the stream params. Shelloid will process the stream query in the background invoke the "highTemperature" function when the query condition holds true.

Shelloid stack is built using cutting-edge technologies such as Node.js (for the web tier), MongoDB (analytics DB), and Clojure (real-time stream computations). Real-time events from raw data can be generating using simple, declarative SQL-like stream queries. 

With its stream query annotations, Shelloid enables web applications to easily generate and process real-time events from IoT sources such as the Nest thermostat, Fitbit/Jawbone fitness bands, and many more. Our vision is to simplify the development of secure and robust IoT-enabled web applications and web services, improving programmer productivity and enabling quick time-to-market. 

Shelloid takes care of the infrastructure logic and lets you focus on your business logic, leading to quick time to market for your business-critical applications. Shelloid is open sourced under LGPL license, allowing you to run your commercial closed source applications on the top of it.


Node - Clojure integration
--------------------------

Shelloid attempts to bring out the best of two cool modern programming platforms: Node.js and Clojure. Node.js is great for web and real-time. Clojure is great for concurrent computations. So, why not let the Node.js handle the web requests and real-time messaging and use Clojure when there is a heavy computation at hand? Shelloid does just that.

Shelloid is essentially a Node.js web application server with integrated Clojure-based compute service which runs as a separate process. Shelloid takes care of all the integration details. While the Clojure compute service is executing a heavy computation, Node.js event loop is freed up to process other requests.

The following code snippet illustrates how the integration works. In the code, we define a compute service named add in Clojure. From Node.js this service is invoked by calling sh.ccs.add function (sh stands for shelloid, ccs for Clojure compute service). This results in parameters being passed to the CCS process and the Clojure add service function being executed. The result of the Clojure function is passed back to Node.js and the callback is invoked with err message if any and the result value. After passing off the computation to the Clojure, Node.js event loop is freed up to execute other requests.

Node.js 

.. code-block:: javascript

	sh.ccs.add(100, 200, function(err, r){
	console.log("Result: " + r);
	});


Clojure

.. code-block:: clojure

	(service add [a b]
		(+ a b)
	)

Clojure compute service (CCS) requires `Leiningen <http://leiningen.org>`_ to be installed somewhere in the system path.

Please Note: More documentation is on the way. Please bear with us for couple of weeks!

Open, extensible architecture
-----------------------------

Shelloid has an open, extensible architecture. While open sourcing is great for the users, Shelloid goes beyond merely being open source. Shelloid has a open architecture created from ground up, allowing you to easily write extensions that can modify the behaviour of the engine to suit your needs. Many of Shelloid's  built-in features are themselves built as extensions, leading to a relatively small and robust core.

Our vision is to simplify the development of secure and robust web applications and services, improving programmer productivity and enabling quick time-to-market. Shelloid takes care of the infrastructure logic and lets you focus on your business logic, leading to quick time to market for your business-critical applications. Shelloid is open sourced under LGPL license, allowing you to run your commercial closed source applications on the top of it.


Key features
-------------

* Integrated Clojure compute service.
* Use of declarative annotations instead of writing code for many useful functions.
* Configurable automatic restarting of the server in case of changes to the application code or unrecoverable errors.
* Built in authentication (via passport.js) - requires only a single authentication function to be written.
* Currently supports local authentication as well as Google, Facebook, Twitter authentications out of the box.
* Built-in login session management.
* Built-in role-based access control with roles attached to controllers via annotations.
* Custom authentication, e.g, for API implementations that is attached to routes via annotations.
* Supports specification-based verification of API requests/responses. Simple API specification which is automatically checked against requests for enhanced security, robustness. The application code will be cleaner owing to lesser checks required.
* Built in cluster support by setting a single configuration flag. Built-in logging with cluster support.
* Simplified DB API with built-in connection pooling.
* Named SQL query strings can be declared as annotations and executed using the name.
* Built-in simulator for controlled functional testing of the application/controller logic (work in progress). Simulator will allow specification and verification of temporal properties, controlled flow of time, etc.
* Support for easily configurable UI themes.
* UI themes can be associated with domains, i.e., depending on the domain by which the site is accessed a separate set of files/views can be served. Note that, at the moment, controllers are shared across domains. This results in a limited support for virtual hosting.
* Built in proper error and exception handling that takes care of sending error responses and freeing DB connections.
* Built in simple and versatile sequencing API that avoids callback hell and results in readily understandable code.
* Simple config specification for allowing cross-origin requests (implementation complying with CORS standard).
* Auto detection of the current node of execution based on specified node names to IP/hostname mapping - useful for distributed and cloud deployments.
* And, more being added every day!
