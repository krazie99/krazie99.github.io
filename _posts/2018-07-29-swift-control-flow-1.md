---
layout: post
title: Swift - Control Flow (1)
excerpt: 제어흐름
comments: true
tags: [ios, Swift, Control Flow, 제어흐름]
---

안녕하세요. iOS 개발자 엔비냥 입니다.  이번 장은 Swift 의 Control Flow (제어 흐름) 에서 반목문들을 번역 하였습니다. 혹시 오역이나 오타, 필요한 부분이 있다면 댓글 부탁드립니다.

---

Swift 는 다양한 제어문 (Control Flow Statements) 들을 제공하고 있습니다.   이중에는 작업에 대한 실행을 여러번 반복 실행하는  `while`  문 , 상황에 따라 코드가 분기되어 실행되는 `if` 문과 `guard` 문 그리고 `switch` 문, `break` 와`continue` 같이 실행 흐름을 코드의 또 다른 지점으로 옮겨주는 문법도 포함하고 있습니다.

Swift 는 또한 Array, Dictionary, Ranges, Strings, 그리고, 다른 시퀀스들을 쉽게 순회 할 수 있게 해주는 `for-in` 루프를 제공하고 있습니다.

Swift의 `switch` 문은 C 와 같은 언어에 있는 것들보다 상당히 더 강력합니다. Case 들은 많은 다른 패턴들과 매칭 될 수 있습니다. (Tuple 등)

`switch` 의 매칭된 값들은 본문내에서 사용하기 위해 임시 상수 혹은 변수에 바인딩 할 수 있으며, 복잡한 매칭 조건들은 각 case 에 대해 `where` 절로 표현 할 수 있습니다.

## For-In Loops
Array , 숫자들의 범위, 혹은 String 의 케릭터들과 같은 연속된 값들을 순회하기 위해 `for-in` 루프를 사용할 수 있습니다.

이 예제는 `for-in` 루프를 사용하여 배열의 아이템들을 순회합니다.

{% highlight swift %}
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    print("Hello, \(name)!")
}
// Hello, Anna!
// Hello, Alex!
// Hello, Brian!
// Hello, Jack!
{% endhighlight %}

Key-Value 페어를 접근하여 Dictionary 를 순회 할수 있습니다. Dictionary 를 순회 할때 각 아이템들은 `(key, value)` 의 튜플을 리턴해줍니다.`for-in` 루프 본문에서 사용하기 위해 명시 적으로 명명 된 상수로 `(key, value)` 튜플의 멤버를 분해 할 수 있습니다.

아래 예제 코드에서, Dictionary 의 키들은 `animalName` 이라는 상수로 분해 되었고, 값들은 `legCount` 라는 상수로 분해 되었습니다.

{% highlight swift %}
let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    print("\(animalName)s have \(legCount) legs")
}
// ants have 6 legs
// spiders have 8 legs
// cats have 4 legs
{% endhighlight %}

Dictionary 의 컨텐츠는 본래 순서가 없고, 해당 아이템들을 순회할때 순서에 대한 보장을 하지 않습니다. 특히, 항목을 Dictionary 에 삽입하는 순서가 반복되는 순서라고 정의하지 않습니다.  Array 와 Dictionary 에 대해 더 알기 위해서는 Collection Types 를 참고 하시기 바랍니다.

또한 숫자의 범위로 `for-in` 루프를 사용할 수 있습니다.

{% highlight swift %}
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
{% endhighlight %}

해당 예제에서 반복되는 시퀀스는 1에서 5사이의 숫자 범위 이고, Close Range Operator `(...)` 에 의해 표시합니다. *index* 값은  (1) 범위 의 첫 번째 숫자로 설정되고 루프 내부의 명령문이 실행됩니다. 이 경우, 루프에는 인덱스의 현재 값에 대한 5 배수의 테이블의 항목을 *print* 하는 명령문이 하나만 포함되어 있습니다. 명령문이 실행 된 후에는, Index 의 값은 (2) 범위에 있는 두번째 값으로 업데이트 되고, `print(_:separator:terminator:)`  함수가 다시 호출 됩니다. 이 프로세스는 범위의 마지막에 도달할때 까지 계속 됩니다.

위의 예제에서, *index* 는 각 이터레이션의 시작시 자동으로 값이 설정 됩니다. 따라서 *index* 가 사용되기 전에 선언 될 필요가 없습니다. let 키워드 선원이 필요 없이 루퍼 안에 암시적으로 선언 됩니다.

