---
layout: post
title: Swift - Collection Types (3)
excerpt: Swift - Dictionary
comments: true
tags: [ios, Swift, Collection Type, Dictionary]
---

안녕하세요. iOS 개발자 엔비냥 입니다.

이번글은 Collection Types 에서 마지막으로 Dictionary 부분을 번역 했습니다. 혹시 오역이나 오타, 필요한 부분이 있다면 댓글 부탁드립니다.

---

# Dictionaries

Dictionary 는 컬렉션 안에 같은 타입의 키들과 같은 타입의 값들 사이의 연결된 값들을 순서 없이 저장합니다.

각 값들은 Dictionary 안에 값을 식별하도록 하는 유니크한 키와 연결 되어있습니다.

배열안의 아이템들과는 달리, Dictionary 안의 아이템들은 특정한 순서를 가지고 있지 않습니다. 우리가 실제 세상의 사전에서 단어를 찾는 방법처럼, Dictionary 는 식별자를 바탕으로 한 값들을 찾을때 사용합니다.

> Swift 의 Dictionary 타입은 Foundation 의 NSDictionary 클래스와 연결되어 있습니다.

## Dictionary Type Shorthand Syntax

Swift 의 Dictionary 타입은 *Dictionary<Key, Value>* 로 쓸 수 있습니다.
여기서 *Key* 는 Dictionary 의 키로 사용할 수 있는 값의 타입이고, *Value*  는 해당 키에 대해 Dictionary 에 저장하는 값들의 타입입니다.  

> Dictionary 의 Key 는 반드시 Hashable 프로토콜을 따라야 합니다.

Dictionary 의 축약형 (Shorthand Form) 으로 *[Key:Value]* 로  쓸 수 있습니다. 두 형태가 기능적으로 동일하더라도, 축약형이  선호되며, 이 책의 가이드에 종종 Dictionary의 타입을 인용 할 때 사용됩니다.

## Creating an Empty Dictionary

배열과 마찬가지로 초기화 Syntax로 어떤 타입의 빈 Dictionary 를 생성할 수 있습니다.

{% highlight swift %}
var namesOfIntegers = [Int: String]()
// namesOfIntegers 는 [Int: String] 빈 dictionary 입니다.
{% endhighlight %}

이 예제에서 Integer 값들의 human-readable 이름들을 저장할 수 있는 *[Int: String]* 타입의 Dictionary 를 생성합니다.  키들은 Int 타입이고 값들은 String 타입입니다.

만약 이미 타입 정보를 제공하고 있다면, 빈 딕셔너리 리터럴 / *[:]* / 을 이용하여 빈 Dictionary 를 생성할 수 있습니다.  

{% highlight swift %}
namesOfIntegers[16] = "sixteen"
// namesOfIntegers 는 이제 1 key-value 페어를 가지고 있습니다.
namesOfIntegers = [:]
// namesOfIntegers 는 다시 [Int: String] 타입의 빈 Dictionary 가 되었습니다.
{% endhighlight %}

## Creating a Dictionary with a Dictionary Literal

Dictionary 를 배열 리터럴과 비슷한 Syntax를 가진 Dictionary 리터럴를 이용하여 초기화 할 수 있습니다.  딕셔너리 리터럴은 하나 혹은 여러개의 Key-Value 페어를 적을 수 있는 축약 방법 입니다.

`[key 1: value 1, key 2: value 2, key 3: value 3]`

아래 예제에서는 국제 공항들의 이름들을 저장하는 Dictionary 를 생성 합니다. 이 Dictionary 에서, 키들은 국제 공항의 코드인 3개의 글자들이고, 값들은 공항의 이름들입니다.

{% highlight swift %}
var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
{% endhighlight %}

