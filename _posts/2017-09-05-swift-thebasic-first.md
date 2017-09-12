---
layout: post
title: Swift - The Basics (1)
excerpt: Swift 3.0.1 - The Basic (1)
comments: true
tags: [ios, Swift] 
---

안녕하세요. iOS 개발자 엔비냥 입니다.
Apple 에서 제공하고 있는 [Swift 3.0.1](https://itunes.apple.com/kr/book/the-swift-programming-language-swift-3-1/id881256329?mt=11) 문서를 번역하려고 합니다. 오역이 있으면 댓글 부탁드립니다.

--

Swift 는 iOS, MacOS, WatchOS & tvOS 어플리케이션 개발을 위한 새로운 프로그래밍 언어 입니다.  그럼에도 불구하고, Swift 의 많은 부분은 C 와 Objective-C 의 개발 경험에서 비롯 됩니다.

## Constants And Variables (상수와 변수)

상수는 변하지 않는 값을 가지고 있는 반면에 변수는 후에 다른 값을 가질수 있습니다.

## Declaring Constants and Variables (상수와 변수 선언)

상수는 let 키워드로 , 변수는 var 키워드로 선언을 하게 됩니다. 예를들어

{% highlight swift %}
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
{% endhighlight %}

이 코드에서, maximumNumberOfLoginAttempts 는 새로운 상수로 선언되었고, 값은 10을 나타 냅니다.  currentLoginAttempt 는 새로운 변수로 선언되고 처음 값은 0을 가지게 됩니다. (즉 currentLoginAttempt 는 추 후에 변할수 있는 값입니다.)

또한, 여러 상수들이나, 변수들을 콤마를 이용해서 한줄의 라인에 선언할 수 있습니다.

{% highlight swift %}
var x = 0.0, y = 0.0, z = 0.0
{% endhighlight %}

## Type Annotations (타입 명시)

상수나 변수 선언시 값에 대한 타입을 명시 할 수가 있습니다. 타입 명시는 콜론(:) 이후에 타입의 이름을 적으면 됩니다.

{% highlight swift %}
var welcomeMessage: String
{% endhighlight %}

이 변수는 welcomeMessage 이고 타입은 String 입니다. 즉, welcomeMessage 는 String 값을 가질수가 있습니다.

{% highlight swift %}
welcomeMessage = “Hello”
{% endhighlight %}

또한, 여러 같은 타입의 변수들을 한줄로 선언이 가능합니다.

{% highlight swift %}
var red, green, blue: Double
{% endhighlight %}

## Naming Constants and Variables (상수와 변수의 이름)

상수와 변수의 이름은 유니코드를 포함한 모든 케릭터들을 사용할 수 있습니다.

{% highlight swift %}
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow”
{% endhighlight %}

상수와 변수의 이름은 공백, 수학 기호, 화살표, 유효하지 않는 유니코드, 라인 (-) , 박스 드로잉 케릭터들([Box-drawing character - Wikipedia](https://en.wikipedia.org/wiki/Box-drawing_character))은 사용할 수 없습니다.
그리고, 숫자로는 시작할 수 없지만, 이름에 숫자가 포함될 수는 있습니다.

한번 선언된 상수나 변수는 같은 이름으로 재 선언 할 수 없고, 다른 타입으로 값으로 바꿀수 없습니다.

> Swift 에서 지정된 키워드와 같은 이름으로 상수나 변수를 만들때에는 backticks(`) 를 앞뒤로 붙여서 사용하면 됩니다.

## Printing Constants and Variables (상수와 변수의 프린팅)

상수와 변수의 값을 print(_:separator:terminator) 함수를 사용하여 프린트 할수 있습니다.

{% highlight swift %}
print(friendlyWelcome)
{% endhighlight %}

print(_:separator:terminator) 함수는 값을 출력할 수 있는 프린트 하는 글로벌 함수 입니다.  예를들어 Xcode 에서 print(_:separator:terminator) 함수를 사용하면 Xcode 콘솔창에 해당 값을 프린트 하게 됩니다.

print 함수를 호출 할때 separator 와 terminator 파라미터는 기본값을가지고 있어서 생략할 수 있습니다.

Swift  에서는 변수와 상수 이름 앞에 백슬래쉬와 가로를 이용하여 문자열 내에 삽입 할 수 있습니다. 

{% highlight swift %}
print(“The current value of friendlyWelcome is \(friendlyWelcom)”)
{% endhighlight %}

## Comments (주석)

주석을 사용하여 메모나 리마인드 용 문구를 실행되지 않도록 코드안에 적을수 있습니다. 

Swift 에 주석을 다는것은 C 언어와 비슷합니다. 한줄 주석은 2개의 슬래쉬를 이용합니다. (//)

{% highlight swift %}
// This is comment.
{% endhighlight %}

여러 줄의 주석은 시작 부분에 (/*) 을 끝 부분에 (*/) 을 사용하게 됩니다.

{% highlight swift %}
/* This is also a comment
but is written over multiple lines. */
{% endhighlight %}

## Semicolons (세미콜론)

많은 다른 언어들과는 다르게 Swift에서는 각 명령문 끝에 세미콜론 (;) 을 필요로 하지 않습니다.  만약 사용하기 원한다면 사용할 수도 있습니다. 혹은, 한 줄에 여러 명령문을 사용하려고 한다면 세미콜론 (;) 을 사용해야 합니다.

{% highlight swift %}
let cat = "🐱"; print(cat)
// Prints "🐱”
{% endhighlight %}

## Integers (정수)

Integer 는 42나 -23 처럼 분수를 포함하지 않은 모든 숫자들을 나타냅니다.  Integers 는 부호가 있거나 (signed) 부호가 없을 수 (unsigned) 있습니다.

Swift 에서는 8,16,32 그리고 64 비트의 signed & unsigned Integer 들이 제공 됩니다. Unsigned 8-bit Integer 는 UInt8 로 표현하고, signed 32-bit 는 Int32 로 표현 합니다.

## Integer Bounds (정수 범위)

min 과 max 프로퍼티를 이용하여 각 Integer 타입의 최소값과 최대값에 접근 할 수 있습니다.

{% highlight swift %}
let minValue = UInt8.min // minValue 는 0 입니다.
let maxValue = UInt8.max // maxValue 는 255 입니다.
{% endhighlight %}

## Int
코드에서 대부분의 케이스는 Integer의 사이즈를 설정 할 필요가 없습니다. Swift 는 Int 라는 타입을 제공하고, 해당 Integer는 현재 사용중인 플랫폼의 사이즈로 제공 하게 됩니다.

> 32 비트 플랫폼에서, Int 는 Int32 와 같습니다.
> 64 비트 플랫폼에서, Int 는 Int64 와 같습니다.

정확한 사이즈가 필요하지 않다면, Int 를 사용 합니다. 

## UInt
또한 Swift 에서는 Unit 키워드로 unsigned (부호가 없는) Integer 타입을 제공하고, 현재 사용중인 플랫폼의 사이즈로 제공하게 됩니다.

> 32 비트 플랫폼에서, UInt 는 UInt32 와 같습니다.
> 64 비트 플랫폼에서, Uint 는 UInt64 와 같습니다.

## Floating-Point Numbers (소숫점)

3.14159 , 0.1 그리고, -273.15 는 분수를 포함한 소숫점 입니다. Floating-Point 타입 들은 Integer 보다 더 많은 범위를 나타낼 수 있습니다. Swift 에서는 2가지 부호가 있는 Floating-Point 타입들이 있습니다.

> Double 은 64비트 Floating-Point 타입을 나타냅니다.
> Float 은 32비트 Floating-Point 타입을 나타냅니다.

## Type Safety and Type Inference (안전한 타입과 타입 추론)
Swift 는 type-safe 언어 입니다.  type safe 언어는 작업시에 값에대한 타입을 명확함을 주게 됩니다.  만약 코드중에, String 을 사용하는 부분에서 Int 를 넣는 실수를 하지 않게 됩니다.

타입 추론 (Type Inference) 는 특히 상수나 변수를 초기값을 가지고 선언할때 유용합니다. 

{% highlight swift %}
let meaningOfLife = 43
// meaningOfLife 는 Int 타입으로 추론하게 됩니다.
{% endhighlight %}

{% highlight swift %}
let pi = 3.14159
// pi 는 Double 타입으로 추론하게 됩니다.
{% endhighlight %}

Swift 에서는 Float 대신에 Double 로 타입 추론을 하게 됩니다.
만약 Integer 와 Floating-Point 를 합치게 되면 해당 타입은 Double 로 추론하게 됩니다.

{% highlight swift %}
let anotherPi = 3 + 0.14159
// anotherPi 는 Double 타입으로 추론하게 됩니다.
{% endhighlight %}

—

The Basics 가 내용이 길어서 나누어서 번역하겠습니다 ;)