만약, 시퀀스의 각 값이 필요 없을때, 변수명에 밑줄 문자 (underscore) `(_)` 를 사용하여 무시 할 수 있습니다.

{% highlight swift %}
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}
print("\(base) to the power of \(power) is \(answer)")
// Prints "3 to the power of 10 is 59049
{% endhighlight %}

위의 예제는 한 숫자의 값을 다른 숫자의 제곱으로 계산합니다 (이 경우 3의 10의 제곱으로). 1 로 시작하고 10 으로 끝나는 *closed range* 를 사용하여, 시작 값 1 (즉, 0의 거듭 제곱에 3) 을 3 을 곱한 것을 열번 (ten times) 반복 합니다. 이 계산의 경우 개별 카운터는 루프를 통해 매번 값을 계산합니다.  루프 변수 대신 사용되 는 밑줄 문자 (underscore) `(_)` 는 개별 값을 무시하게하고 루프 반복 마다 현재 값에 대한 액세스를 제공하지 않습니다.

일부 상황에서는 두 끝점을 모두 포함하는 *closed range* 를 사용하지 않을 수도 있습니다. 시계에서 매 순간마다 tick marks 를 그린다고 생각합시다. 그리고, 0분에서 시작해서 60개의 tick marks 를 그리려고 합니다. 이때, 하한은 포함하지만 상한은 포함하지 않게 Half-Open Range Operator `(..<)` 를 사용합니다.

Ranges 에 대해 더 많은것들은 *Range Operators* 에서 살펴 보겠습니다.

{% highlight swift %}
let minutes = 60
for tickMark in 0..<minutes {
    // render the tick mark each minute (60 times)
}
{% endhighlight %}

어떤 사용자들은 그들의 UI 에서 몇개의 tick marks 만을 그리기 원할수 도 있습니다.  그들은 매 5분마다 1개의 mark 만 원합니다. 그렇다면, `stride(from:to:by:)` 함수를 사용하여 원하지 않는 mark 들을 건너 띌수 있습니다.

{% highlight swift %}
let minuteInterval = 5
for tickMark in stride(from: 0, to: minutes, by: minuteInterval) {
    // render the tick mark every 5 minutes (0, 5, 10, 15 ... 45, 50, 55)
}
{% endhighlight %}

또한 *Closed Ranges* 도 `stride(from:through:by:)` 를 사용하는것으로 가능합니다.

{% highlight swift %}
let hours = 12
let hourInterval = 3
for tickMark in stride(from: 3, through: hours, by: hourInterval) {
    // render the tick mark every 3 hours (3, 6, 9, 12)
}
{% endhighlight %}


## While Loops

while 루프는 조건이 false 가 될때까지 일련의 실행문들을 수행합니다. 이러한 종류의 루프는 첫 이터레이션 전에 반복 횟수를 알 수 없을 때 가장 잘 사용됩니다. Swift 는 두종류의 while 루프문을 제공합니다.

	* **while** 루프 동안 각 패스의 시작에서 조건을 평가합니다.
	* **repeat-while** 루프 동안 각 패스의 마지막에서 조건을 평가 합니다.

### While

while 루프는 하나의 조건으로 시작합니다. 만약 해당 조건이 true 라면, 조건이 false가 되기 전까지 일련의 실행문들을 반복 실행하게 됩니다.

이것이 기본적인 while 루프의 폼입니다.

{% highlight swift %}
while 조건 {
	실행문
}
{% endhighlight %}

이 예제는 간단한 Snakes and Ladders 라는 게임을 플레이하는것 입니다. (Chutes and Ladders 라고도 알려져 있습니다.)


![]({{ site.url }}/img/swift/controlflow_1.png)

게임의 룰은 아래와 같습니다.

	* 보드는 25 개의 정사각형을 가지고 있으며, 목표는 정사각형 25 위 또는 그 이상의 정사각형입니다.
	* 플레이어의 시작 사각형은 보드의 왼쪽 하단 모서리 바로 옆에있는 "제로 제곱 (square zero)"입니다.
	* 각 회전마다 6면 주사위를 굴려 위의 점선 화살표로 표시된 수평 경로를 따라 그 숫자만큼 움직입니다.
	* 당신의 차례가 사다리의 끝에서 끝나면, 그 사다리 위로 올라갑니다.
	* 네 차례가 뱀의 머리에서 끝나면 그 뱀의 아래로 움직입니다.

