!SLIDE subsection

# Intro to WebSocket with<br>Spring Framework 4.0
## [Rossen Stoyanchev](http://twitter.com/rstoya05)

!SLIDE small
# This presentation
<br><br>
## [https://github.com/rstoyanchev/](https://github.com/rstoyanchev/s2gx2013-intro-websocket-spring-framework-4)
## [s2gx2013-intro-websocket-spring-framework-4](https://github.com/rstoyanchev/s2gx2013-intro-websocket-spring-framework-4)

!SLIDE small bullets incremental
# About this talk

* Introduces WebSocket and Spring Framework support
* Separate talk on actually-<br>"Building WebSocket Browser Apps with Spring"
* [https://github.com/rstoyanchev/](https://github.com/rstoyanchev/s2gx2013-websocket-browser-apps-with-spring)<br>[s2gx2013-websocket-browser-apps-with-spring](https://github.com/rstoyanchev/s2gx2013-websocket-browser-apps-with-spring)

!SLIDE small
# WebSocket
<br>
## "mechanism for browser-based applications...
## two-way communication with servers...
## does not rely on multiple HTTP connections"
<br>
\- [RFC 6455](http://www.ietf.org/rfc/rfc2616.txt), <i>The WebSocket Protocol</i>

!SLIDE center
![HTML5 logo](html5.png)

!SLIDE smaller bullets incremental
# Excitement is justified
# given long history of Ajax/Comet

!SLIDE smaller bullets incremental
# However expectations have come
# ahead of experience

!SLIDE smaller bullets incremental
# A Few (False) Expectations

* It's standard, it's supported everywhere
* It's a replacement for Ajax/Comet ([maybe even REST](http://www.infoq.com/news/2012/02/websockets-rest))
* I know web apps, how different can this be?
* I will program to a WebSocket API

!SLIDE smaller bullets incremental
# Reality Check
<br><br>
* Not supported in IE < 10
* There are issues with proxies
* Not a replacement for REST
* A socket is very low level to work on
* Event-driven, messaging architecture

!SLIDE center
# WebSockets
_"Toto, I've a feeling we're not in REST land any more"_
<br>
![Wizard of Oz](WizardYellowBrick.jpg)

!SLIDE smaller bullets incremental
# Last year's talk
## [Available on YouTube](http://www.youtube.com/watch?v=z-CYO1ABCp4)
<br><br><br>
* Broad, pragmatic introduction
* A survey of the land
* Some key (open-ended) questions defined

!SLIDE smaller bullets incremental
# Key Takeaways from Last Year
<br><br>
* The need for fallback options will persist
* Integrating into a real application not yet trivial
* "Pure" WebSocket apps in the wild unlikely
* Questions remain around usage patterns






