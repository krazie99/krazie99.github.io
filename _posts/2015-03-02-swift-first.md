
---
layout: post
title: XCode Test Case (Swift)
excerpt: "XCode에서 iOS 테스트 케이스 작성 하기"
tags: [ios, objective-c, xctext, test, test-case, swift]
---

# 시작하며

Objective-C 개발자의 Swift의 간단한 어플 개발에 대한 글을 적으려고 합니다.

[스위프트(Swift)]는 애플의 iOS와 OS X를 위한 프로그래밍 언어이고, 2014년 6월 2일 애플 세계 개발자 회의에서 소개 되었습니다.

이 새로운 언어를 가지고 웹뷰를 이용한 간단한 앱을 만들도록 하겠습니다 :)

*해당 글은 제가 버즈니에서 근무할 때 적은 글[^1]입니다*

# 기본 Swift 문법


### 변수,상수 & 문자열

새로운 언어인 Swift는 [추론 데이터 형식] - 함수형 언어 입니다. 즉 프로그래머가 형을 결정 하지 않고 컴파일러가 데이터 형식을 확인하게 됩니다.

Swift에서 변수는 `var`, 상수는 `let` 으로 표기 합니다.

{% highlight swift %}
var str = "변수"
let mVal = 10
{% endhighlight %}

해당 변수등에 타입을 지정하려면 `:` 를 사용합니다.

{% highlight swift %}
var str : String?
{% endhighlight %}

문자열이나 숫자 안에 값을 포함 시기는 방법은 \\(X) 를 사용하시면 됩니다.

{% highlight swift %}
let sun = 10
let ho = 20
let sum = sun + ho
let str = "10 + 20 = \(sum) = \(sun + ho)"
{% endhighlight %}


### 함수

Swift에서는 `func` 을 이용하여 함수를 선언할 수 있습니다.

{% highlight swift %}
func getWorld(first : String, last : String) -> String { // (인자값 : 타입) -> 리턴타입
    return "Hello World with \(first) \(last)"
}
{% endhighlight %}

Swift에서는 함수 선언시 파라미터에 기본값을 설정 할수 있고,

두개 이상의 파라미터가 존재한다면 기본값을 가지는 파라미터를 마지막에 두어야 합니다. (호출시 생략가능)

그리고 두개 이상 값을 반환할 수 있습니다.

{% highlight swift %}
func getWorld(first : String, last : String = "최") -> (world : String, name : String) {
    return ("Hello World", "\(first) \(last)")
}

var r = getWrold()
var r1 = getWorld().world
var r2 = getWrold().name
{% endhighlight %}


### Optional Type

Optional Type 은 `nil`[^2] 이 될 수 있는 변수(상수)를 의미하며 선언할 때 `?` 를 사용합니다.

기존 nil로 인한 앱 크래쉬를 막아 주는것입니다.

값이 있는 경우에는  `!`[^3] 를 이용하여 값이 있음을 명시적으로 알려어야 합니다.

if 문을 사용해서 해당 Optional Type 값이 유효한 지 확인할 수 있습니다.

{% highlight swift %}
var nVal : Int?

if nVal {
    println("nVal has value \(nVal)")
} else {
    println("nVal has no value") // nVal이 nil 값이므로 해당줄이 실행
}
{% endhighlight %}


# Demo

Swift로 구글 모바일 사이트를 WebView를 통해 화면에 표시해주고

사용자의 클릭이벤트를 잡아서 검색결과를 네비게이션 컨트롤러를 이용해 다음페이지로 푸쉬해주는 앱을 만들어보겠습니다.

해당 샘플 프로젝트는 [GitHub]에서 다운로드 가능합니다.


### 뷰 생성

구글 모바일 사이트를 보여줄 웹뷰를 생성하고 현재 화면에 표시합니다.

{% highlight swift %}
class ViewController: UIViewController, UIWebViewDelegate{

    var webview : UIWebView?

    override func viewDidLoad() {
        //웹뷰 생성
        webview = UIWebView(frame: self.view.bounds);
        //오토리사이즈마스크 사용시
        //webview?.autoresizingMask = UIViewAutoresizing.FlexibleRightMargin | UIViewAutoresizing.FlexibleWidth | UIViewAutoresizing.FlexibleHeight | UIViewAutoresizing.FlexibleBottomMargin |   UIViewAutoresizing.FlexibleTopMargin | UIViewAutoresizing.FlexibleLeftMargin
        webview?.loadRequest(NSURLRequest(URL: NSURL(string: "http://google.com/")!))
        webview?.scrollView.bounces = true
        webview?.delegate = self

        self.view.addSubview(webview!)
    }
}
{% endhighlight %}

### Delegate

웹뷰 `webview?.delegate = self` 에 대한 Delegate 함수들 입니다.

로딩시 인디케이터등을 사용 하거나 시점에 관한 필요한 처리가 가능합니다.

{% highlight swift %}
//MARK: WEBVIEW
//웹뷰 로딩 실패
func webView(webView: UIWebView, didFailLoadWithError error: NSError) {
    print("LOAD FAILED : \(error.localizedDescription)\n")
}

//웹류 로딩 끝
func webViewDidFinishLoad(webView: UIWebView) {
    print("LOAD FIN\n")
}

//웹뷰 로딩 시작
func webViewDidStartLoad(webView: UIWebView) {
    print("LOAD START\n")
}

//웹뷰 클릭시 이동
func webView(webView: UIWebView, shouldStartLoadWithRequest request: NSURLRequest, navigationType: UIWebViewNavigationType) -> Bool {

    print("LOAD : \(request.URL.absoluteString)\n")

    //클릭이벤트를 잡아서 Push
    if navigationType == UIWebViewNavigationType.LinkClicked
    {
        var v = SubWebViewController();
        v.strUrl = request.URL.absoluteString
        v.title = request.URL.host
        self.navigationController?.pushViewController(v, animated: true)

        return false;
    }

    return true;
}
{% endhighlight %}

# 정리하며

본 글에서는 웹(뷰)를 생성 하고 및 Delegate에 연결하여 사용하는 방법을 설명하고 간단한 앱을 만들어 보았습니다.

기존의 Objective-C 와는 완전히 다른 개념으로 코딩을 해야 하는 부분이 어려웠습니다.

이 샘플 프로젝트를 통해서 Swift에 한발자국 더 다가갈수 있기를 바랍니다.

Swift에 더 자세한 정보를 얻으시려면 [레퍼런스 문서]를 참고 하시기 바랍니다.

감사합니다.


[추론 데이터 형식]: http://en.wikipedia.org/wiki/Type_inference
[스위프트(Swift)]: https://developer.apple.com/swift/
[GitHub]: https://github.com/krazie99/swift_webview
[레퍼런스 문서]: https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/index.html


[^1]: (버즈니 블로그)[http://engineering.buzzni.com/2015/03/02/swift_first.html]
[^2]: Swift에서의 nil은 모든 타입에 대한 '값이 없다'를 나타냄
[^3]: forced-unwrapping operator
