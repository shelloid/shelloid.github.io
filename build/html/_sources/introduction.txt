Introduction
===============

Overview
---------

Shelloid is an open source web application server for Node.js that aims at making Node.js web application development simple and secure. It takes care of the infrastructure logic and lets you focus on your business logic, leading to quick time to market for your business-critical applications. It is open sourced under LGPL license, allowing you to run your commercial closed source applications on the top of it.

In order to improve programmer productivity and make your code readable, maintainable, and secure, Shelloid employs the following foundational principles:

1. Convention over configuration.
2. Declarative over procedural.
3. Separation of concerns.
4. Secure defaults.


Key features
-------------

* Use of declarative annotations instead of writing code for many useful functions.
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
* Built in proper error and exception handling that takes care of sending error responses and freeing DB connections.
* Built in simple and versatile sequencing API that avoids callback hell and results in readily understandable code.
* Simple config specification for allowing cross-origin requests (implementation complying with CORS standard).
* Auto detection of the current node of execution based on specified node names to IP/hostname mapping - useful for distributed and cloud deployments.
* And, more being added every day!
