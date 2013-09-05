!SLIDE subsection
# Runtime Support

!SLIDE smaller bullets incremental
# Java API for WebSocket

* Several containers pre-date JSR-356
* Jetty 7/8, Tomcat 7, GlassFish 3.x
* Much debate on the JSR-356 EG
* And all-new WebSocket implementations

!SLIDE smaller bullets incremental
# Relationshipt to Servlet Spec

* JSR-356 has no dependency on Servlets
* Still, built for and by Servlet containers
* Servlet 3.1 provides the upgrade hook WebSocket engines need
* `HttpServletRequest.upgrade(Class<?>)`

!SLIDE smaller bullets incremental
# Container Versions

* Tomcat 8 + backport to Tomcat 7
* Jetty 9 native API, `JSR-356` on top in Jetty 9.1
* Glassfish 4 
* All complete re-writes based on JSR-356

!SLIDE smaller bullets incremental
# JSR-356 API Details

* Two main options
* Extend abstract class `Endpoint`, or
* Use annotations `@ServerEndpoint`, `@ClientEndpoint`

!SLIDE smaller bullets incremental
# JSR-356 Server-Side Deployment

* Two main options
* Servlet container scans for annotated endpoints
* Programmatically deploy endpoints at startup via `WebSocketContainer`

!SLIDE smaller bullets incremental
# Spring Container Support for JSR-356

* Initialize endpoints through Spring container
* `ServerEndpointExporter` for `ServerEndpointRegistration` beans
* `SpringConfigurator.class` for use with `@ServerEndpoint`
* See Javadoc on respective classes

!SLIDE smaller bullets incremental
# JSR-356 Limitations

* No fallback options means no IE
* No sub-protocol support means hard to build real apps
* Can't consolidate HTTP and WebSocket request handling
* Built more for applications than as server foundation

!SLIDE smaller bullets incremental
# Why Sub-Protocol Support Matters

* Apps should aim to keep one socket per client
* One "main" pipeline for various messages
* Leads to 1 @ServerEndpoint per application
* Ideally class boundaries should be around functionality

!SLIDE center

"Using annotations and things is clearly in the vein of Spring and Hibernate and other popular Java libraries. When trying to build on top of it, though, I find myself wishing for an API more like Jetty 8, where I can just implement some interfaces and build my own abstractions on top of WebSocket."

[Comment](http://dev.eclipse.org/mhonarc/lists/jetty-users/msg03689.html) on jetty-users list









