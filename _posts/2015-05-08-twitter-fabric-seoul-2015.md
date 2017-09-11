---
layout: post
title: Twitter Flock Seoul 2015
excerpt: Crashlytics, Digits & Mopub
comments: true
tags: [app, twitter, fabric, digits, mopub, crashlytics]
---

# 시작하며

***해당 글은 제가 버즈니에서 근무할 때 작성했던 글[^4]입니다***

Twitter에서 2014년에 [Fabric] SDK[^1]를 선보였고, 이번에 [Flock 2015] 행사를 아시아투어 첫번째로 한국에서 개최 하였습니다.

저는 이번에 발표하는 [Digits] 와 [Mopub] 에 관심이 있어서 이번 행사에 참여 하게 되었습니다.

![](http://i61.tinypic.com/291dll0.jpg)

이번 글에서는 Twitter Flock에서 발표했던 내용 중에 Crashlytics, Digits 와 Mopub에 대해 간단히 소개하려고 합니다.

SDK 설치 방법은 [Fabric] 사이트에 자세히 나와있으므로 이 포스트에서 다루지 않겠습니다.


## Crashlytics

Crashlytics는 앱 개발자들에게 실시간으로 앱 크래쉬 오류를 수집해 주고 베타 테스팅을 도와주는 툴입니다.

![](http://i60.tinypic.com/s1nx3c.png)
![](http://i58.tinypic.com/35asmz7.png)

> 각 앱 크래쉬 로그는 어느 클래스(파일)의 몇 라인에서 오류가 나는지, 몇번의 크래쉬가 나왔는지 분석해 줍니다.

![](http://i62.tinypic.com/29y2gw4.png)

> 안드로이드는 APK 를 iOS 는 애드훅 배포를 Crashlytics 를 통해 간편하게 이용할 수 있습니다.

## Digits

많은 앱들이 ID, Email, Password 등 여러 인증 방식을 사용합니다.

근래에 모바일 SNS가 발달하고 더 편한 방식을 위해 소셜 로그인[^2]을 이용하여 사용자 로그인을 하기도 합니다.

하지만, 이 방식도 이제는 너무 많아진 SNS 플랫폼들로 인해 많이 불편해지고 있습니다.

[Digits]는 사용자 로그인을 더 간편하게 사용하기 위해 나온, 휴대폰 번호를 이용하는 로그인 방식입니다.

물론 이미 여러 어플리케이션들이 사용하는 방식이긴 하지만, 트위터에서 툴을 제공 함으로써 모든 것을 직접 구현할 필요가 없고,

SMS 비용도 무료이며, 현재 216개의 나라와, 32개의 언어를 제공합니다.

![](https://get.digits.com/assets/merges-ea829b491da3ad982d7e41a80185d421.png)

> Digits 는 iOS,Android & Web 에서 사용할 수 있도록 제공 됩니다.

사용하는 방법은 간편합니다.  자세한 사용 방법은 [Digits 문서]를 확인하시기 바랍니다.

{% highlight objective-c %}
// Objective-c
- (void)viewDidLoad {
    DGTAuthenticateButton *digitsButton =
        [DGTAuthenticateButton buttonWithAuthenticationCompletion:^
            (DGTSession *session, NSError *error) {
            // Inspect session/error objects
        }];

    [self.view addSubview:digitsButton];
}

{% endhighlight %}

{% highlight swift %}
// Swift
override func viewDidLoad() {
    let digitsButton = DGTAuthenticateButton(
    authenticationCompletion: { (session, error) in
    // Inspect session/error objects
    })

    self.view.addSubview(digitsButton)
}
{% endhighlight %}

> iOS에서 Digits 버튼을 사용한 예제.


Digits의 다이얼로그는 자신의 앱에 맞게 색상이나 문구등 커스텀이 가능합니다.

사용자의 주소록을 이용하여 친구들이 해당 어플리케이션을 사용하고 있는지 확인이 가능합니다.

그리고, 트위터의 보안[^3]시스템으로 안전하게 이용할 수 있습니다.

## Mopub

[Mopub]은 Twitter에서 나온 모바일 광고 SDK 입니다. 물론 현재에도 iAD, 애드몹등 여러가지 모바일 광고 SDK가 있습니다.

요즘은 많은 사용자들이 모바일 어플리케이션의 광고에 대한 거부감을 가지고 있습니다.

특히 하단/상단 배너나, 전면 광고등은 많이 꺼려지고 있습니다만 어플리케이션을 개발하고 운영을 하려면 수익이 필요합니다.

많은 업체들은 페이스북처럼 네이티브형 광고를 넣는 등 사용성을 최대한 헤치지 않는 형태의 광고를 통해 수익을 도모하고 있습니다.

[Mopub]을 이용하면 개발자가 원하는 레이아웃을 제작하고 이를 통해 거부감 없이 자연스럽게 광고를 내보내고 수익을 창출 할 수 있습니다.

또한, 기존의 배너, 전면 광고, 동영상 방식 등도 지원합니다.

![](http://www.mopub.com/wp-content/uploads/2015/01/formats_lg_2.png)

# 정리하며

Twitter에서 [Fabric] SDK를 통해 위와 같은 모바일 통합 플랫폼을 배포하고 있고,

이러한 플랫폼을 사용하게 되면 더 안정적이고 신속하게 앱을 만들고 배포할 수 있습니다.


[Fabric]: https://get.fabric.io
[Flock 2015]: http://flock.fabric.io
[Crashlytics]: https://get.fabric.io/crashlytics
[Digits]: https://get.fabric.io/digits
[Mopub]: https://get.fabric.io/mopub
[Digits 문서]: https://dev.twitter.com/twitter-kit/overview

[^1]: 트위터의 모바일 앱 개발을 위한 모듈형 통합 플랫폼
[^2]: 쇼셜 로그인중 대표적으로 페이스북, 트위터, 구글+ 등이 있습니다.
[^3]: Digits 보안 - http://get.digits.com/enterprise-security
[^4]: [버즈니 블로그](http://engineering.buzzni.com/2015/05/08/twitter_fabric.html)
