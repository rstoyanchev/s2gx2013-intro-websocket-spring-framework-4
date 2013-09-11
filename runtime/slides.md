!SLIDE subsection
# Runtime Support

!SLIDE smaller bullets incremental
# The Java API for WebSocket
<br><br>
* Several Servlet containers pre-date JSR-356
* Jetty 7/8, Tomcat 7, GlassFish 3.x
* Much debate on JSR-356 EG
* All-new WebSocket implementations

!SLIDE smaller bullets incremental
# Relationship to Servlet Spec
<br><br>
* JSR-356 has no dependency on Servlet spec
* Nevertheless built for and by Servlet containers
* Servlet 3.1 provides a hook for upgrading:<br>`HttpServletRequest.upgrade(Class<?>)`
* SCI scan used also in Servlet containers

!SLIDE smaller bullets incremental
# Servlet Container Versions

* Tomcat 8 (currently RC1)-<br>expect RC2 soon and also backport to Tomcat 7
* Jetty 9 already has native WebSocket API-<br>Jetty 9.1 will add `JSR-356`
* Glassfish 4 with Tyrus WebSocket engine
* More containers to follow

!SLIDE smaller bullets incremental
# The JSR-356 API
<br><br>
* Two main options
* Extend abstract class `Endpoint`, or
* Use annotated endpoints via<br> `@ServerEndpoint`, `@ClientEndpoint`

!SLIDE smaller bullets incremental
# Server-Side Deployment
## _(JSR-356)_
<br><br>
* Also two main options
* Servlet container scan for annotated endpoints
* Programmatic deployment at startup<br> via `WebSocketContainer`

!SLIDE smaller bullets incremental
# JSR-356 in Spring Apps
<br><br>
* Create endpoints through Spring container
* [`ServerEndpointExporter`](http://docs.spring.io/spring/docs/4.0.0.BUILD-SNAPSHOT/javadoc-api/org/springframework/web/socket/server/endpoint/ServerEndpointExporter.html) deploys beans of type<br>[`ServerEndpointRegistration`](http://docs.spring.io/spring/docs/4.0.0.BUILD-SNAPSHOT/javadoc-api/org/springframework/web/socket/server/endpoint/ServerEndpointExporter.html)
* [`SpringConfigurator`](http://docs.spring.io/spring/docs/4.0.0.BUILD-SNAPSHOT/javadoc-api/org/springframework/web/socket/server/endpoint/SpringConfigurator.html) can be referenced<br>via `@ServerEndpoint` attribute
* Check Javadoc of these classes

!SLIDE smaller bullets incremental
# JSR-356 Limitations

* No fallback options (no IE)
* No sub-protocol support, hard to build real apps
* No way to [handle HTTP and WebSocket requests](https://java.net/jira/browse/WEBSOCKET_SPEC-211)<br>from one place (i.e. "front controller" pattern)
* Resembles application framework<br>rather than remain flexible for frameworks to build on

!SLIDE smaller bullets incremental
# Why Frameworks Matter?

* If you maintain one WebSocket per client
* i.e. one pipeline for all messages
* You end up with single `@ServerEndpoint` per application
* This is too rudimentary
* Much like Servlet vs Web framework

!SLIDE center

"Using annotations and things is clearly in the vein of Spring and Hibernate and other popular Java libraries. When trying to build on top of it, though, I find myself wishing for an API more like Jetty 8, where I can just implement some interfaces and build my own abstractions on top of WebSocket."

[Comment](http://dev.eclipse.org/mhonarc/lists/jetty-users/msg03689.html) on jetty-users mailing list









