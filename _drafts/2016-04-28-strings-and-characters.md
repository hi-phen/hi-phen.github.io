---
title: Swift 정리 - Strings and Characters
---

역시 별다른 내용없으니 가볍게 보고 가자

뻔한 내용은 역시 생략

## Initializing an Empty String

문자열 초기화

{% highlight swift %}
var emptyString = ""               // empty string literal
var anotherEmptyString = String()  // initializer syntax
if emptyString.isEmpty {
    print("Nothing to see here")
}
//Nothing to see here
if anotherEmptyString.isEmpty {
    print("Nothing to see here")
}
//Nothing to see here
{% endhighlight %}

## Strings Are Value Types

문자열은 `Value Type` 이다.

즉 함수로의 전달이나 변수 할당 시 값의 복사본을 가진다.

`Reference Type`과 `Value Type`의 차이를 모르면 따로 공부하도록

{% highlight swift %}
var string1 :String = "value1"
var string2 :String

string2 = string1
print(string2)	//value1
string2 = "value2"
print(string1)	//value1
print(string2)	//value2
{% endhighlight %}

## Working with Characters

코드를 써놓기는 하겠지만.. 쓸일이 있으려나

{% highlight swift %}

for character in "Dog!🐶".characters {
    print(character)
}
// D
// o
// g
// !
// 🐶

let catCharacters: [Character] = ["C", "a", "t", "!", "🐱"]
let catString = String(catCharacters)
print(catString)
// Prints "Cat!🐱"
{% endhighlight %}

## Concatenating Strings and Characters

문자열 합치기

{% highlight swift %}
let string1 = "hello"
let string2 = " there"
var welcome = string1 + string2
// welcome now equals "hello there"

var instruction = "look over"
instruction += string2
// instruction now equals "look over there"

let exclamationMark: Character = "!"
welcome.append(exclamationMark)
// welcome now equals "hello there!"
{% endhighlight %}

## Counting Characters

문자열 세기

{% highlight swift %}
var string1 = "한글"
print(string1.characters.count) //2
{% endhighlight %}

## String Indices

문자열 인덱스

{% highlight swift %}
let greeting = "Guten Tag!"
greeting[greeting.startIndex]
// G
greeting[greeting.endIndex.predecessor()]
// !
greeting[greeting.startIndex.successor()]
// u
let index = greeting.startIndex.advancedBy(7)
greeting[index]
// a

for index in greeting.characters.indices {
    print("\(greeting[index]) ", terminator: "")
}
// prints "G u t e n   T a g ! "
{% endhighlight %}

## Inserting and Removing

문자열의 삽입과 삭제

{% highlight swift %}
var welcome = "hello"
welcome.insert("!", atIndex: welcome.endIndex)
// welcome now equals "hello!"

welcome.insertContentsOf(" there".characters, at: welcome.endIndex.predecessor())
// welcome now equals "hello there!"

welcome.removeAtIndex(welcome.endIndex.predecessor())
// welcome now equals "hello there"

let range = welcome.endIndex.advancedBy(-6) ..< welcome.endIndex
welcome.removeRange(range)
// welcome now equals "hello"
{% endhighlight %}

## Prefix and Suffix Equality

이상하게 `hasPrefix(_:)`, `hasSuffix(_:)`가 [여기](https://swiftlang.ng.bluemix.net){:target="_blank"} 에서는 컴파일이 안된다. 하지만 실제로는 되는 듯 함

{% highlight swift %}
let str = "has prefix"

print(str.hasPrefix("has"))	//true
print(str.hasSuffix("has"))	//false
print(str.hasPrefix("prefix")) //false
print(str.hasSuffix("prefix")) //true
{% endhighlight %}

문자열의 검색은 아래와 같이 가능하다고 한다

Swift 그 자체에는 없고 Objective-C의 Foundation 프레임워크를 통해 사용 가능한듯

Swift라이브러리에서 한참 찾았는데 결국 Objective-C..

{% highlight swift %}
let s = "ABCDE"
let range = s.rangeOfString("C")
range.startIndex                   // 2
range.endIndex                     // 3
s[range]                           // "C"
{% endhighlight %}
