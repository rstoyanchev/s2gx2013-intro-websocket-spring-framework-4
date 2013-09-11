!SLIDE subsection
# SockJS Support

!SLIDE small bullets incremental
# [SockJS](https://github.com/sockjs/sockjs-client) in a Nutshell
<br><br>
* Emulate WebSocket API as close as possible
* At least one streaming protocol per major browser
* Cross-domain and cookie support
* Polling in old browsers, hosts behind restrictive proxies
* No Flash inside

!SLIDE center
## SockJS Transports by Browser

![Table with SockJS transports by browser](transports.png)

!SLIDE smaller
# Configure SockJS

    @@@ java

    @Configuration
    @EnableWebSocket
    public class WebSocketConfig implements WebSocketConfigurer {


      @Override
      public void registerWebSocketHandlers(
          WebSocketHandlerRegistry registry) {

        WebSocketHandler echoHandler = new EchoHandler();
        registry.addHandler(echoHandler, "/echo").withSockJS();
      }

    }

!SLIDE smaller
# `WebSocketHandler`
## (remains unchanged)

    @@@ java

    public class EchoHandler extends TextWebSocketHandlerAdapter {

      @Override
      public void handleTextMessage(WebSocketSession session,
          TextMessage message) throws Exception {

        session.sendMessage(message);
      }

    }

!SLIDE small bullets incremental
# SockJS client

    @@@ javascript

      var ws = new SockJS("ws://localhost:8080/echo");

      ws.onopen = function (event) {
        // ...
      };

      ws.onmessage = function (event) {
        // ...
      };

      ws.onclose = function (event) {
        // ...
      };

!SLIDE center
![Chrome browser with SockJS network activity](sockjs-demo.png)

!SLIDE small bullets incremental
# The SockJS Protocol

* Defines URL scheme
* Provided in the form of a readable [test suite](http://sockjs.github.io/sockjs-protocol/sockjs-protocol-0.3.3.html)
* [Wide support](https://github.com/sockjs/sockjs-client) across languages

!SLIDE small bullets incremental
# The SockJS URL Scheme
<br><br><br>
        GET  /echo

        GET  /echo/info

        POST /echo/<server>/<session>/<transport>

!SLIDE small
# Example SockJS Requests
<br><br><br>

        GET /echo/info

        POST /echo/375/5rzpg08l/xhr_streaming

        POST /echo/375/5rzpg08l/xhr_send
        POST /echo/375/5rzpg08l/xhr_send

!SLIDE small bullets incremental
# Runtime Support

* Any Servlet 3.0 container
* Even without WebSocket support!
* No hard dependency on Servlet API
* Experimental Netty support

!SLIDE smaller bullets incremental
# Client Disconnects

* Servlet 3 containers don't detect clients going away
* `SockJsService` however sends periodic heartbeats
* A failure to send a message closes the session
* Check [SERVLET_SPEC-44](https://java.net/jira/browse/SERVLET_SPEC-44) (vote please)<br> and also [related discussion](http://markmail.org/message/yhsslizqedcpg4zp)


