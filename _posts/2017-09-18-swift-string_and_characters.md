---
layout: post
title: Swift - String and Characters
excerpt: Swift 3 - 문자열과 캐릭터
comments: true
tags: [ios, Swift, String, Character] 
---

안녕하세요. 엔비냥 입니다.
이번에는 Swift 3 의 String and Characters 챕터를 번역 하려고 합니다.
오타나 오역이 있으면 댓글 부탁드립니다. 감사합니다.

---

String 은 “hello, world” 나 “albatross” 같은 연속된 문자들(characters) 입니다.  Swift 에서는 String 타입으로 사용하게 됩니다.  String 의 내용은 여러 다른 종류의 문자 (Character) 들의 컬렉션들을 포함할 수 있습니다.

Swift의 String 및 Character types은 코드에서 텍스트를 사용하여 작업 할 수있는 빠른 유니 코드 호환 방식을 제공합니다.  String 의 생성 및 취급에 대한 신텍스는 C와 비슷하게 가볍고 읽기 쉽습니다. String 의 연결은 2개의 string 을 + 연산자로 쉽게 연결 할 수 있습니다.

> Swift 의 String 타입은 Foundation 의 NSString 클래스에 브릿징 되어 있습니다. Foundation은 String을 확장하여 NSString에 정의 된 메서드를 노출합니다. 즉, Foundation을 임포트하면 캐스팅하지 않고 String의 NSString 메서드에 액세스 할 수 있습니다. 

## String Literals

String Literals 과 같이,  코드에서 String 값을 미리 지정 할 수 있습니다. String Literal 은 double quotes (“) 사이에 연속된 문자를 넣습니다.

{% highlight swift %}
let someString = "Some String literal value"
{% endhighlight %}

여기 someString 상수에는 String literal 값이 으로 초기화 하여서, String 타입으로 추론 하게 됩니다.

## Initializing an Empty String

빈 String 값을 만들려면 empty string literal 을 변수에 부여하거나, 새로운 String 객체를 생성하면 돕니다.

{% highlight swift %}
var emptyString = "" // empty string literal
var anotherEmptyString = String() // 신텍스 초기화
// 두 String 들은 모두 빈값을 가지게 됩니다.
{% endhighlight %}

String 의 값이 비어있는지 체크 하려면 isEmpty 프로퍼티의 Boolean 값을 이용합니다.

{% highlight swift %}
if emptyString.isEmpty {
print("Nothing to see here")
}
{% endhighlight %}

## String Mutability

특정 String을 변수 (이 경우 수정할 수 있음) 또는 상수 (이 경우 수정할 수 없음)에 할당하여 수정할 수 있는지 여부를 나타냅니다.

{% highlight swift %}
var variableString = "Horse"
variableString += " and carriage"
// variableString 은 이제 "Horse and carriage" 입니다.

let constantString = "Highlander"
constantString += " and another Highlander"
// 컴파일 에러, 상수는 수정할 수 없습니다.
{% endhighlight %}

## Strings Are Value Types

Swift 의 String 타입은 value 타입 입니다. 만약  새로운 String 값을 생성하면, 함수를 지나거나 상수나 변수에 부여할때 String 값을 복사하게 됩니다.
각 케이스에, 원래 값들이 아닌 새로운 복사된 String 값들이 생성되고, 부여됩니다.

## Working with Characters

String 에서 characters 프로퍼티를 For-in 루프를 이용하여 각 Character 들의 값들을 접근 할수 있습니다.

{% highlight swift %}
for character in "Dog!🐶".characters {
print(character)
}
// D
// o
// g
// !
// 🐶
{% endhighlight %}

Character 타입을 이용하여 한 문자의 상수나 변수를 생성할 수 있습니다.

{% highlight swift %}
let exclamationMark: Character = "!"
{% endhighlight %}

Character 들의 배열을 사용해서 String 값을 생성할 수 있습니다.

{% highlight swift %}
let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
let catString = String(catCharacters)
print(catString)
// Prints "Cat!🐱"
{% endhighlight %}

## Concatenating Strings And Characters

String 값들은 + 연산자를 이용하여 합치고, 새로운 String 값을 만들수 있습니다.

{% highlight swift %}
let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2
// welcome now equals "hello there"
{% endhighlight %}

또한,  addition assignment 연산자 (+=) 를 이용하여 합칠수 있습니다.

{% highlight swift %}
var instruction = "look over"
instruction += string2
// 이제 instruction 은 "look over there" 입니다.
{% endhighlight %}

String 타입의 append() 메소드를 사용하여 Character 값을 String 값에 추가할 수 있습니다.

{% highlight swift %}
let exclamationMark: Character = "!"
welcome.append(exclamationMark)
// 이제 welcome 은 "hello there!" 입니다.
{% endhighlight %}

> 반대로, String 값을 Character 변수에 추가할 수 없습니다. Character 값은 하나의 character 만 가질수 있기 문입니다.

## String Interpolation

