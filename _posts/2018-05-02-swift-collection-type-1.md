---
layout: post
title: Swift - Collection Types (1)
excerpt: Swift- Array
comments: true
tags: [ios, Swift, Collection Type, Array]
---

안녕하세요. iOS 개발자 엔비냥 입니다. 번역을 중간에 너무 쉬고 있었더니 벌써 Swift 4.1 버전이 나왔네요. 전에 번역한 부분은 크게 바뀐 부분이 없어서 그대로 두었습니다.

이번 글은 Collection Types 에서 Array 부분까지 번역한 부분입니다. 오역이나 오타, 필요한 부분이 있다면 댓글 부탁드립니다.

---

Swift 는 Arrays, Sets, 그리고, Dictionaries 라는 3가지 Collection 타입들을 제공합니다.  Array 들은 순서가 있는 값들의 컬렉션 입니다. Set 은 순서가 없는 중복이 없는 고유의 값들의 컬렉션 입니다. Dictionary 는 순서가 없는 Key-Value 조합의 컬렉션 입니다.

![]({{ site.url }}/img/swift/collection_1.png)

스위프트의 Arrays, Sets, 그리고, Dicionary 들은 항상 저장하는 값들과 키들의 타입들에 대해서 명확합니다. 즉, 이 말은 잘못된 타입의 값을 실수로 해당 컬렉션에 추가 할 수 없습니다. 또한, 이 말은 즉, 컬렉션에서 가져오는 값들의 타입을 확신할 수 있습니다.

## Mutability of Collections
만약 Array, Set 혹은 Dictionary 를 변수로 정하여 생성한다면, 해당 컬렉션은 가변적일 수  있도록 생성될 것 입니다. 이 말은, 컬렉션을 만든 이 후에 해당 컬렉션 안의 아이템에 대한 추가, 삭제, 변경을 할 수 있습니다. 만약 Array, Set, 혹은 Dictionary 를 상수로 부여한다면, 해당 컬렉션은 불변이고, 사이즈나 컨텐츠를 변경 할 수 없습니다.

## Arrays
배열은 같은 타입의 값들을 순서가 있는 리스트로 저장합니다. 배열에서는 같은 값이라도 다른 위치에 여러번 있을 수 있습니다.

`Swift의 Array 타입은 Foundation의 NSArray 클래스에 연결되어 있습니다.`

### Array Type Shorthand Syntax
Swift 배열 타입은 *Array<Element>* 로 쓰여집니다. 이것은 Element라는 배열 값들의 타입으로 저장이 가능하게 하는것을 나타냅니다. 또한 배열타입을 축약형, 즉 *[Element]* 라고 쓸수도 있습니다. 두개의 양식은 기능상 동일하더라도, 배열 타입을 언급할때 축약형을 사용하는것이 바람직합니다.

### Creating an Empty Array
정해진 타입의 빈 배열을 생성할때는 이니셜라이져 문법을 사용합니다 :

{% highlight swift %}
var someInts = [Int]()
print(“someInts는 [Int]타입이고, \(someInts.count)개의 아이템이 있다”)
//someInts 변수는 이니셜라이져를 보면 [Int] 라고 추론할 수 있습니다.
{% endhighlight %}

만약 상황이 함수 인자 혹은 타입이 지정된 상수/변수 같이 이미 타입의 정보를 제공하고 있다면, 빈 배열 리터럴 `[]` 으로 빈 배열을  생성할 수 있습니다.

{% highlight swift %}
someInts.append(3)
//someInts는 1개의 Int타입을 값을 가지고 있습니다.
someInts = []
//someInts는 이제 빈 배열입니다. 그러나 계속 [Int]형 입니다.
{% endhighlight %}

### Creating an Array with a Default Value

Swift의 배열 타입은 모든값이 같은 기본값으로 설정된 일정한 사이즈의 배열로 생성하는 이니셜라이져를 제공하고 있습니다. (repeating) 그리고, 새 배열안에 되풀이 되는 값들의 숫자를 제공하고 있습니다. (count)

