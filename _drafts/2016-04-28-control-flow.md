---
layout: post
title: Swift 정리 - Control Flow
date: 2016-04-28 17:18:00 +0900
comments: true
categories: ["dev","swift"]
--- 

## For-In Loops

앞서 여러번 봤던 for in 문이다 가장 빈번히 사용되는 제어문이 아닐까 생각됨

`_`은 Swift여러군데에서 쓰이는데 간단히 말해서 `무시`나 `필요없음`, `상관없음` 정도가 아닐까 싶다.
아래와 같이 index를 받아야 할 곳에 index가 필요없는 경우 사용

{% highlight swift %}
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}
{% endhighlight %}

두가지의 예재를 후르륵 보고 가자 

{% highlight swift %}
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    print("Hello, \(name)!")
}
// Hello, Anna!
// Hello, Alex!
// Hello, Brian!
// Hello, Jack!

let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    print("\(animalName)s have \(legCount) legs")
}
// ants have 6 legs
// cats have 4 legs
// spiders have 8 legs
{% endhighlight %}

## While

별거없다 조건문이 참이면 실행문 실행

{% highlight swift %}
while condition {
	statment
}
{% endhighlight %}

`do-while` 문을 swift에서 `repeat-while` 문으로 사용하는 것 같다 repeat 안의 실행문은 최소 한번 실행된다.

{% highlight swift %}
repeat {
	statment
} while condition
{% endhighlight %}

## If

{% highlight swift %}
if statment {
	condition
} else if statment{
	condition
} else {
	condition
}
{% endhighlight %}

## Switch

Switch 문은 `case`절에 `,`을 통해 여러개의 조건을 기술할 수 있고
`break`를 쓰지 않아도 다음 절을 수행하지 않는다.

{% highlight swift %}
let someCharacter: Character = "e"
switch someCharacter {
case "a", "e", "i", "o", "u":
    print("\(someCharacter) is a vowel")
case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
     "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
    print("\(someCharacter) is a consonant")
default:
    print("\(someCharacter) is not a vowel or a consonant")
}
//e is a vowel
{% endhighlight %}

`case`문에 아무것도 기술하지 않으면 컴파일 에러가 나며 다음 `case` 절을 수행하고싶으면 `fallthrough` 를 명시해야 함.
아래의 예제는 예제일뿐 아래 상황에서는 `,`를 통해 하나의 `case`문에 기술하는게 좋다.

{% highlight swift %}
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a":
    fallthrough
case "A":
    print("The letter A")
default:
    print("Not the letter A")
}
// The letter A
{% endhighlight %}

## Interval Matching

`...` 나 `..<`를 통해 범위로도 매칭이 가능하다.

{% highlight swift %}
let approximateCount = 62
let countedThings = "moons orbiting Saturn"
var naturalCount: String
switch approximateCount {
case 0:
    naturalCount = "no"
case 1..<5:
    naturalCount = "a few"
case 5..<12:
    naturalCount = "several"
case 12..<100:
    naturalCount = "dozens of"
case 100..<1000:
    naturalCount = "hundreds of"
default:
    naturalCount = "many"
}
print(naturalCount)
//dozens of
{% endhighlight %}

## Tuples

튜플 매칭도 아래와 같이 가능하다

{% highlight swift %}
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    print("(0, 0) is at the origin")
case (_, 0):
    print("(\(somePoint.0), 0) is on the x-axis")
case (0, _):
    print("(0, \(somePoint.1)) is on the y-axis")
case (-2...2, -2...2):
    print("(\(somePoint.0), \(somePoint.1)) is inside the box")
default:
    print("(\(somePoint.0), \(somePoint.1)) is outside of the box")
}
//(1, 1) is inside the box
{% endhighlight %}

## Value Bindings

임시 상수,변수를 통해 `case`문 안에서 사용가능하다

{% highlight swift %}
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    print("on the x-axis with an x value of \(x)")
case (0, let y):
    print("on the y-axis with a y value of \(y)")
case let (x, y):
    print("somewhere else at (\(x), \(y))")
}
//on the x-axis with an x value of 2
{% endhighlight %}

## Where

`case`문안에 `where`절을 사용하여 조건문까지 기술이 가능하다.

{% highlight swift %}
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    print("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    print("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    print("(\(x), \(y)) is just some arbitrary point")
}
// (1, -1) is on the line x == -y
{% endhighlight %}

## Control Transfer Statements

간단하게 설명하고 넘어가자

* continue : 현재 실행문은 종료하고 다음 실행문 실행
* break : 반복문이나 `swich`문을 즉시 종료
* fallthrough : `swich`문에서 `case`절 종료 후 다음 `case`문을 실행

## Labeled Statements

중첩된 반복,제어절에 이름을 붙이면 `break`와 `continue`를 사용할때 좀 더 명시적으로 사용이 가능하다

`label : while` 와 같은 형식으로 사용 가능

{% highlight swift %}
loop : for idx in 0...2 {
    print(idx)
    switch idx {
        case 0:
            continue loop
        case 1:
            break loop
        default:
            break
    }
}
//0
//1

//여기서 loop를 지정하지 않으면 0,1,2가 출력됨
{% endhighlight %}

## Early Exit

`guard`문은 `if`문과 흡사하지만 조건이 `true` 일때만 다음으로 넘어가고 `false`일때는 `else`문을 수행한다.

`guard`문은 항상 `else`문을 가지고 있다. 

{% highlight swift %}
func greet(person: [String: String]) {
    guard let name = person["name"] else {
        return
    }
    
    print("Hello \(name)!")
    
    guard let location = person["location"] else {
        print("I hope the weather is nice near you.")
        return
    }
    
    print("I hope the weather is nice in \(location).")
}
 
greet(["name": "John"])
// Prints "Hello John!"
// Prints "I hope the weather is nice near you."
greet(["name": "Jane", "location": "Cupertino"])
// Prints "Hello Jane!"
// Prints "I hope the weather is nice in Cupertino."
{% endhighlight %}

## Checking API Availability

아래와 같이 API 버전 체크가 가능

{% highlight swift %}
if #available(iOS 9, OSX 10.10, *) {
    // Use iOS 9 APIs on iOS, and use OS X v10.10 APIs on OS X
} else {
    // Fall back to earlier iOS and OS X APIs
}
{% endhighlight %}