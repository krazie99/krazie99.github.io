---
layout: post
title: iOS Push Certification (pem)
excerpt: iOS 푸쉬 인증서 만들기
comments: true
tags: [ios, objective-c, push, push-notification, notification, apns]
image:
  feature: push/apns.png
---

## iOS용 푸쉬 인증서 생성하기

- [애플 개발자사이트](https://developer.apple.com/account/ios/certificate/certificateList.action) 에서 로그인후 APNS 인증서를 만듭니다. 다운로드후에 더블 클릭해서 **키체인**에 넣습니다.

![]({{ site.url }}/img/push/1.png.jpeg)

> 개발용, 애드훅 및 릴리즈용은 따로 만들어야 합니다.

- **응용프로그램 > 유틸리티 > 키체인 > 내 인증서** 에서 개발 및 릴리즈용 *푸쉬 인증서*를 확인합니다. 화살표를 클릭하면 개인키가 보입니다.

![]({{ site.url }}/img/push/2.png.jpeg) <br>

- 해당 인증서와 개인키를 따로따로 보내기를 이용하여 바탕화면으로 보냅니다.

![]({{ site.url }}/img/push/3.png.jpeg) <br>
![]({{ site.url }}/img/push/4.png.jpeg) <br>
![]({{ site.url }}/img/push/5.png) <br>

- 해당 명령어 인증서와 키파일의 인증서를 생성합니다. 여기서 PEM 패스워드를 적절하게 입력합니다. *(4자 이상)*

{% highlight objective-c %}
$ sudo openssl pkcs12 -clcerts -nokeys -out apns-dist-cert.pem -in apns-dist-cert.p12  
$ sudo openssl pkcs12 -nocerts -out apns-dist-key.pem -in apns-dist-key.p12  
{% endhighlight %}

![]({{ site.url }}/img/push/6.png.jpeg) <br>
![]({{ site.url }}/img/push/7.png) <br>

- 해당 명령어로 개인키를 제거 합니다.

{% highlight objective-c %}
$ sudo openssl rsa -in apns-dist-key.pem -out apns-dist-key-noenc.pem
{% endhighlight %}

![]({{ site.url }}/img/push/8.png.jpeg) <br>
![]({{ site.url }}/img/push/9.png) <br>

- 이제 마지막으로 key 파일과 cert 파일을 합쳐줍니다.

{% highlight objective-c %}
$ cat apns-dist-cert.pem apns-dist-key-noenc.pem > apns-dist.pem
{% endhighlight %}

![]({{ site.url }}/img/push/10.png.jpeg) <br>
![]({{ site.url }}/img/push/11.png) <br>

개발용 푸쉬 인증서도 위의 과정을 반복하여 만들면 됩니다.
