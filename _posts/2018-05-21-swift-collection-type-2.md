---
layout: post
title: Swift - Collection Types (2)
excerpt: Swift - Set
comments: true
tags: [ios, Swift, Collection Type, Set]
---

안녕하세요. iOS 개발자 엔비냥 입니다.

이번글은 Collection Types 에서 Set 부분에 대해 번역 했습니다. 혹시 오역이나 오타, 필요한 부분이 있다면 댓글 부탁드립니다.

---

# Sets

Set 은 컬렉션에서 순서 없이 같은 타입의 확실한 값들을 저장 합니다.  아이템들의 순서가 중요하지 않거나 아이템이 오직 하나만 있어야만 할때 Array 대신에 Set 을 사용할 수 있습니다.

>  Swift의 Set 타입은 Foundation 의 NSSet 클래스에 연결되어 있습니다.

###  Hash Values for Set Types

 Set 에 저장되는 타입은 그 자체로 해쉬 값으로 계산할 수 있게 제공 되는 타입, 즉 Hashable 이어야 합니다. 해시 값은 `a == b` 이면 `a.hashValue == b.hashValue` 와 같이 동일하게 비교되는 모든 객체에 대해 동일한 Int 값입니다.

모든 Swift 기본 타입들 (String, Int, Double, 그리고, Bool) 은 기본적으로 hashable 이고, value 타입과 Key 타입들로 사용할 수 있습니다.

연관값 (associated values) 이 없는 조합 열거형 (Enumeration) case의 값들도 기본적으로 hashable 입니다.

### Set Type Syntax

Swift의 Set 은 예를들어, Element 라는 타입을 Set 에 저장할 수 있게 허용한다면,   `Set<Element>` 으로 적을 수 있습니다. Set 은 배열과 다르게 축약형 (shorthand form)[^1] 이 없습니다.

### Creating and Initializing an Empty Set

해당 initializer syntax를 이용하여 확실한 타입의 빈 set 을 생성할 수 있습니다.

{% highlight swift %}
var letters = Set<Character>()
print("letters is of type Set<Character> with \(letters.count) items.")
// "letters is of type Set<Character> with 0 items."
{% endhighlight %}

양자택일로, 만약  함수 인자 나 이미 타입이 정의된 변수/상수 처럼 상황이 이미 타입 정보를 제공하고 있다면, 빈 배열 리터럴 (empty array literal) 로 빈 set 을 생성할 수 있습니다.

{% highlight swift %}
lettters.insert("a")
// letters 는 이제 1개의 Character 타입을 가지고 있습니다.
letters = []
// letters 는 이제 빈 set 이지만, 계속 Set<Character> 타입 입니다.
{% endhighlight %}

### Creating a Set with an Array Literal

약칭으로 하나 혹은 여러개의 값들을 적는 배열 리터럴 (Array Literal) 으로 set 을 초기화 할수 있습니다.

{% highlight swift %}
var favoriteGenres : Set<String> = ["Rock", "Classical", "Hiphop"]
// favoriteGenres 는 3개의 아이템으로 초기화 되었습니다.
{% endhighlight %}

