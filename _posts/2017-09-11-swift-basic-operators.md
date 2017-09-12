---
layout: post
title: Swift - Basic Operators
excerpt: Swift 3 - 기본 연산자들
comments: true
tags: [ios, Swift, operator, 연산자] 
---

안녕하세요. iOS 개발자 엔비냥 입니다.
이번에는 Basic Operators 챕터를 번역 하려고 합니다.  오역이나 오타가 있으면 댓글로 부탁드립니다.

---

연산자 (operator) 는 값을 검사, 변경 혹은 합쳐주는 특별한 심볼 혹은 어법 입니다. 예를 들어, let i = 1 + 2 에서의 덧셈 연산자 (+) 는 2개의 숫자들을 더해 줍니다. 그리고,  If enteredDoorCode && passedRetinaScan 에서의 AND 연사자 (&&) 는 두개의 Boolean 값들을 합쳐 줍니다.

Swift 는 C 기본 연산자의 대부분을 지원하고, 일반적인 코딩 오류를 제거하는 몇 가지 기능을 향상 시켰습니다.  같음 연산자 (==) 대신에실수로 사용되는것을 막아주기 위해 대입 연산자 (=) 는 값을 반환하지 않습니다.

산술 연산자 (+, -, *, /, % 등)는 값 오버플로를 감지하고 허용하지 않으므로 숫자를 처리 할 때 예상치 못한 결과가 발생하지 않도록합니다.  Swift의 오버플로우 연사자들을 사용하여 값 오버플로우 상태를 선택할 수 있습니다. (오버플로우 연산자 파트에서 더 자세히 설명 하도록 하겠습니다.)

Swift 는 C에 없는 2개 숫자의 범위 연산자를 제공 하고 있습니다. (a..<b 와 a…b)

이 챕터에서는 Swift 의 기본적인 연산자들을 설명합니다. Advance Operators 에서 좀더 스위프트의 고급 연산자에 대해 설명 할 것 입니다.

## Terminology 

연산자들은 단일, 바이너리 (이항) 혹은 터너리 (삼항) 이 있습니다.

* 단일 연산자 (-a 같은) 는 하나의 타겟에 작용 합니다.  !b와 같이 단일 prefix 연산자는 타겟의 바로 앞에 적어줍니다.  그리고, c! 와 같은 단일 postfix 연산자는 타겟의 바로 뒤에 적어줍습니다.
* 바이너리 (이항) 연산자들 (2 +3 같은) 은 2개의 타겟들에게 작용 됩니다. 이것들은 2개의 타겟의 사이에 있기때문에 infix 라고 합니다. 
* 터너리 (삼항) 연산자들은 3개의 타겟 사이에 작용 합니다. Swift 에서는 단 하나의 터너리 연산자가 있습니다. (a ? b : c)

## Assignment Operator

대입 연산자 (a = b) 는 b의 값으로 a의 값을 초기화 혹은 업데이트 해줍니다.

{% highlight swift %}
let b = 10
var a = 5
a = b
// a의 값은 10 입니다.
{% endhighlight %}

만약 오른쪽값이 여러 값의 tuple 로 할당된다면, 각각 요소들이 여러 상수나, 변수에 한번에 할당 됩니다.

{% highlight swift %}
let (x, y) = (1, 2)
// x 는 1 , y 는 2 로 할당 됩니다.
{% endhighlight %}

C 와 Objective-C 와 다르게 Swift 의 대입 연산자 에서는  그 자체로 값을 반환 하지 않습니다. 그래서 다음의 문구는 유효하지 않습니다.

{% highlight swift %}
if x = y {
// x = y 는 값을 반환 하지 않기 때문에 유효하지 않습니다. 
}
{% endhighlight %}

## Arithmetic Operators

Swift 는 기본적인 4가지 산술 연산자를 지원합니다.

* 덧셈 (+)
* 뺄샘 (-)
* 곱셈 (*)
* 나눗셈 (/)

{% highlight swift %}
1 + 2 		// = 3
5 - 3 		// = 2
2 * 3 	 	// = 6
10.0 / 2.5	// = 4.0
{% endhighlight %}

C 와 Objective-C 와는 다르게, Swift 의 산술 연산자들은 기본적으로 값에 대한 오버플로우를 지원하지 않습니다. 값의 오버플로우를 사용하려면 overflow 연산자들 ( a &+ b 와 같은) 사용해야 합니다. 

