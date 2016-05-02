---
layout: post
title: Swift 정리 - Collection Types
date: 2016-04-28 16:22:00 +0900
comments: true
categories: ["dev","swift"]
--- 

Swift는 Array, Set, Dictionary 3가지 콜렉션을 지원한다.

* Set : 정렬되지 않은 고유 값 저장
* Dictionary : 정렬되지 않은 Key-value 저장
* Array : 걍 배열

각 콜렉션은 지정된 타입의 값만 저장이 가능하다.

## Mutability of Collections

모든 콜렉션 타입은 변형이 가능하다. 즉 콜렉션 타입을 만들고 난 후 주가,삭제,변경이 가능. 당연히 `let`로 지정하면 변형은 불가.

## Arrays

배열은 정렬된 값의 리스트이며 같은값이 다른 위치에 여러번 존재 할 수 있다.

> Swift의 배열은 `Foundation`의 `NSArray` 클래스와 연결되어 있으며 다른 여러 타입들도 마찬가지 인듯 하다 [여기](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/BuildingCocoaApps/WorkingWithCocoaDataTypes.html){:target="_blank"}를 참고

## Array Type Shorthand Syntax

Swift에서 배열 사용시에는 `Array<Element>` 를 사용하지만 `[Element]` 로도 사용이 가능함

{% highlight swift %}
let arr : Array<Int> = [1,2]
let arr2 : [Int] = [1,2]

print(arr == arr2)
//true
{% endhighlight%}

## Creating an Empty Array

빈 배열 선언

{% highlight swift %}
var someInts : [Int] = []
var anotherInts = [Int]()

someInts.append(2)
anotherInts.append(3)

print(someInts) //[2]
print(anotherInts.count) //1
{% endhighlight%}

## Creating an Array with a Default Value

초기값과 함께 배열 선언하기 

{% highlight swift %}
var threeDoubles = [Double](count: 3, repeatedValue: 0.0)
var anotherThreeDoubles = [0.0,0.0,0.0]

print(threeDoubles) //[0.0,0.0,0.0]
print(anotherThreeDoubles) //[0.0,0.0,0.0]
{% endhighlight%}

## Creating an Array by Adding Two Arrays Togethe

같은형식의 배열은 `+`연산을 통해 합치기도 가능하다.

{% highlight swift %}
var threeDoubles = [Double](count: 3, repeatedValue: 0.0)
var anotherThreeDoubles = [2.5]

print(threeDoubles+anotherThreeDoubles)
//[0.0, 0.0, 0.0, 2.5]
{% endhighlight%}

## Creating an Array with an Array Literal

배열을 초기화 할 때 `[]` 안에 값을 직접 넣어 배열 선언이 가능하다.
이때에도 타입추정을 통해 타입은 생략이 가능하다

{% highlight swift %}
var shoppingList: [String] = ["Eggs", "Milk"]
var shoppingList = ["Eggs", "Milk"]
{% endhighlight%}

## Accessing and Modifying an Array

배열의 접근과 수정

{% highlight swift %}
var shoppingList = ["Eggs", "Milk"]
print(shoppingList.count) //2
print(shoppingList.isEmpty) //false
shoppingList.append("Flour")
shoppingList += ["Baking Powder"]
print(shoppingList) // ["Eggs", "Milk", "Flour", "Baking Powder"]
shoppingList[2...3] = ["Bananas", "Apples"]
print(shoppingList) // ["Eggs", "Milk", "Bananas", "Apples"]
shoppingList.insert("Maple Syrup", atIndex: 0)
print(shoppingList) // ["Maple Syrup", "Eggs", "Milk", "Bananas", "Apples"]
shoppingList.removeAtIndex(0)
shoppingList.removeLast()
print(shoppingList) // ["Eggs", "Milk", "Bananas"]
{% endhighlight%}

## Iterating Over an Array
 
루프문 배울때도 나올꺼같은데..

`enumerate()`를 사용하면 `index`를 받아올수 있다는것만 기억해두자

{% highlight swift %}
var shoppingList = ["Eggs", "Milk"]

for item in shoppingList {
    print(item)
}
//Eggs
//Milk
for (index,item) in shoppingList.enumerate(){
    print(index,item)
}
//0 Eggs
//1 Milk
{% endhighlight%}

## Sets

각 항목의 값이 고유하고 순서가 중요하지 않을때 Set을 사용하는걸 고려 해보자

>역시 `Foundation`의 `NSSet`을 사용할 수 있다

## Hash Values for Set Types

`Set` 값의 저장 타입은 `hashable` 해야 한다. Swift에서 제공되는 기본 타입은 모두 `hashable` 하며 사용자 지정 타입의 경우 `Hashable` 프로토콜[^1]을 구현하면 된다. 

## Set Type Syntax

Set은 `Set<Element>` 으로 사용 가능 하며 배열과 같은 단축형이 없다.

## Creating and Initializing an Empty Set

{% highlight swift %}
var letters = Set<Character>()
print(letters.count) //0
letters.insert("a")
print(letters.count) //1
letters = [] // 빈 set으로 초기화됨
print(letters.count) //0
{% endhighlight%}

## Creating a Set with an Array Literal

배열과 비슷하게 초기화 하여 사용하기

{% highlight swift %}
var favoriteGenres: Set<String> = ["Rock", "Classical", "Hip hop"]
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]
{% endhighlight%}

