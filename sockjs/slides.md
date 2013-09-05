!SLIDE subsection
# SockJS Support

!SLIDE small bullets incremental
# [Philosophy](https://github.com/sockjs/sockjs-client)

* Emulate WebSocket API as close as possible
* At least one streaming protocol per major browser
* Cross-domain and cookie support
* Polling in old browsers, hosts behind restrictive proxies
* No Flash inside

!SLIDE center
## SockJS Transports by Browser

![Table with SockJS transports by browser](transports.png)

!SLIDE smaller
# Enable SockJS in Spring

    @@@ java

    @Configuration
    @EnableWebSocket
    public class WebSocketConfig implements WebSocketConfigurer {

      @Override
      public void registerWebSocketHandlers(WebSocketHandlerRegistry reg) {
        reg.addHandler(new EchoHandler(), "/echo").withSockJS();
      }

    }

!SLIDE smaller
# `WebSocketHandler`
## (same as before)

    @@@ java

    public class EchoHandler extends TextWebSocketHandlerAdapter {

      @Override
      public void handleTextMessage(WebSocketSession sess, TextMessage msg) {
        sess.sendMessage(msg);
      }

    }

!SLIDE small bullets incremental
# SockJS client

    @@@ javascript

      var ws = new SockJS("ws://localhost:8080/echo");

      ws.onopen = function (event) { };

      ws.onmessage = function (event) { };

      ws.onclose = function (event) { };

!SLIDE center
![Chrome browser with SockJS network activity](sockjs-demo.png)

!SLIDE small bullets incremental
# The SockJS Protocol

* Defines URL scheme
* Provided in the form of a readable [test suite](http://sockjs.github.io/sockjs-protocol/sockjs-protocol-0.3.3.html)
* [Wide support](https://github.com/sockjs/sockjs-client) across languages

!SLIDE small bullets incremental
# SockJS URL Scheme

        GET  /echo

        GET  /echo/info

        POST /echo/<server>/<session>/<transport>

!SLIDE small
# SockJS Requests

    GET /echo/info

    POST /echo/375/5rzpg08l/xhr_streaming  # server-to-client

    POST /echo/375/5rzpg08l/xhr_send  # client-to-server

    POST /echo/375/5rzpg08l/xhr_send  # client-to-server

!SLIDE small bullets incremental
# Where Does It Work?

* Any Servlet 3.0 container
* Even if server doesn't have WebSocket yet!
* No hard dependency on Servlet API though
* Experimental Netty support

!SLIDE small bullets incremental
# Client Disconnects

* Servlet 3 containers don't detect clients going away
* `SockJsService` however sends periodic heartbeats
* A failure to send a message closes the session 
* See [related discussion](http://markmail.org/message/yhsslizqedcpg4zp)