{% highlight swift %}
var threeDoubles = Array(repeating: 0.0, count: 3)
//threeDoubles는 [Double] 타입이고 [0.0,0.0,0.0] 과 같습니다.
{% endhighlight %}

### Creating an Array by Adding Two Arrays Together

addition 연산자 (+) 로 호환되는 타입의 2개의 기존 배열을 합쳐서 새로운 배열을 생성할 수 있습니다. 새로운 배열의 타입은 합친 2개의 배열의 타입으로 추론할 수 있습니다.

{% highlight swift %}
var anotherThreeDoubles = Array(repeating:2.5, count:3)
var sixDoubles = threeDoubles + anotherThreeDoubles
//sixDoubles는 [Double] 타입으로 추론할 수 있고, [0.0,0.0,0.0,2.5,2.5,2.5] 와 같습니다.
{% endhighlight %}

### Creating an Array with an Array Literal

또한 간단한 방법으로 1개 혹은 배열같은 여러개의 값을 쓸수 있는 배열 리터럴을 이용하여 배열을 초기화 할 수 있습니다.  배열 리터럴은 콤마 (,) 로 나누고 대가로 쌍 [] 으로 둘러싼 값들의 리스트로 적을 수 있습니다.

`[value 1, value 2, value 3]`

{% highlight swift %}
var shoppingList: [String] = [“Eggs”, “Milk”]
//shoppingList는 2개의 아이템으로 초기화 되었습니다.
{% endhighlight %}

shoppingList 변수는 “String 값들의 배열” [String] 으로  선언되었습니다. 이 독특한 배열은 String 타입으로 지정되어 있음으로, String 값들만 저장되도록 허용합니다. 여기서 shoppingList 배열은 2개의 String 값들인 (“Eggs” 와 “Milk”) 을 배열 리터럴로 쓰여서 초기화가 됩니다.

이 경우, 배열 리터럴은 2개의 String 값 이외에 다른 어떤것도 포함하고 있지 않습니다.  

Swift의 타입 추론에게 감사할 것은, 배열 리터럴에 같은 타입의 값들로 초기화가 된다면 배열의 타입을 적을 필요가 없습니다.

`var shoppingList = [“Eggs”, “Milk”]`

모든 값들이 같은 타입 이기 때문에, Swift 는 shoppingList 변수가 정확한 타입인 [String] 로 추론 합니다.

### Accessing and Modifying an Array

메소드들과 프로퍼티들을 통하거나 subscript 문법을 사용하여 배열을 접근 및 수정을 합니다. 배열의 아이템 갯수를 찾을때, 읽음 전용 프로퍼티인 count 를 체크 합니다.

`print(“shoppingList는 \(shoppingList.count) 개의 아이템을 가지고 있습니다.”)`

 isEmpty 프로퍼티의 Boolean 을 사용하여 count 가 0인지 체크 합니다.

{% highlight swift %}
if shoppingList.isEmpty {
	print(“shoppigList 는 비어있습니다.”)
} else {
	print(“shoppigList 는 비어있지 않습니다.”)
}
{% endhighlight %}

배열의 append(_ :) 메소드를 이용하여 배열의 마지막에 새로운 아이템을 추가 할 수 있습니다.

`shoppingList.append(“Flour”)`

아니면, 배열에 하나 또는 여러개의 적합한 아이템들을 추가할때 += 연산자를 사용하여 추가 할 수 있습니다.

{% highlight swift %}
shoppingList += [“Baking Powder”] // 총 4개의 아이템을 포함
ShoppingList += [“Chocolate Spread”, “Cheese”, “Butter”] // 총 7개의 아이템을 포함
{% endhighlight %}

배열 이름 다음에 대가로 `[]`  안에 값의 인덱스를 넣는 Subscript 문법으로 배열에서 값을 꺼냅니다.

{% highlight swift %}
var firstItem = shoppingList[0]
//firstItem 은 “Eggs” 입니다.
{% endhighlight %}

 Subscipt 문법을 이용하여 인덱스 번호의 현재의 값을 바꿀수 있습니다.

