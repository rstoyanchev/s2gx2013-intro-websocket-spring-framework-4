!SLIDE subsection
# Spring WebSocket API

!SLIDE smaller bullets incremental
# Spring WebSocket API

* Abstraction for WebSocket runtimes
* Including JSR-356 containers
* But not only - e.g. Jetty 9 API, Netty, etc
* SockJS fallback options
* New `spring-websocket` dependency

!SLIDE smaller
# Example

    @@@ java

    public class EchoHandler extends TextWebSocketHandlerAdapter {

      @Override
      public void handleTextMessage(WebSocketSession sess, TextMessage msg) {
        sess.sendMessage(msg);
      }

    }

!SLIDE smaller
# Java config

    @@@ java

    @Configuration
    @EnableWebSocket
    public class WebSocketConfig implements WebSocketConfigurer {

      @Override
      public void registerWebSocketHandlers(WebSocketHandlerRegistry reg) {
        reg.addHandler(new EchoHandler(), "/echo");
      }

    }

!SLIDE small bullets incremental
# `HandshakeInterceptor`

* Before/after handshake
* Access to HTTP request & response
* Ability to preclude handshake
* Can pass "handshake" attributes to `WebSocketSession`
* See `HttpSessionHandshakeInterceptor`

!SLIDE small bullets incremental
# `WebSocketHandlerDecorator`

* Transparent decoration
* `ExceptionWebSocketHandlerDecorator`
* `LoggingWebSocketHandlerDecorator`
* Automatically applied

!SLIDE smaller
# `PerConnectionWebSocketHandler`

    @@@ java

    @Configuration
    @EnableWebSocket
    public class WebSocketConfig implements WebSocketConfigurer {

      // ...

      @Bean
      public WebSocketHandler snakeHandler() {
        return new PerConnectionWebSocketHandler(SnakeWebSocketHandler.class);
      }

    }

!SLIDE small bullets incremental
# Note on URL Mapping

* Spring doesn't use JSR-356 deployment
* Free to map `WebSocketHandler` via Spring MVC or other
* Requires container-specific `RequestUpgradeStrategy`
* Currently supported: Tomcat, Jetty, Glassfish
* See [WEBSOCKET_SPEC-211](https://java.net/jira/browse/WEBSOCKET_SPEC-211) (vote please)

!SLIDE small bullets incremental
# The Client-Side

* Programmatic handshake via `WebSocketClient`
* Also declarative style that can auto-start
* Via `ConnectionManagerSupport` and sub-classeses

!SLIDE smaller
# Example

    @@@ java

    @Configuration
    static class ClientConfig {

      @Bean
      public WebSocketConnectionManager connectionManager() {

        String url = "ws://example.com:8080/echo";
        WebSocketHandler handler = new EchoWebSocketHandler();
        WebSocketClient client = new StandardWebSocketClient();

        WebSocketConnectionManager manager = 
            new WebSocketConnectionManager(client, handler, url);

        manager.setAutoStartup(true);
        return manager;
      }

    }





