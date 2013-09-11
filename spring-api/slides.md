!SLIDE subsection
# Spring WebSocket API

!SLIDE smaller bullets incremental
# Spring's own WebSocket API
<br><br>
* Abstraction over WebSocket runtimes
* Including JSR-356 containers
* But not limited to it-<br>Jetty 9 native API, Netty (experimental)
* Supports transparent fallback options<br>based on SockJS protocol
* New `spring-websocket` module

!SLIDE smaller
# Example
<br><br>
    @@@ java

    public class EchoHandler extends TextWebSocketHandlerAdapter {


      @Override
      public void handleTextMessage(WebSocketSession session,
          TextMessage message) throws Exception {

        session.sendMessage(message);
      }

    }

!SLIDE smaller
# Java config

    @@@ java

    @Configuration
    @EnableWebSocket
    public class WebSocketConfig implements WebSocketConfigurer {


      @Override
      public void registerWebSocketHandlers(
          WebSocketHandlerRegistry registry) {

        registry.addHandler(new EchoHandler(), "/echo");
      }

    }

!SLIDE small bullets incremental
# `HandshakeInterceptor`

* Access to HTTP request & response<br>before and after handshake
* Can preclude handshake
* Can pass "handshake" attributes to `WebSocketSession`
* Example `HttpSessionHandshakeInterceptor`

!SLIDE small bullets incremental
# `WebSocketHandlerDecorator`

* Transparent decoration
* `ExceptionWebSocketHandlerDecorator`
* `LoggingWebSocketHandlerDecorator`
* The above applied by default

!SLIDE smaller
# `PerConnectionWebSocketHandler`

    @@@ java

    @Configuration
    @EnableWebSocket
    public class WebSocketConfig implements WebSocketConfigurer {


      // ...


      @Bean
      public WebSocketHandler snakeHandler() {
        Class<?> clazz = SnakeWebSocketHandler.class;
        return new PerConnectionWebSocketHandler(clazz);
      }

    }

!SLIDE smaller bullets incremental
# Note on URL Mapping

* Spring does not use JSR-356 deployment mechanism
* Enables mapping `WebSocketHandler` in Spring MVC
* Requires container-specific `RequestUpgradeStrategy`
* Currently supported are Tomcat, Jetty, Glassfish
* [WEBSOCKET_SPEC-211](https://java.net/jira/browse/WEBSOCKET_SPEC-211) (exercise vote)

!SLIDE small bullets incremental
# Client-Side API

* Programmatic handshake via `WebSocketClient`
* Returns `ListenableFuture<WebSocketSession>`
* Also available is declarative style (can auto-start)
* `ConnectionManagerSupport` and sub-classeses

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