덧셈 연산자는 String 연결에도 지원 합니다.

{% highlight swift %}
"hello, " + "world" // "hello, world"
{% endhighlight %}

## Remainder Operator

나머지 값을 구하는 연산자 (a % b) 는 a에 얼마나 많은 b의 배수가 들어가고 남은 값 (나머지 값)을 반환합니다.

> reminder operator 는 다른 언어에서 modulo operator 라고 알려져 있습니다.

{% highlight swift %}
9 % 4 // = 1
- 9 % 4 // = -1
{% endhighlight %}

첫번째 라인에서 9를 4의 2배수가 들어가게 채우고 난, 나머지 1이 반환 됩니다. 즉, *a = (b x 배수) + 나머지* 에 대한 나머지를 반환 하게 됩니다.

두번째 라인의 음수에서는 -9 = (4 * -2) + -1 과 같고 나머지인 -1 을 반환 합니다.

## Unary Minus Operator 

숫자의 앞에 - 의 사이 붙을수 있는데, 이것을 단일 마이너스 연산자라고 합니다.

{% highlight swift %}
let three = 3
let minusThree = -three 		// minusThree 는 -3 입니다.
let plusThree = -minusThree	// plusThree 는 3 혹은 "마이너스 마이너스 three" 입니다.
{% endhighlight %}

단일 마이너스 연산자 (-) 는 빈칸 없이 값의 바로 앞에 붙여 집니다. 

## Unary Plus Operator 

단일 플러스 연산자 (+) 는 변화없이 값 자체를 반환 해줍니다.

{% highlight swift %}
let minusSix = -6
let alsoMinusSix = +minusSix // alsoMinusSix 는 -6 입니다.
{% endhighlight %}

## Compound Assignment Operators

C에서와 같이, Swift 에서는 다른 연산자와 대입 연산자 (=)를 합쳐서 사용하는 복합 대입 연산자를 제공합니다. 

{% highlight swift %}
var a = 1
a += 2
// a 는 3 입니다.
{% endhighlight %}

a += 2 라는 표현은 a = a + 2 의 간단하게 적은 방법 입니다.  덧셈과 대입 을 하나의 연산자로 합치면서 더 효과적으로 한번에 실행 할 수 있습니다.

> 복합 대입 연산자는 값을 반환하지 않습니다. 즉, let b = a += 2 라고 사용할 수 없습니다.

## Comparison Operators 

Swift 에서는 모든 C 의 기본 비교 연산자들을 제공합니다.

* 같다 ( a == b )
* 다르다 ( a != b )
* .. 보다 크다 ( a > b )
* .. 보다 작다 ( a < b )
* .. 보다 같거나 크다 ( a >= b )
* .. 보다 같거나 작다 ( a <= b )

> Swift 에서는 2개의 Identity (동일) 연산자 (=== & !==) 를 제공합니다. 이 연산자는 두 개의 객체 참조가 모두 동일한 객체 인스턴스를 참조하는지 여부를 테스트하는 데 사용됩니다. 

각 비교 연산자들은 성공인지 실패인지 Bool 값을 반환 합니다.

{% highlight swift %}
1 == 1 // true
2 != 1 // true
2 > 1 // true
1 < 2 // true
1 >= 1 // true
2 <= 1 // false
{% endhighlight %}

비교 연산자들은 if 문 같은 조건문에서 때때로 사용 됩니다.

{% highlight swift %}
let name = "world"
if name == "world" {
print("hello, world")
} else {
print("I'm sorry \(name), but I don't recognize you")
}
// name 과 "world" 는 같기 떄문에 "hello, world" 가 프린트 됩니다.
{% endhighlight %}

비교 할 수 있는한, 동일한 수 값을 가지고 있는 tuple들도 비교 할 수 있습니다. 예를들어 (Int, String) 타입의 tuple에서 Int 와 String 둘 다 비교 할 수 있습니다.  그러나, Boolean 값을 가지고 있는 tuple 에서는 Bool 값을 비교 할 수 없습니다.

{% highlight swift %}
(1, "zebra") < (2, "apple")   // true, 1 은 2보다 작고, zebra 와 apple 은 비교가 되지 않습니다.
(3, "apple") < (3, "bird")    // true, 3은 3이랑 같고, apple 은 bird 보다 작습니다.
(4, "dog") == (4, "dog")      // true, 4는 4와 같고, dog 는 dog 랑 같습니다.
{% endhighlight %}