String interpolation (삽입)  은 상수들, 변수들, 리터럴들을 가지고 새로운 String 값을 조합 합니다. 삽입할 각 항목들은 backslash (\) 들로 감싸서 사용하게 됩니다.

{% highlight swift %}
let multiplier = 3
let message = "\(multiplier) times 2.5 is \(Double(multiplier) * 2.5)"
// message 는 "3 times 2.5 is 7.5" 입니다.
{% endhighlight %}

## Unicode

Unicode 는 다른  Writing 시스템에서 인코딩, 표현, 그리고 text 프로세싱 을 위한 국제적인 기본 기준입니다. Swift 의 String 과 Character 는 완벽하게 Unicode 를 호환 합니다.

### Unicode Scalars

Swift 의 네이티브 String 타입은 Unicode Scalar 값들로 만들어 집니다.
Unicode scalar 는 U+0061 (소문자 a) 혹은 U+1F425 ( 앞을 보고 있는 병아리 🐥) 와 같은 문자나 수식어을 위해 21-bit 번호들로 이루어 집니다.

모든 21-bit Unicode Scalar 가 문자에 할당되지는 않습니다. 일부 Scalar 는 나중에 할당 할 수 있도록 예약되어 있습니다.

### Special Characters in String Literals

String literal 다음의 특별한 문자들도 포함할 수 있습니다.

* The escaped special characters 
* \0 (null character)
* \\ (backslash)
* \t (horizontal tab)
* \n (line feed)
* \r (carriage return)
* \" (double quote)
* \' (single quote)
* An arbitrary Unicode scalar, written as \u{n}, where n is a 1–8 digit hexadecimal number with a value equal to a valid Unicode code point

{% highlight swift %}
let wiseWords = "\"Imagination is more important than knowledge\" - Einstein"
// "Imagination is more important than knowledge" - Einstein
let dollarSign = "\u{24}"        // $,  Unicode scalar U+0024
let blackHeart = "\u{2665}"      // ♥,  Unicode scalar U+2665
let sparklingHeart = "\u{1F496}" // 💖, Unicode scalar U+1F496
{% endhighlight %}

### Extended Grapheme Clusters

Swift의 Character 유형의 모든 인스턴스는 하나의 확장 된 grapheme cluster 들을 나타냅니다. 확장 된 축약 형 Cluster 는 사람이 읽을 수있는 한 문자를 생성하는 (조합 된) 하나 이상의 유니 코드 스칼라의 시퀀스입니다.

예를들어, é 는 single Unicode scalar é (라틴 소문자 양음 악센트 e 혹은 U+00E9) 로 표현될수 있습니다.

{% highlight swift %}
let eAcute: Character = "\u{E9}"  // é
let combinedEAcute: Character = "\u{65}\u{301}" // e followed by ́
// eAcute is é, combinedEAcute is é
{% endhighlight %}

Extended grapheme cluster 들은 하나의 Character 값인 complex script character 들로 표현될 수도 있습니다. 예를 들어 한글 을 표현할 때 사용 됩니다.

{% highlight swift %}
let precomposed: Character = "\u{D55C}"  // 한
let decomposed: Character = "\u{1112}\u{1161}\u{11AB}" // ᄒ, ᅡ, ᆫ
// precomposed is 한, decomposed is 한
{% endhighlight %}

{% highlight swift %}
let enclosedEAcute: Character = "\u{E9}\u{20DD}"
// enclosedEAcute is é⃝

let regionalIndicatorForUS: Character = "\u{1F1FA}\u{1F1F8}"
// regionalIndicatorForUS is 🇺🇸
{% endhighlight %}

## Counting Characters

String 에서 Character 값들의 숫자를 가져올때, string 의 characters 프로퍼티의 count 프로퍼티를 사용합니다. (Swift 4 에서는 characters 프로퍼티에 접근 안하고 count 프로퍼티가 생겨서 직접 접근 하여 가져올 수 있습니다.)

{% highlight swift %}
let unusualMenagerie = "Koala 🐨, Snail 🐌, Penguin 🐧, Dromedary 🐪"
print("unusualMenagerie has \(unusualMenagerie.characters.count) characters")
// Prints unusualMenagerie 은 40 캐릭터들을 가지고 있습니다.
{% endhighlight %}

## Accessing and Modifying a String

메서드와 속성 혹은 subscript syntax 응 사용하여 String에 접근하고 수정합니다.

### String indices

각 String 값은 각 문자들의 위치를 상응하는 연관 인덱스 타입인 String.Index 를 가지고 있습니다.

위에서 언급했듯이 다른 문자들을 저장할 때 다른 양의 메모리가 필요하므로, 어떤 문자가 특정 위치에 있는지 판별하려면 해당 String의 시작 또는 끝에서 각 Unicode Scalar 를 반복해야합니다. 이런 이유로  Swift 의 String 은 정수 값으로 인덱싱 될 수 없습니다.