{% highlight swift %}
shoppingList[0] = “Six eggs”
//이제 shoppingList 의 첫번째 아이템은 Eggs 가 아니라 Six eggs 입니다.
{% endhighlight %}

Subscript 문법을 사용할때, 지정한 인덱스가 유효해야 합니다. 예를 들어, `shoppingList[shoppingList.count] = “Salt”`는 배열의 마지막에 아이템을 추가 하려고 했지만, runtime 에러가 나옵니다.

또한 Subscript 문법을 이용하여 값들의 범의를 한번에 변경할 수 있습니다. 대체할 값 세트가 대체하려는 범위와 다른 길이 인 경우에도 가능합니다.

{% highlight swift %}
shoppingList[4..6] = [“Bannas”, “Apples”]
//shoppingList는 이제 6개의 아이템을 가지고 있습니다.
{% endhighlight %}

배열의 특정한 인덱스에 삽입하려면, 배열의 `insert(_:at:)` 메소드를 사용합니다.

{% highlight swift %}
shoppingList.insert(“Maple Syrup”, at:0)
//shoppingList 는 이제 7개의 아이템을 가지고 있습니다.
//Maple Syrup은 이제 리스트의 첫번째 아이템 입니다.
{% endhighlight %}

`insert(_:at:)` 메소드를 불러서 “Maple Syrup”의 값의 새 아이템을 shopping list 의 인덱스 0 즉 맨 처음에 삽입하게 됩니다.

비슷하게, 아이템을 제거하려면 배열의 `remove(at:)` 메소드를 사용합니다. 이 메소드는 지정한 인덱스의 아이템을 제거하고 제거된 아이템을 return 합니다. (Return된 값이 필요하지 않으면 무시할 수 있습니다.)

{% highlight swift %}
let mapleSyrup = shoppingList.remove(at:0)
//이제 인덱스 0번의 아이템은 제거되었습니다.
//shoppingList 는 이제 6개의 아이템을 가지고 있고 Maple Syrup은 없습니다.
//mapleSyrup 에는 제거된 “Maple Syrup” 라는 String 값을 가지고 있습니다.
{% endhighlight %}

만약 배열의 마지막 아이템을 제거하려면 remove(at:) 보다 `removeLast()` 메소드를 사용하여 배열의 count property에 질의를 할 필요 없습니다. remove(at:) 메소드 처럼 removeLast() 메소드도 제거된 아이템을 return 합니다.

{% highlight swift %}
let apples = shoppingList.removeLast()
//배열의 마지막 아이템은 제거되었습니다.
//shoppingList 는 이제 5개의 아이템들을 가지고 있고, apples 는 없습니다.
//apples 에는 제거된 “Apples” String 값을 가지고 있습니다.
{% endhighlight %}

### Iterating Over an Array

`for-in` 루프를 이용하여 배열의 배열의 모든 값의 세트를 반복 순회할 수 있습니다.

{% highlight swift %}
for item in shoppingList {
	print(item)
}
//Six eggs
//Milk
//Flour
//Baking Powder
//Bananas
{% endhighlight %}

 만약 각 아이템의 integer 인덱스가 필요하면 `enumerated()` 메소드를 사용하여 배열을 반복 순회할 수 있습니다. 각 배열의 아이템들은 `enumerated()` 메소드에서 integer 인덱스와 각 아이템을 이룬 tuple 을 return 합니다.

{% highlight swift %}
for (index, value) in shoppingList.enumerated() {
	print(“Item \(index + 1): \(value)”)
}
// Item 1: Six eggs
// Item 2: Milk
// Item 3: Flour
// Item 4: Baking Powder
// Item 5: Bananas
{% endhighlight %}

더 자세한 for-in 루프에 대해서는 다음 챕터인 Control Flow의 For-In Loops 에서 다루도록 하겠습니다.


[출처]: Apple Inc. ‘The Swift Programming Language (Swift 4.1).’ iBooks. https://itunes.apple.com/kr/book/the-swift-programming-language-swift-4-1/id881256329?mt=11
