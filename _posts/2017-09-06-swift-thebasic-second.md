---
layout: post
title: Swift - The Basics (2)
excerpt: Swift - The Basic (2)
comments: true
tags: [ios, Swift]
---

안녕하세요. iOS개발자 엔비냥 입니다.
Swift : The Basics 두번째 번역입니다. 오역이 있으면 답글 부탁드립니다.

## Numeric Literals (숫자 리터럴)

* 10진수는 prefix 가 없습니다.
* 2진수는 0b 를 prefix로 사용합니다.
* 8진수는 0o 를 prefix로 사용합니다.
* 16진수는 0x 를 prefix로 사용합니다.

{% highlight swift %}
let decimalInteger = 17
let binaryInteger = 0b10001       // 17 (2진수)
let octalInteger = 0o21           // 17 (8진수)
let hexadecimalInteger = 0x11     // 17 (16진수)
{% endhighlight %}

소숫점 리터럴은 10진수와 16진수로 가능 합니다. 소숫점의 양쪽 사이드에는 10진수 혹은 16진수 숫자가 있어야 합니다. 십진수 소숫점은 대문자 혹은 소문자 e로 지수 표현이 가능합니다.

* 1.25e2 는 1.25 x 10^2 혹은 125.0 을 의미 합니다.
* 1.25e-2 는 1.25 x 10^-2 혹은 0.0125 를 의미 합니다.

16진수의 지수 표현은 2^exp 를 기본으로 사용 합니다.

* 0xFp2 는 15 x 2^2 혹은 60.0 을 의미합니다.
* 0xFp-2 는 15 x 2^-2 혹은 3.75 를 의미 합니다.

아래에 소숫점 리터럴들은 전부 12.1875를 나타 냅니다.

{% highlight swift %}
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
{% endhighlight %}

숫자 리터럴들은 읽기 쉽기 위해 추가 표현이 가능합니다.  추가적으로 0을 넣거나, underscores (언더바 _) 를 넣을 수 있습니다.

{% highlight swift %}
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
{% endhighlight %}

## Numeric Type Conversion (숫자 타입 전환)
대부분의 integer 상수나 변수들은 음수가 아니라는것을 알면서도 Int 타입을 사용합니다.  하고 있는 작업을 위해 명확하게 필요 할때나, 외부 소스의 명확한 사이즈 데이터 혹은 메모리나 퍼포먼스등을 위해서나 다른 타입의 integer 를 사용하게 됩니다.

### Integer Conversion

Integer 상수나 변수의 숫자 타입에 따라 저장되는 범위가 다릅니다. Int8 상수나 변수는 -128 과 127 사이의 숫자들을 저장할 수 있습니다. UInt8 상수나 변수는 0 하고 255 사이의 숫자들을 저장할 수 있습니다.  상수나 변수에 들어가는 숫자가 범위를 벗어나게 되면 컴파일시 에러가 보고 됩니다.

{% highlight swift %}
let cannotBeNegative: UInt8 = -1
// UInt8 는 음수를 저장할 수 없습니다. 그래서 해당 코드는 에러가 나옵니다.
let tooBig: Int8 = Int8.max + 1
// Int8 는 최대 값을 넘어서 저장할 수 없습니다. 그래서 해당 코드는 에러가 나옵니다.
{% endhighlight %}

각 숫자 유형은 다른 값 범위를 저장할 수 있기 때문에 상황에 따라 숫자 유형 변환을 선택해야합니다. 이 옵트 인 방식은 숨겨진 변환 오류를 방지하고 코드에서 유형 변환 의도를 명확하게 나타냅니다.

아래 예제에서 상수 twoThousand는 UInt16 유형이고 상수는 UInt8 유형입니다. 같은 유형이 아니기 때문에 직접 추가 할 수 없습니다. 대신이 예제에서는 UInt16 (one)을 호출하여 새로운 Uint16 을 one 을 초기값으로 생성하고, 기존값을 대체 합니다.

{% highlight swift %}
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
{% endhighlight %}

SomType(ofInitialValue) 는 Swift 에서 기본적인 초기화 방법 입니다.

### Integer And Floating-Point Conversion

정수와 소숫점 사이에 변환 명시적 이어야 합니다.

{% highlight swift %}
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi 는 3.14159 와 같고 ,  Double 타입으로 추론 합니다.
{% endhighlight %}

{% highlight swift %}
let integerPi = Int(pi)
// integerPi 는 3 이고, Int 타입으로 추론 합니다.
{% endhighlight %}

Integer 값으로 초기화가 된다면 소숫점 값들은 버리게 됩니다. 즉, 4.75 는 4가 되고 -3.9 는 -3 이 됩니다.

## Type Aliases
Type Aliases 는 현재 사용되는 타입의 선택적인 이름을 정의합니다.  typealias 키워드를 이용해서 Type Aliase 정의가 가능합니다.

Type Aliases 는 기존이 타입을 좀더 명확한 이름으로 인용하여 사용할 수 있습니다.

{% highlight swift %}
typealias AudioSample = UInt16
var maxAmplitudeFound = AudioSample.min
// maxAmplitudeFound 는 0 입니다.
{% endhighlight %}

여기서, AudioSampe 은 Uint16 의 다른 이름입니다. AudioSample.min 은 실제적으로는 UInt16.min 을 호출하게 됩니다.

## Booleans
Swift 는 Bool 이라는 기본적인 Boolean 타입을 가지고 있습니다.  Swift 의 Boolean 상수값인 true 와 false 를 제공합니다.

{% highlight swift %}
let orangesAreOrange = true
let turnipsAreDelicious = false
{% endhighlight %}

Boolean 값은 특히 if 문같은 조건문에서 유용하게 쓰입니다.

{% highlight swift %}
if turnipsAreDelicious {
print("Mmm, tasty turnips!")
} else {
print("Eww, turnips are horrible.")
}
{% endhighlight %}

## Tuples
Tuples 그룹은 여러개의 값들을 하나의 복합적인 값으로 표현 합니다. tuple 내의 값은 어떤 타입이라도 될 수 있고 서로 같은 타입 일 필요는 없습니다.

{% highlight swift %}
let http404Error = (404, "Not Found")
// http404Error 는 (Int, String) 타입입니다.
{% endhighlight %}

그리고, tuple 의 내용들을 각각 상수나 변수로 분해 할수도 있습니다.

{% highlight swift %}
let (statusCode, statusMessage) = http404Error
print("The status code is \(statusCode)")
// Prints "The status code is 404"
print("The status message is \(statusMessage)")
// Prints "The status message is Not Found
{% endhighlight %}

만약 tuple 내의 값들중에 일부만 필요 하다면, underscore (_) 을 이용하여 무시 할수 있습니다.

{% highlight swift %}
let (justTheStatusCode, _) = http404Error
print("The status code is \(justTheStatusCode)")
// Prints "The status code is 404
{% endhighlight %}

각 Element 값들은 Index 번호를 이용하여 접근할 수도 있습니다.

{% highlight swift %}
print("The status code is \(http404Error.0)")
// Prints "The status code is 404"
print("The status message is \(http404Error.1)")
// Prints "The status message is Not Found
{% endhighlight %}

각 Element 들의 고유의 이름을 지정할 수도 있습니다.

{% highlight swift %}
let http200Status = (statusCode: 200, description: "OK")
{% endhighlight %}

그리고, 이름을 사용하여 해당 값을 접근할 수도 있습니다.

{% highlight swift %}
print("The status code is \(http200Status.statusCode)")
// Prints "The status code is 200"
print("The status message is \(http200Status.description)")
// Prints "The status message is OK
{% endhighlight %}

---