이 *airports* Dictionary 는 *[String:String]* 타입으로 선언 되어 있습니다. 이것은  */“ Dictionary 의 키들은 String 타입이고 값들의 타입도 String 입니다.”/* 를 의미 합니다.

이 *airports* Dictionary 는 2개의 Key-Value 페어를 포함한 Dictionary 리터럴로 초기화 되었습니다.  첫 페어의 키는 “YYZ” 이고 값은 “Toronto Pearson” 입니다. 두번째 페어는 “DUB” 라는 키를 가지고 있고, “Dublin” 이라는 값을 가지고 있습니다.

이 딕셔너리 리터럴은 2개의 *String:String* 페어를 가지고 있습니다.

배열과 마찬가지로, 일관된 키들과 값들의 Dictionary 리터럴로 초기화 할때 Dictionary 의 타입을 적을 필요가 없습니다.

{% highlight swift %}
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
{% endhighlight %}

왜냐하면, Dictionary 안에 모든 키들이 서로 같은 타입이고, 게다가 모든 값들도 서로 같은 타입이기 떄문에 Swift 는 airports 라는 Dictionary 에 대해 *[String:String]* 으로 추론할 수 있습니다.

## Accessing and Modifying a Dictionary

해당 메소드들과 프로퍼티들 혹은 subscript Syntax를 사용해서 Dictionary 에 접근 및 수정할 수 있습니다.

배열과 마찬가지로, Dictionary 안의 아이템 갯수를 읽기 전용인 *count* 프로퍼티를 체크 하여 찾을 수 있습니다.

{% highlight swift %}
print("The airports dictionary contains \(airports.count) items.")
// "The airports dictionary contains 2 items." 가 출력됩니다.
{% endhighlight %}

Boolean *isEmpty* 프로퍼티를 사용하여 count 프로퍼티가 0 인지 체크 할 수 있습니다.

{% highlight swift %}
if airports.isEmpty {
    print("The airports dictionary is empty.")
} else {
    print("The airports dictionary is not empty.")
}
// "The airports dictionary is not empty." 가 출력됩니다
{% endhighlight %}

Dictionary 에 Subscript Syntax 를 사용하여 새로운 아이템을 추가 할 수 있습니다. Subscript 인덱스로써 적절한 타입의 새로운 키를 사용하고, 적절한 타입의 새로운 값들을 할당할 수 있습니다.

{% highlight swift %}
airports["LHR"] = "London"
// airports dictionary 는 이제 3개의 아이템을 가지고 있습니다.
{% endhighlight %}

또한 Subscript Syntax 를 사용하여 개개의 키에 대한 값을 바꿀 수 있습니다.

{% highlight swift %}
airports["LHR"] = "London Heathrow"
// "LHR" 키에 대한 값이 "London Heathrow" 로 바뀌었습니다.
{% endhighlight %}

Subscript Syntax 대신에 Dictionary  의 *updateValue(_ :forKey:)* 메소드를 사용하여 개개의 키에 대한 값들을 세팅하거나 업데이트 할 수 있습니다. 만약 해당 키에 대한 값이 없다면 추가가 되고, 해당 키에 대한 값이 이미 있다면 업데이트가 될 것 입니다. Subscript 와 달리 *updateValue(_ :forKey:)* 메소드는 업데이트 이전의 값을 리턴해 줍니다.

*updateValue(_ :forKey:)* 메소드는 의 Value 타입의 Optonal 값이 리턴해 줍니다.

{% highlight swift %}
if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {
    print("The old value for DUB was \(oldValue).")
}
// "The old value for DUB was Dublin." 이 출력됩니다.
{% endhighlight %}

Subscript Syntax 를 이용하여 Dictionary 에서 개개의 키에 대한 값을 가져올 수 있습니다. 값이없는 키를 요청할 수 있으므로 Dictionary 는 Optional 값을 리턴해 줍니다. Dictionary에 요청 된 키의 값이 포함되어 있으면,  해당 키의 기존 값을 포함하는 Optional 값을 리턴해 줍니다. 그렇지 않으면,  nil을 리턴해 줍니다.

{% highlight swift %}
if let airportName = airports["DUB"] {
    print("The name of the airport is \(airportName).")
} else {
    print("That airport is not in the airports dictionary.")
}
// "The name of the airport is Dublin Airport." 가 출력됩니다.
{% endhighlight %}

Subscript Syntax 를 이용하여 nil을 대입하여 Dictionary 에서 Key-Value 페어를 제거 할 수 있습니다.

{% highlight swift %}
airports["APL"] = "Apple International"
// "Apple International" 는 실제 공항이 아니어서 삭제 해야 합니다.
airports["APL"] = nil
// APL 은 이제 Dictionary 에서 제거 되었습니다.
{% endhighlight %}

또한, *removeValue(forKey:)* 메소드를 이용하여 Dictionary 의 Key-Value 페어의 값을 제거 할수도 있습니다. 이 메소드는 만약 해당 키에 대한 값이 있다면 제거 된 값을 리턴해 줍니다. 만약 값이 없다면 nil 을 리턴해 줍니다.

{% highlight swift %}
if let removedValue = airports.removeValue(forKey: "DUB") {
    print("The removed airport's name is \(removedValue).")
} else {
    print("The airports dictionary does not contain a value for DUB.")
}
// "The removed airport's name is Dublin Airport." 가 출력됩니다.
{% endhighlight %}

## Iterating Over a Dictionary

*for-in* loop 를 이용하여 Dictionary 안의 Key-Value 페어들을 순환 할 수 있습니다. Dictionary 안의 각 아이템들은 *(key, value)* 튜플로 리턴해 줍니다.

{% highlight swift %}
for (airportCode, airportName) in airports {
    print("\(airportCode): \(airportName)")
}
// YYZ: Toronto Pearson
// LHR: London Heathrow
{% endhighlight %}

*for-in* 루프에 대해서는 다음에 For-In Loops 에서 다루도록 하겠습니다.

또한 키와 값 속성에 접근하여 Dictionary 의 키나 값의 반복 가능한 컬렉션을 검색 할 수 있습니다.

{% highlight swift %}
for airportCode in airports.keys {
    print("Airport code: \(airportCode)")
}
// Airport code: YYZ
// Airport code: LHR

for airportName in airports.values {
    print("Airport name: \(airportName)")
}
// Airport name: Toronto Pearson
// Airport name: London Heathrow
{% endhighlight %}

만약 Dictionary 의 키들 혹은 값들을 배열 인스턴스가 필요하다면, keys 와 Values 프로퍼티를 이용하여 새로운 배열로 초기화 할 수 있습니다.

{% highlight swift %}
let airportCodes = [String](airports.keys)
// airportCodes 는 ["YYZ", "LHR"] 입니다.

let airportNames = [String](airports.values)
// airportNames 는 ["Toronto Pearson", "London Heathrow"] 입니다.
{% endhighlight %}

Swift 의 Dictionary 타입은 순서를 가지고 있지 않습니다. Dictionary 의 키들 혹은 값들을 순환 할때 순서가 필요 하다면, keys 와 values 프로퍼티에 *sorted()* 메소드를 이용할 수 있습니다.


[출처]: Apple Inc. ‘The Swift Programming Language (Swift 4.1).’ iBooks. https://itunes.apple.com/kr/book/the-swift-programming-language-swift-4-1/id881256329?mt=11