> Swift 기본 라이브러리에는 tuple 비교는 7개 미만의 요소들만 비교 할 수 있습니다. 만약 7개 이상의 값들을 비교 하려면, 직접 비교 연산자를 제공 해야 합니다.

## Ternary Conditional Operator

삼항 조건 연산자는 (question ? answer1 : answer2) 에서 3개의 파트를 사용하는 특별한 연산자 입니다.  이것은 quesion 이 true 인지 false 인지 두 표현중 하나를 구하는 줄임 표현 입니다. 만약 question 이 true 이면 answer1 을 구하고 해당 값을 반환 합니다. 그렇지 않으면 answer2 를 구하고 해당 값을 반환 합니다.

{% highlight swift %}
if question {
answer1
} else {
answer2
}
{% endhighlight %}

## Nil-Coalescing Operator

Nil-Coalescing 연산자 ( a ?? b ) 는 optional a 를 언랩하여, 만약 a 가 nil 이면 b 를 기본값으로 반환 합니다. 여기서 a 는 optional type 이어야 합니다.
Nil-Coalescing 연산자는 해당 코드의 줄임 표현 입니다.

{% highlight swift %}
a != nil ? a! : b
{% endhighlight %}

## Range Operators

Swift 는 2가지의 범위 연산자를 가지고 있습니다. 

### Closed Range Operator

Closed 범위 연산자 ( a…b ) 는 a에서 b까지 실행되고 a와 b 값을 포함하는 범위를 정의합니다. a의 값은 b보다 커야합니다.

Closed 범위 연산자는  for-in 루프문 에서 유용하게 사용 됩니다.

{% highlight swift %}
for index in 1...5 {‘
print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
{% endhighlight %}

### Half-Open Range Operator

Half-Open 범위 연산자 ( a..<b ) 는 b가 포함되지 않는 a 에서 b 까지 실행 되는 범위를 정의 합니다. half-open 범위 연산자는 첫번째 값은 포함하나 마지막 값은 포함하지 않는것을 이야기 합니다.

{% highlight swift %}
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..<count {
print("Person \(i + 1) is called \(names[i])")
}
// Person 1 is called Anna
// Person 2 is called Alex
// Person 3 is called Brian
// Person 4 is called Jack
{% endhighlight %}

## Logical Operators

논리 연산자들은 Boolean 값들을 합치거나 변경 합니다. Swift 는 C 언어 베이스의 4개의 기본적인 논리 연산자들을 제공합니다.

* Logical NOT (!a)
* Logical AND (a && b)
* Logical OR (a || b)

### Logical Not Operator

Logical Not 연산자 (!a) 는 Boolean 값 즉, true 를 false로, false를 true로 바꾸어 놓습니다. Logical Not 연산자는 값 앞에 적고, “not a” 라고 읽습니다.

### Logical AND Operator

Logical AND 연산자 ( a && b ) 는 양쪽 값들이 모두 true 이면 true 값을 반환 합니다. 만약 한쪽이라도 false 라면, 표현식의 마지막에는 false 로 나타냅니다.

### Logical OR Operator

Logical OR 연산자 ( a || b ) 는 2개의 파이프 케릭터들로 이루어 집니다.  둘중 한쪽만 true 이면 이 표현식에서는 true 로 나타냅니다.

{% highlight swift %}
let hasDoorKey = false
let knowsOverridePassword = true
if hasDoorKey || knowsOverridePassword {
print("Welcome!")
} else {
print("ACCESS DENIED")
}
// Prints "Welcome!
{% endhighlight %}

### Combining Logical Operators

여러개의 논리 연산자들을 합쳐서 복합적인 표현식을 만들 수 있습니다.

{% highlight swift %}
if enteredDoorCode && passedRetinaScan || hasDoorKey || knowsOverridePassword {
print("Welcome!")
} else {
print("ACCESS DENIED")
}
// Prints "Welcome!"
{% endhighlight %}

### Explicit Parentheses

표현식이 쉽게 읽혀지지 않거나 정확하지 않을때 괄호를 이용하는것이 때때로 유용하게 사용할 수 있습니다.

{% highlight swift %}
if (enteredDoorCode && passedRetinaScan) || hasDoorKey || knowsOverridePassword {
print("Welcome!")
} else {
print("ACCESS DENIED")
}
// Prints "Welcome!"
{% endhighlight %}

