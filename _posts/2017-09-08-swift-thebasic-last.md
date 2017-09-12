---
layout: post
title: Swift - The Basics (3)
excerpt: Swift 3.0.1 - The Basic (3)
comments: true
tags: [ios, Swift] 
---

안녕하세요. iOS 개발자 엔비냥 입니다.
이제 마지막으로 The Basic 챕터를 번역하였습니다. 오역이나 오타가 있으면 댓글로 부탁드립니다.

—- 

## Optionals

값이 없는 상황에서 optional을 사용하게 됩니다.  optional은 값이 있고 unwrap optional 을 하여 해당 값에 접근 할수 있다는 것과, 값이 없을수 있다는것 이라는 2가지의 가능성을  나타냅니다.

{% highlight swift %}
let possibleNumber = "123"
let convertedNumber = Int(possibleNumber)
// convertedNumber 는 Int? 혹은 옵셔널 Int 타입으로 추론 됩니다. 
{% endhighlight %}

이 예제에서 초기화 시 String 을 Int 로 변환 하려고 합니다. 여기서는 Int 로 반환되기 보다 초기화가 실패를 할 수가 있기 때문에 optional Int 로 반환 됩니다. Optional Int 는 Int? 라고 적습니다. 물음표는 값이 옵셔널을 가지고 있다, 즉 Int 값이 있거나 없을수도 있다는것을 의미 합니다. (다른 타입의 값 즉 Bool, String 같은 값들이 있을수는 없습니다.)

## nil

Optional  변수는 값이 없다를 나타내는 nil 을 가질수 있습니다.

{% highlight swift %}
var serverResponseCode: Int? = 404
// serverResponseCode 실제로 404라는 값을 가지고 있습니다.
serverResponseCode = nil
// serverResponseCode 는 이제 값이 없습니다.
{% endhighlight %}

> nil 은 nonoptional (옵셔널이 아닌) 변수나 상수에서 사용할 수 없습니다.

만약에 optional 변수에 기본 값을 제공하지 않으면, 해당 변수는 자동으로 nil 이 세팅 됩니다.

{% highlight swift %}
var surveyAnswer: String?
// surveyAnswer 는 자동으로 nil 이 세팅됩니다.
{% endhighlight %}

## If Statements and Forced Unwrapping

if 문을 사용해서 nil 이 아닌 optional 값을 가져올수가 있습니다.  equal to (==) 와 not equal to (!=) 을 이용해서 비교 실행을 할 수 있습니다.

{% highlight swift %}
if convertedNumber != nil {
print("convertedNumber contains some integer value.")
}
// convertedNumber 가 어떠한 Integer 값을 가지고 있다.
{% endhighlight %}

만약 optional 이 값이 있다고 확신할때, optional 이름 뒤에 느낌표 (!) 를 붙여서 내재하고 있는 값에 접근할 수 있습니다. 

{% highlight swift %}
if convertedNumber != nil {
print("convertedNumber has an integer value of \(convertedNumber!).")
}
// convertedNumber 123 이라는 값을 가지고 있다.
{% endhighlight %}

## Optional Binding

optional binding 을 이용하여 optional 이 값을 가지고 있는지 찾고나, 만약 가지고 있다면, 임시 상수나 변수로 값을 사용할 수 있게 만들수 있습니다. optional binding 은 if 나 while 문을 사용해서 값이 있는지 체크 할수 있습니다.

{% highlight swift %}
if let #constantName = #someOptional {
#statements
}
{% endhighlight %}

{% highlight swift %}
if let actualNumber = Int(possibleNumber) {
print("\"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
print("\"\(possibleNumber)\" could not be converted to an integer")
}
// Prints ""123" has an integer value of 123
{% endhighlight %}

이 코드는 “ 만약 Int(possibleNumber) 값이 있어서 Int 가 반환이 된다면, 새로운 상수인 actualNumber 에 값을 넣어주라” 라고 읽을 수 있습니다.

만약 변환이 성공한다면 actualNumber 상수는 if문의 첫번째 브랜취에서 사용할수 있게 됩니다.

## Implicitly Unwrapped Optionals

optional 은 상수나 변수가 값이 없다라는것을 허용해 준다고 가르킵니다. Optional 은 if 문으로 값이 있는지 체크를 할수가 있고,  만약 값이 있다면, 조건부로 값을 접근 할수 있습니다.

때때로, 프로그램  구조에서 optional 이 언제나 값이 있을수 있다고 확신할 수 있을수 있습니다.  이때에 Optional 을 열어서 체크를 하는게 필요 하지 않을 수 있습니다.

이런 optional 들은 Implicitly Unwrapped Optionals (절대적인 언래핑 옵셔널) 이라고 합니다. 물음표 (String?) 대신에 느낌표 (String!) 를 이름 뒤에서 써서 사용할 수 있습니다.

{% highlight swift %}
let possibleString: String? = "An optional string."
let forcedString: String = possibleString! // requires an exclamation mark

let assumedString: String! = "An implicitly unwrapped optional string."
let implicitString: String = assumedString // no need for an exclamation mark
{% endhighlight %}

> 만약에 Implicitly Unwrapped Optional 이 값이 없고 (nil), 접근을 하게 된다면 런타임 에러를 발생하게 됩니다.

## Error Handling

error handling을 이용하여 에러 조건에 따라 응답을 할 수 있습니다.

{% highlight swift %}
func canThrowAnError() throws {
// this function may or may not throw an error
}
{% endhighlight %}

만약 함수가 에러 조건을 만나게 되면 error 를 던질수가 있습니다. throws 키워드를 사용해서 함수에서 error 를 던질수 있게 할 수 있습니다.

error 를 던지는 함수를 호출할때, try 키워드를 사용해서 표현할 수 있습니다.

{% highlight swift %}
do {
try canThrowAnError()
// no error was thrown
} catch {
// an error was thrown
}
{% endhighlight %}

## Assertions

어떤 경우에, 코드에서 만족하지 않는 조건이 있다면, 간단하게 멈춰야 할때가 있습니다. 이 상황에는, debug 시 값이 없거나 맞는 값이 아닐때 assertion 을 사용해서 코드가 멈추가 할 수 있습니다.

Swift 의 글로벌 스탠다드 라이브러리 함수인 assert(_:_:file:line:) 을 사용하여 assertion 을 이용 할 수 있습니다.

{% highlight swift %}
let age = -3
assert(age >= 0, "A person's age cannot be less than zero")
// this causes the assertion to trigger, because age is not >= 0
{% endhighlight %}

> Xcode 에서 assertion 들은 릴리즈 컴파일이 될때 사용이 불가능 하게 됩니다.

——

지금까지 Swift 3.0.1 에서 The Basic 챕터를 번역 하였습니다.
모든 글을 다 번역한 것이 아니고, 최대한 간략하게 정리 하였습니다.
각 섹션들은 다음 챕터들에서 더 자세히 설명이 될것이고, 번역 하도록 하겠습니다. 감사합니다.