게임 보드는 **Int** 값들의 배열로 표현됩니다. 그 크기는 **finalSquare** 라는 상수를 기반으로 합니다. 이 상수는 배열을 초기화하고 나중에 예제에서 승리 조건을 확인하는 데 사용됩니다. 플레이어가 보드에서 시작하기 때문에 “square zero” 에서 보드는 25개가 아닌 26개의 Int 값 0 으로 초기화됩니다.

{% highlight swift %}
let finalSquare = 25
var board = [Int](repeating: 0, count: finalSquare + 1)
{% endhighlight %}

그런 다음 일부 사각형에는 뱀과 사다리의 특정 값이 설정됩니다. 사다리 기지가있는 사각형은 보드 위로 올라갈 수있는 양의 숫자를 갖지만, 뱀 머리가있는 사각형은 보드를 다시 내려 놓기 위해 음수를 갖습니다.

{% highlight swift %}
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
{% endhighlight %}

**Square 3** 은 사다리의 밑면을 포함합니다. 이것을 표현하기 위해 **board[03]** 은 **+08** 과 같습니다. 이는 정수 값 8 (3과 11의 차이) 과 같습니다. 값과 명령문을 정렬하기 위해 단항 더하기 연산자 (+i) 는 단항 마이너스 연산자 (-i) 와 함께 명시 적으로 사용되며 10보다 작은 수는 0으로 채워집니다. (문체 기술은 엄격히 필요하지 않지만 더 순수한 코드로 이어집니다.)

{% highlight swift %}
var square = 0
var diceRoll = 0
while square < finalSquare {
   // 주사위를 굴립니다.
   diceRoll += 1
   if diceRoll == 7 { diceRoll = 1 }
   // 굴린 값 만큼 이동합니다.
   square += diceRoll
   if square < board.count {
       // 만약 여전히 보드 위에 있다면 뱀이나 사다리를 위 혹은 아래로 이동합니다.
	   square += board[square]
   }
}
print("Game over!")
{% endhighlight %}

위의 예제는 아주 간단한 주사위 굴림 접근법을 사용합니다. 난수를 생성하는 대신 **diceRoll** 값을 0으로 시작합니다. **while** 루프를 통과 할 때마다 **diceRoll** 이 1 씩 증가하고 그 다음에 너무 커 졌는지 확인합니다. 이 반환 값이 7 일 때마다 주사위 롤이 너무 커져 값을 1로 재설정 합니다. 결과는 항상 1, 2, 3, 4, 5, 6, 1, 2 식으로 이어지는 **diceRoll** 값의 시퀀스입니다.

주사위를 굴린 후, 플레이어는 **diceRoll** 사각형으로 앞으로 이동합니다. 주사위 굴림으로 인해 플레이어가 정사각형 25 이상으로 이동했을 가능성이 있습니다.이 경우 게임이 끝났습니다. 이 시나리오에 대처하기 위해 코드는 **square** 가 보드 배열의 **count** 속성보다 작은 지 확인합니다. **square** 가 유효한 경우 **board[square]** 에 저장된 값이 현재 제곱 값에 더해져 플레이어가 뱀이나 사다리를 위아래로 움직입니다.

### Repeat-While

**repeat-while** 루프 라는 다른 **while** 루프의 변형은, 해당 루프의 조건을 고려하기 전에 루프 블락을 통해 처음 한번은 수행합니다. 그런 다음 조건이 false 가  될 때까지 루프를 계속 반복합니다.

이것이 기본적인 **repeat-while** 루프의 폼입니다.

{% highlight swift %}
repeat {
	실행문
} while 조건
{% endhighlight %}

> swift 의 repeat-while 루프는 다른 언어의 do-while 루프와 유사합니다.

{% highlight swift %}
repeat {
   // 뱀이나 사다리를 위 혹은 아래로 움직입니다.
   square += board[square]
   // 주사위를 굴립니다.
   diceRoll += 1
   if diceRoll == 7 { diceRoll = 1 }
   // 주사위를 굴린 만큼 이동합니다.
   square += diceRoll
} while square < finalSquare
print("Game over!")
{% endhighlight %}

> /Repeat-while 코드 에 대한 설명은  [link](https://docs.swift.org/swift-book/LanguageGuide/ControlFlow.html)  에서 자세히 확인할 수 있습니다.

[출처]: Apple Inc. ‘The Swift Programming Language (Swift 4.1).’ iBooks. https://itunes.apple.com/kr/book/the-swift-programming-language-swift-4-1/id881256329?mt=11