## Accessing and Modifying a Set

Set의 접근과 수정

{% highlight swift %}
var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"]
print(favoriteGenres.isEmpty) // false
favoriteGenres.insert("Jazz")
favoriteGenres.remove("Rock")
print(favoriteGenres) // ["Classical", "Hip hop", "Jazz"]
print(favoriteGenres.contains("Funk")) // false
{% endhighlight%}

## Iterating Over a Set

아래 예제에는 없지만 Set역시 `enumerate()`를 사용해서 `index`를 받아오는게 가능하다.

{% highlight swift %}
for genre in favoriteGenres {
    print("\(genre)")
}
{% endhighlight%}


`.sort()`를 사용하면 정렬된 값을 받아올 수 있다

{% highlight swift %}
for genre in favoriteGenres.sort() {
    print("\(genre)")
}
{% endhighlight%}

## Fundamental Set Operations

Set의 연산으로 교집합, 교집합의 여집합, 합집합, 차집합 연산이 가능하다.

{% highlight swift %}
let oddDigits: Set = [1, 3, 5, 7, 9]
let evenDigits: Set = [0, 2, 4, 6, 8]
let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]
 
print(oddDigits.union(evenDigits).sort()) //합집합
// [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
print(oddDigits.intersect(evenDigits).sort()) //교집합
// []
print(oddDigits.subtract(singleDigitPrimeNumbers).sort()) //차집합
// [1, 9]
print(oddDigits.exclusiveOr(singleDigitPrimeNumbers).sort()) //교집합의 여집합
// [1, 2, 9]
{% endhighlight%}

## Set Membership and Equality

아래 연산을 통해 각 Set이 서로 포함관계인지 아닌지 연산이 가능하다.
`isStrictSubsetOf(_:)`, `isStrictSupersetOf(_:)`는 포함관계이지만 `==`가 성립하지 않아야 한다.

{% highlight swift %}
let houseAnimals: Set = ["🐶", "🐱"]
let anotherHouseAnimals: Set = ["🐶", "🐱"]
let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let cityAnimals: Set = ["🐦", "🐭"]
 
print(houseAnimals.isSubsetOf(farmAnimals))
// true
print(farmAnimals.isSupersetOf(houseAnimals))
// true
print(farmAnimals.isDisjointWith(cityAnimals))
// true
print(houseAnimals.isStrictSubsetOf(anotherHouseAnimals)) // false
print(houseAnimals.isSubsetOf(anotherHouseAnimals)) //true
{% endhighlight%}

## Dictionaries

Key-value 콜렉션 타입으로 자바의 `Map`과 같은 타입

> 역시 NSDictionary 사용 가능

## Dictionary Type Shorthand Syntax

선언은 `Dictionary<Key,Value]`로 가능하며 `[Key: Value]`로도 사용이 가능하다. 여기서 Key는 `hashable`해야 함.

## Creating an Empty Dictionary

빈 Dictionary 선언

{% highlight swift %}
var namesOfIntegers = [Int: String]()
namesOfIntegers[16] = "sixteen"
namesOfIntegers = [:]
{% endhighlight%}

## Creating a Dictionary with a Dictionary Literal

초기값과 함께 선언

{% highlight swift %}
var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
{% endhighlight%}

## Accessing and Modifying a Dictionary

Dictionary 의 접근과 수정

{% highlight swift %}
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
print(airports.count) //2
print(airports.isEmpty) //false
airports["LHR"] = "London"
airports["LHR"] = "London Heathrow"
print(airports) //["YYZ": "Toronto Pearson", "DUB": "Dublin", "LHR": "London Heathrow"]
airports.updateValue("Dublin Airport", forKey: "DUB")
print(airports) //["YYZ": "Toronto Pearson", "DUB": "Dublin Airport", "LHR": "London Heathrow"]
airports["APL"] = "Apple International"
airports["APL"] = nil //삭제
airports.removeValueForKey("DUB")
print(airports) //["YYZ": "Toronto Pearson", "LHR": "London Heathrow"]
{% endhighlight%}

## Iterating Over a Dictionary

역시 `enumerate()`는 사용 가능하고 (key,value) 튜플을 반환한다.

{% highlight swift %}
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
for (airportCode, airportName) in airports {
    print("\(airportCode): \(airportName)")
}
// YYZ: Toronto Pearson
// DUB: DUB Dublin

for (index,(key,value)) in airports.enumerate(){
    print(index,key,value)
}
//0 YYZ Toronto Pearson
//1 DUB Dublin
{% endhighlight%}

`.keys`,`.values`를 통해 키,값 배열을 받아올수도 있다. `.sort()`를 통해 값을 정렬할수도 있다.

{% highlight swift %}
var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
for airportCode in airports.keys {
    print("Airport code: \(airportCode)")
}
// Airport code: YYZ
// Airport code: DUB
 
for airportName in airports.values {
    print("Airport name: \(airportName)")
}
// Airport name: Toronto Pearson
// Airport name: Dublin

let airportCodes = [String](airports.keys)
let airportNames = [String](airports.values)

print(airportCodes) //["YYZ", "DUB"]
print(airportNames) //["Toronto Pearson", "Dublin"]
print(airports.keys.sort()) //["DUB", "YYZ"]
{% endhighlight%}
---
[^1]: 프로토콜은 자바의 인터페이스와 같은 개념