String 의 첫 문자의 위치에 접근하려면 startIndex 프로퍼티를 이용해야 합니다. endIndex 프로퍼티는 String 의 마지막 문자의 포지션 다음 인덱스를 나타냅니다.

index(before:) 하고 index(after:) 메소드들로 인덱스들에 접근할 수 있습니다.

{% highlight swift %}
let greeting = "Guten Tag!"
greeting[greeting.startIndex]
// G
greeting[greeting.index(before: greeting.endIndex)]
// !
greeting[greeting.index(after: greeting.startIndex)]
// u
let index = greeting.index(greeting.startIndex, offsetBy: 7)
greeting[index]
// a
{% endhighlight %}

만약 String 범위에 벗어난 인덱스를 접근하려고 한다면, 런타임 에러가 발생합니다.

### Insert and Removing

insert(_:at:) 메소드를 사용하여 지정된 인덱스에 하나의 문자를 추가할 수 있습니다. 혹은, 다른 String의 내용을 지정된 인덱스에 추가할 때에는 insert(contentOf:at:) 메소드를 이용합니다.

{% highlight swift %}
var welcome = "hello"
welcome.insert("!", at: welcome.endIndex)
// welcome 은 "hello!" 와 같습니다.

welcome.insert(contentsOf: " there".characters, at: welcome.index(before: welcome.endIndex))
// 이제 welcome 은 "hello there! 와 같습니다.
{% endhighlight %}

하나의 문자를 삭제하려면 remove(at:) 메소드를 사용하고, 지정된 범위의 문자들을 삭제할때는 removeSubrange(_:) 메소드를 사용합니다.

## Comparing Strings

Swift 는 텍스트의 값을 비교하는 3가지 방법 ( String 과 문자의 같음, prefix 의 같음, suffix 의 같음) 을 제공합니다. 

### String and Character Equality

String 과 문자의 같음은 equal to 연산자 (==) 와 nor equal to 연산자 (!=) 로 확인합니다.

{% highlight swift %}
let quotation = "We're a lot alike, you and I."
let sameQuotation = "We're a lot alike, you and I."
if quotation == sameQuotation {
print("These two strings are considered equal")
}
// Prints "These two strings are considered equal"
{% endhighlight %}

### Prefix and Suffix Equality

hasPrefix(_:) 와 hasSuffix(_:) 메소드를 사용하여 String 이 특정한 prefix 혹은 suffix 를 가지고 있는지 확인할 수 있습니다. 두 메소드 모두 String 을 받아서 Boolean 값을 반환 합니다.

## Unicode Representations of Strings

Unicode String 을 텍스트 파일 또는 다른 저장용도에 적을때 해당 String 의Unicode Scalar 는 encoding forms 에 정의된 양식 중 하나로 인코딩됩니다. UTF-8, UTF-16, UTF-32 등을 포함합니다.

Swift 는 String 의 Uniode 표현에 대한 여러 방법을 제공합니다. for-in 문을 사용하여 문자열을 반복할 수 있고, 개개별 케릭터 값을 Unicode extended grapheme clusters) 로 접근 할 수 있습니다.

다른 방법으로는, String 값에 3개의 Unicode-compliant 표현 중 하나를 이용해서 접근 할 수 있습니다.

* UTF-8 유닛들의 모음 (String 의 utf8 프로퍼티로  접근)
* UTF-16 유닛들의 모음 (String 의 utf16 프로퍼티로 접근)
* UTF-32 인코딩 폼 과 동일한 UTF-21 비트 Unicode scalar 값의 모음 (String 의 unicodeScalars 프로퍼티로 접근)

### UTF-8 표현

utf8 프로퍼티를 이용하여 String 의 UTF-8 표현에 접근할 수 있습니다. 이 프로퍼티는 unsigned 8-bit (UInt8) 값들의 모음인 String.UTF8View 타입입니다.

![]({{ site.url }}/img/swift/string_1.png)

{% highlight swift %}
for codeUnit in dogString.utf8 {
print("\(codeUnit) ", terminator: "")
}
print("")
// "68 111 103 226 128 188 240 159 144 182" 이 프린트 됩니다.
{% endhighlight %}

이 예제에서 처음 3개 codeUnit 인 (68, 111, 103) 은 ASCII 표현과 같은 UTF-8 표현인 (D, o, g) 의 케릭터를 나타냅니다. 

### UTF-16 표현

utf16 프로퍼티를 이용하여 String 의 UTF-16 표현에 접근할 수 있습니다.  이 프로퍼티는 unsigned 16-bit (UInt16) 값들의 모음인 String.UTF16View 타입입니다.

![]({{ site.url }}/img/swift/string_2.png)

### Unicode Scalar Representation

unicodeScalars 프로퍼티를 이용하여 String 의 Unicode Scalar 표현에 접근할 수 있습니다. 이 프로퍼티는 UnicodeScalar 값들의 모음인 UnicodeScalarView 타입입니다.

![]({{ site.url }}/img/swift/string_3.png)
