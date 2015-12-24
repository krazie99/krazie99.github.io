---
layout: post
title: iOS9 Universal Links
excerpt: "웹 주소 링크로 바로 앱을 열수 있게 해주는 Universal Links (iOS9)"
tags: [ios, objective-c, Universal Link, ios9, 유니버셜링크, swift]
---

### Universal Links

**유니버셜 링크[^1]**란 iOS9 이상 버전에서 웹 링크를 눌렀을때 사파리 브라우져가 아닌 바로 설치된 앱으로 연결 해주도록 하는 기술 입니다.  
만약 앱이 설치 되어 있지 않다면 사파리로 자동으로 연결이 됩니다.

예를들어 사파리에서 [http://youtube.com](http://youtube.com) 을 링크를 눌러서 열때, 앱이 설치 되어 있으면
**유투브 앱**이 실행되게 하는 기술 입니다.

즉, **하나의 URL**을 가지고 앱이나 웹을 자동으로 연결 되도록 하기때문에 좀더 심플해지고[^2] 사용하기 편해졌습니다.  

그리고, **Universal Links** 를 사용하려면 https (SSL) 을 적용 해야 사용이 가능합니다.

<br>

#### apple-app-site-association ####

유니버셜 링크를 적용하려면 해당 JSON 데이터가 적혀있는 **apple-app-site-association** 파일을 웹서버의 루트 혹은 사용할 URL의 위치에 업로드 해야 합니다.

{% highlight JSON %}
{
    "applinks": {
        "apps": [],
        "details": [
            {
                "appID": "9JA89QQLNQ.io.github.krazie99",
                "paths": [ "*", "/"]
            }
        ]
    }
}
{% endhighlight %}
> **details**에는 하나 이상 입력 가능합니다.

+ **AppID**
  - **PrefixID**.앱번들아이디  
+ **paths**
  - **\*** : ```하위 모든 항목```
  - **/** : ```루트```
  - **/서브/** : ```서브 폴더```
  - **/서브/\*** : ```서브 이하 모든 항목```
  - **NOT /서브2/** : ```서브2를 제외```

![]({{ site.url }}/img/universallink/1.png)      

> 애플 개발자 사이트에서 **Prefix ID** 를 확인 하실 수 있습니다.  

<br>

#### XCode Project Setting ####

위에 **apple-app-site-association** 파일을 서버에 업로드를 하였으면, 앱 프로젝트 세팅에서 앱 링크 도메인을 입력 해주셔야 합니다.  
***XCode Project Setting > Capabilities*** 에서 ***Associated Domains*** 을 ```ON``` 해주시고,
Domains 에 *"**applinks:도메인**"* 을 입력하시고 저장을 하게 되면 ```Entitlements``` 파일이 생성 되고 해당 파일에 저장됩니다.

![]({{ site.url }}/img/universallink/2.png)   

위의 설정을 완료 하고 나서는 꼭 **Provisioning Profile** 을 갱신 하셔야 정상적으로 작동 합니다.

<br>
  
#### AppDelegate ####

마지막으로, 링크를 타고 실행 되는 **AppDelegate** 의 딜리게이트 처리를 하시면 됩니다.

{% highlight swift %}
func application(application: UIApplication, continueUserActivity userActivity: NSUserActivity, restorationHandler: ([AnyObject]?) -> Void) -> Bool {

  guard let _rootViewController = self.window?.rootViewController as? ViewController else {
      return false
    }

    if let strUrl = userActivity.webpageURL?.absoluteString {
      //딥링크 처리  
    }

    return true
}
{% endhighlight %}

유니버셜 링크를 적용 후에는 [링크](https://search.developer.apple.com/appsearch-validation-tool/) 에서 제대로 적용이 되었는지 확인이 가능합니다.

<br>

### 정리하며

만약 개발하고 있는 혹은 개발된 앱에서 **유니버셜 링크** 를 사용하게 된다면 사용자에게 더 좋은 경험을 줄 수 있다고 생각합니다.

<br>

[^1]: [유니버셜 링크 레퍼런스 문서](https://developer.apple.com/library/ios/documentation/General/Conceptual/AppSearch/UniversalLinks.html#//apple_ref/doc/uid/TP40016308-CH12-SW2)
[^2]: 기존에는 **App Scheme**을 따로 입력하기때문에 웹이랑 앱이랑 URL 이 달랐습니다.
