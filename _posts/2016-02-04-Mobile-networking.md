---
layout: post
title: Mobile Networking
excerpt: "모바일 통신에 대한 간단한 정리"
tags: [mobile, socket, tcp/ip, http, networking]
---

## 시작하며

회사 웹&앱 서비스 개발을 하다 보면 네트워크 통신 개발이 거의 대부분을 차지할정도로 많은 부분에서 사용하게 됩니다.    
그렇다면 서비스 개발을 할 때 어떤 방식의 통신을 사용 하면 좋을 지에 대해 많은 생각을 하게 됩니다.  

그리고, 간혹 모바일에서는 어떤 통신을 사용하는지 궁금해 하는 분들이 있습니다만, 통신 기술은 기본적으로 다 같다고 생각 하면 됩니다.

여기서는 **통신 프로토콜** 중에서 HTTP 통신과 Socket 통신에 관련된 글을 간단하게 적어보려고 합니다.  
<br>

### Communications protocol

**통신 프로토콜**[^1]은 통신 서비스 혹은 기능 수행을 위해서 당사자간 (서버/클라이언트) 교환하는
데이터의 종류와 표현 방식, 교환 절차, 그리고, 교환 과정에서 실행해야 할 행위(Action)에 대한 규약입니다.

대표적인 프로토콜은 IBM의 폐쇄형 망 구조인 **SNA(System Network Architecture)**와 개방형 망 구조인 **TCP/IP**가 있습니다.  
**TCP/IP** 응용 계층에 적용 확장된 프로토콜에는 전자 우편을 위한 **SMTP(Simple Mail Transfer Service)**, 파일 전송을 위한 **FTP(File Transfer Protocol)**, 그리고 제일 많이 사용하게 되는 웹서비스를 위한 **HTTP(Hyper Text Transfer Protocol)**등이 있습니다.

{% highlight c %}
HTTP : Hyper Text Transfer Protocol
HTTPS : Secure Hyper Text Transfer Protocol
FTP : File Transfer Protocol
SFTP : Secure File Transfer Protocol
Telnet : TEminaL NETwork
POP3 : Post Office Protocol version 3
SMTP : Simple Mail Transfer Protocol
SSH : Secure Shell
SSL : Secure Socket Layer
SOAP : Simple Object Access Protocol
{% endhighlight %}
<br>

### HTTP (HyperText Transfer Protocol)

**HTTP**(HyperText Transfer Protocol, 문화어: 초본문전송규약, 하이퍼본문전송규약)는 **WWW** 상에서 정보를 주고받을 수 있는 프로토콜입니다. 주로 HTML 문서를 주고받는 데에 쓰인다. TCP와 UDP를 사용하며, 80번 포트를 사용합니다.[^2]

![]({{ site.url }}/img/http/1.png)

> **HTTP Request Structure**

- **Request Line** : HTTP 요청에 대한 메소드[^3]와 파일 경로 정보 및 HTTP 버전을 나타냅니다.
- **General Headers** : 클라이언트 요청 및 서버의 응답 양쪽에서 사용 되고 날짜 등의 정보들이 들어갑니다.
- **Request Headers**
  - **Host** : 호스트의 이름 및 URI의 포트 번호를 지정합니다.
  - **From** : 현재 사용하고 있는 클라이언트의 전자 우편주소를 반환 합니다.
  - **Accept** : 클라이언트가 우선적으로 받아들이는 미디어 형을 명시 합니다.[^4]
  - **User-Agent** : 클라이언트 프로그램에 대한 식별 가능한 정보를 줍니다.
- **Entity Headers** : 메시지의 페이로드(payload)로서 전송되는 정보.
- **Message Body** : 클라이언트 요청에 대한 메세지 (Params).

**HTTP Response Header** 에는 HTTP 통신 상태에 대한 코드 **(Status Code)**[^5] 등이 추가 됩니다.

<br>

### Socket

소켓 통신은 네트워크를 통한 서로 다른 컴퓨터에 수행 되는 프로세스간의 통신 채널 입니다. 그리고, 소켓 통신 종류에는 **TCP** 와 **UDP** 있습니다.

- **TCP** : 상대방의 IP와 포트를 알고 접속 (신뢰성), 양방향 통신이 가능합니다.
- **UDP** : 소켓을 개설하고 무조건 데이터를 전송 (비신뢰성), 데이터 전송에 대해 받는곳에서 포트를 열어보기 전에는 알수가 없습니다.

![]({{ site.url }}/img/http/2.gif)

간단하게 **Socket** 은 통신을 좀더 쉽게 사용할 수 있도록 한 **API 함수** 를 모아놓은 **Library** 라고 생각하면 됩니다.

![]({{ site.url }}/img/http/3.png)

> Socket 요청 절차

소켓 TCP 방식은 양방향 요청 및 응답이 가능하기 때문에 채팅 프로그램 등에서 자주 사용하게 됩니다.

<br>  

## 정리하며

제목은 거창하게 **Mobile Networking** 이라고 적었지만, 이 글에서는 제가 모바일 개발시에 많이 사용하게 되는 **HTTP 프로토콜** 과 **Socket** 에 대해 간단하게 정리 하였습니다.

물론 HTTP 통신에 대한 모든 부분을 구현하지는 않습니다. **애플워치** 같은 특별한 경유를 제외하고는 보통 **iOS 프로그래밍** 에서 **HTTP 통신** 을 할때 [AFNetworking (Objective-c)](http://afnetworking.com) 및 [Alamofire (Swift)](https://github.com/Alamofire/Alamofire) 통신 라이브러리를 사용하고 있습니다.

이 글을 통해 통신 프로토콜에 대해 간단하게라도 이해가 되었으면 합니다.

<br>  


[^1]:통신 프로토콜 (Communications protocol) [위키백과](https://ko.wikipedia.org/wiki/통신_프로토콜)
[^2]:HTTP [위키백과](https://ko.wikipedia.org/wiki/HTTP)
[^3]:HTTP 메소드 : GET, POST, HEAD, PUT, DELETE, TRACE
[^4]:Accept-Charaset (문자셋), Accept-Encoding (gzip 등 인코딩 방식), Accept-Language (지원 언어)
[^5]:HTTP 상태 코드 [위키백과](https://ko.wikipedia.org/wiki/HTTP_상태_코드)