favoriteGenres 변수는 `Set<String>` 이라고 적고, String 값들의 Set 으로 선언 되었습니다. 이 Set 은 String 타입의 값들로 지정되어 있기 때문에, 오직 String 값들만 저장할 수 있습니다. 여기, favoriteGenres set 은  String 값들 ("Rock", "Classical", "Hiphop”) 배열 리터럴로 적어서 초기화 되었습니다.

>  favoriteGenres set 은 추가 하거나 제거 할 수 있기 때문에, 상수 (let) 가 아닌 변수 (var) 로 선언되었습니다.

Set 타입은 배열 리터럴 하나로는 추론 할 수 있습니다. 그래서, set 타입은 명시적으로 선언해 주어야 합니다. 그러나, Swift의 타입 추론 때문에, 같은 타입의 값들로 포함된 배열 리터럴로 초기화 한다면, 해당 set 의 타입을 적지 않아도 됩니다.  

favoriteGenres 의 초기화 는 이렇게 약식으로 적을 수 있습니다 :

{% highlight swift %}
var favoriteGenres: Set = ["Rock", "Classical", "Hiphop"]
{% endhighlight %}

배열 리터럴 안에 모든 값들은 다 같은 타입이어서, Swift 는 favoriteGenres 변수에 대해 Set<String> 타입으로 추론할 수 있습니다.

### Accessing and Modifying a Set

해당 메소드와 프로퍼티들을 통하여 Set 에 접근과 수정이 가능합니다.
읽기 전용인 *count* 프로퍼티를 통하여 Set 안에 아이템들의 숫자를 찾을 수 있습니다.

{% highlight swift %}
print("I have \(favoriteGenres.count) favorite music genres.")
// "I have 3 favorite music genres. 가 출력 됩니다.
{% endhighlight %}

Count 가 0 인지 체크할때에는 Boolean *isEmpty* 프로퍼티를 사용합니다.

{% highlight swift %}
if favoriteGenres.isEmpty {
    print("As far as music goes, I'm not picky.")
} else {
    print("I have particular music preferences.")
}
// "I have particular music preferences." 가 출력 됩니다.
{% endhighlight %}

Set 의 *insert(_:)* 메소드를 불러서 새로운 아이템을 추가 할 수 있습니다.

{% highlight swift %}
favoriteGenres.insert("Jazz")
// favoriteGenres 은 이제 4개의 아이템을 가지고 있습니다.
{% endhighlight %}

해당 Set 의 멤버 라면 Set의 *remove(_:)* 메소드를 불러서 아이템을 제거 할 수 있고, 해당 제거한 값을 리턴하거나 만약 포함되있지 않으면 nil 을 리턴 합니다. 모든 아이템을 제거 하려면 *removeAll()* 메소드를 이용하여 제거 할 수 있습니다.

{% highlight swift %}
if let removedGenre = favoriteGenres.remove("Rock") {
    print("\(removedGenre)? I'm over it.")
} else {
    print("I never much cared for that.")
}
// "Rock? I'm over it." 가 출력 됩니다.
{% endhighlight %}

어떠한 아이템이 포한되어 있는지 체크 하려면 *contains(_:)* 메소드를 이용합니다.

{% highlight swift %}
if favoriteGenres.contains("Funk") {
    print("I get up on the good foot.")
} else {
    print("It's too funky in here.")
}
// "It's too funky in here." 가 출렵 됩니다.
{% endhighlight %}

### Iterating Over a Set

*for-in* 루프를 이용하여 Set 의 값들을 반복할 수 있습니다.

{% highlight swift %}
for genre in favoriteGenres {
    print("\(genre)")
}
// Jazz
// Hip hop
// Classical
{% endhighlight %}

*for-in* 루프에 대해서는 다음에 For-In Loops 에서 다루도록 하겠습니다.

Swift의 Set 타입은 순서를 가지고 있지 않습니다.  명확한 순서로 set 을 값들을 반복하러면, set의 < 연산자를 이용하여 정렬된 배열로 리턴되는 *sorted()* 메소드를 사용합니다.

{% highlight swift %}
for genre in favoriteGenres.sorted() {
    print("\(genre)")
}
// Classical
// Hip hop
// Jazz
{% endhighlight %}

## Performing Set Operations

두 Set 을 함께 결합하거나, 두 Set 가 공통으로 갖고있는 값을 판별하거나, 두 Set 에 동일한 값이 모두 혹은 일부가 들어 있는지 여부를 판별하는 것과 같은 기본 Set 에 대한 조작을 효율적으로 수행 할 수 있습니다.

## Fundamental Set Operations

아래 그림은  두 Set *a와 b* 에 대해 음영 처리 된 영역으로 표시된 다양한 Set 연산의 결과들을 보여줍니다.

![]({{ site.url }}/img/swift/collection_2.png)

* *intersection(_:)* 메소드를 이용하여 두 Set 모두 포함된 값들로만 이루어진 새로운 Set 을 만들어 줍니다. (교집합)
* *symmetricDifference(_:)* 메소드를 이용하여 두 Set 에 한쪽에만 있는 값들로만 이루어진 새로운 Set 을 만들어 줍니다. (대칭 차집합)
* *union(_:)* 메소드를 이용하여 두 셋의 모든값을 합한 새로운 Set 을 만들어 줍니다. (합집합)
* *subtracting(_:)* 메소드를 이용하여 해당 Set 에 없는 값들로 새로운 Set 을 만들어 줍니다. (차집합)

{% highlight swift %}
let oddDigits: Set = [1, 3, 5, 7, 9]
let evenDigits: Set = [0, 2, 4, 6, 8]
let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]

oddDigits.union(evenDigits).sorted()
// [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
oddDigits.intersection(evenDigits).sorted()
// []
oddDigits.subtracting(singleDigitPrimeNumbers).sorted()
// [1, 9]
oddDigits.symmetricDifference(singleDigitPrimeNumbers).sorted()
// [1, 2, 9]
{% endhighlight %}

## Set Membership and Equality

아래 그림은 Set 간에 공유되는 요소를 나타내는 겹치는 영역이있는 세 세트 *a, b 및 c* 를 나타냅니다. a는 집합 b의 수퍼 집합입니다. 왜냐하면 a에 b의 모든 요소가 포함되어 있기 때문입니다. 반대로, 집합 b는 집합 a의 부분 집합입니다. 왜냐하면 b의 모든 요소도 a에 포함되기 때문입니다. 집합 b와 집합 c는 공통적 인 요소를 공유하지 않기 때문에 서로 분리되어 있습니다.

![]({{ site.url }}/img/swift/collection_3.png)

* is Equal 연산자 (==) 를 사용하여 두 Set 가 모두 같은 값을 가지고 있는지 측정할 수 있습니다.
* *isSubset(of:)* 메소드로 Set 의 모든 값들이 해당 Set 에 포함되어 있는지 측정할 수 있습니다.
* *isSuperset(of:)* 메소드로 Set 에 해당 Set 의 값들이 모두 포함되어 있는지 측정할 수 있습니다.
* *isStrictSubset(of:)* 혹은 *isStrictSuperset(of:)* 메소드로 Set 이 해당 Set 과 같지 않고, 부분집합 혹은 슈퍼세트 인지 측정할 수 있습니다.
* *isDisjoint(with:)* 메소드로 두 Set 가 공통의 값이 없는지 측정할 수 있습니다.

{% highlight swift %}
let houseAnimals: Set = ["🐶", "🐱"]
let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let cityAnimals: Set = ["🐦", "🐭"]

houseAnimals.isSubset(of: farmAnimals)
// true
farmAnimals.isSuperset(of: houseAnimals)
// true
farmAnimals.isDisjoint(with: cityAnimals)
// true
{% endhighlight %}


[출처]: Apple Inc. ‘The Swift Programming Language (Swift 4.1).’ iBooks. https://itunes.apple.com/kr/book/the-swift-programming-language-swift-4-1/id881256329?mt=11

[^1]: Array<String> 의 축약형은 [String] 입니다.
