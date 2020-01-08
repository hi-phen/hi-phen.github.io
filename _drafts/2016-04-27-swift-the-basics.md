---
title: Swift 정리 - The Basics
---

어쩌다 보니 아이폰 개발을 해야 할 것 같아서 관련 공부를 좀 해야 하는데..
기왕에 하는거 요즘 새로 나온 Swift로 공부해보기로 결정 했다

기존에 자바 서버와 안드로이드쪽 개발만 해봐서 이런 계열의 언어에 익숙치가 않은데[^1]
공부 하다 보니 정리할 필요도 있을 것 같고 깃헙에 블로그 만드는것도 해볼겸 정리해 본다.

[여기](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/TheBasics.html){:target="_blank"}를 보고 공부하고 있는데 영어다..

한글 번역본은 옛날 버전이라 안맞는 부분도 있고 한창 자라나는(?) 언어인지 버전업이 빨라 이것저것 바뀌는 모양 이라
일단 공식 가이드의 코드만 보고[^2] **내멋대로 해석**해서 정리하고 나중에 다른 정보들을 습득하여 수정하는 방식으로 해야겠다.

---

## Declaring Constants and Variables

변수 선언은 `var`

상수 선언은 `let`

여기서 상수는 자바의 `final`과 같다

`var/let 이름 : type = 값` 과 같이 사용 가능

{% highlight swift %}
let maximumNumberOfLoginAttempts = 10
var currentLoginAttempt = 0
{% endhighlight %}

## Type Annotations

타입지정은 `:`을 통해서 가능

Swift는 `타입추정`을 통해서 추정이 가능한 경우에는 생략이 가능하다

이 `타입추정`은 Swift의 전반적으로 사용되어 사용을 편리하게 해준다

변수타입을 지정하지 않아도 되니 마치 자바스크립트의 `var`와 같은 의미로 착각하지 말자,
추정해서 자동할당을 해줄뿐 한번 초기화된 변수에 다른 타입 할당하면 에러.

{% highlight swift %}
var welcomeMessage: String
var welcome = "Hello" //타입추정을 통해 String 타입을 가짐
{% endhighlight %}

## Naming Constants and Variables

변수와 상수의 이름은 마음대로 해도 된다. 근데 이렇게 다된다고 해도 이렇게 쓰는사람이 많을까 싶다..

{% highlight swift%}
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
{% endhighlight%}

## Printing Constants and Variables

콘솔출력은 단순하게 `print` 문자열안의 변수 출력은 `\()`로 감싸주면 됨

{% highlight swift%}
let hello = "Hello";
print(hello)
print(hello+" World")
print("\(hello) World")
{% endhighlight %}

## Comments

주석은 `//`

여러줄 주석은 `/**/`

자바와 동일

{% highlight swift%}
// this is a comment
/* this is also a comment,
 but written over multiple lines */
{% endhighlight %}

## Semicolons
눈치 챗겠지만 끝에 `;`를 붙이지 않아도 됨.

한줄에 여러 동작을 기술하거나 굳이 쓰고싶으면 써도 에러는 아님.
{% highlight swift%}
let cat = "🐱"; print(cat)
{% endhighlight %}

## Integers

`Int`와 `UInt`가 사용 가능하다

하지만 타입추정을 통해 컴파일러가 알아서 할테니 일부러 `UInt`를 쓰지 않아도 된다고 한다.

32비트와 64비트 운영체제에서 min, max값은 다르다 `Int.max`, `Int,min`값을 참고해 보자

{% highlight swift %}
//64비트에서
print(Int.max) //9223372036854775807
print(Int.min) //-9223372036854775808
{% endhighlight %}

## Floating-Point Numbers

부동소수점역시 자바와 동일하게 `Double`과 `Float`가 있다

`Float`는 소수점 6자리 `Double`은 죄소 소수점 15자리까지 표기가 가능하다.

Swift는 부동소수점 타입추정 시 언제나 `Double`을 사용한다.

## Numeric Literals

숫자의 문자표기

* 10진수 없음
* 2진수 `0b`
* 8진수 `0o`
* 16진수 `0x`

지수표기

* 1.25e2 = 1.25 x 102
* 1.25e-2 = 1.25 x 10-2
* 0xFp2 = 15 x 22
* 0xFp-2 = 15 x 2-2

{% highlight swift %}
let decimalInteger = 17
let binaryInteger = 0b10001       // 17 in binary notation
let octalInteger = 0o21           // 17 in octal notation
let hexadecimalInteger = 0x11     // 17 in hexadecimal notation
let decimalDouble = 12.1875
let exponentDouble = 1.21875e1
let hexadecimalDouble = 0xC.3p0
{% endhighlight %}

보기 좋기 위해서 숫자 앞에 `0` 을 붙이거나 구분을 위해 `_`을 넣어도 됨 해당 값은 무시된다.

{% highlight swift %}
let paddedDouble = 000123.456
let oneMillion = 1_000_000
let justOverOneMillion = 1_000_000.000_000_1
{% endhighlight %}

## Integer Conversion

정수형 타입 변환은 아래와 같이

{% highlight swift %}
let twoThousand: UInt16 = 2_000
let one: UInt8 = 1
let twoThousandAndOne = twoThousand + UInt16(one)
//2001
{% endhighlight %}

## Integer and Floating-Point Conversion

정수와 소수 타입 변환은 아래와 같이

{% highlight swift %}
let three = 3
let pointOneFourOneFiveNine = 0.14159
let pi = Double(three) + pointOneFourOneFiveNine
// pi 는 3.14159, Double형을 가짐
let integerPi = Int(pi)
// integerPi는 3, Int형을 가짐
{% endhighlight %}

## Type Aliases

타입 별칭. 쓸날이 있을까?

{% highlight swift %}
typealias AudioSample = UInt16
{% endhighlight %}

## Booleans

`true`, `false` 있습니다. 이하 생략

## Tuples

튜플은 아주 유용한것 같다. 여러개의 값을 하나로 묶는게 가능하기 떄문에 함수에서 여러개의 리턴값을 주고 싶을때의 작업이 매우 단순하게 처리가 가능해진다.

선언과 사용은 아래와 같이 사용가능

{% highlight swift %}
let http404Error = (404, "Not Found") //타입 추정
print(http404Error.0) //404
print(http404Error.1) // "Not Found"

let http200Status = (statusCode: 200, description: "OK") //이름 지정
print(http200Status.statusCode) //200
print(http200Status.description) // "OK"
//이름 지정으로 해도 .0 .1과 같은 접근 역시 가능

let http500Status: (Int,description:String) = (500,"Error") //타입지정도 가능
print(http500Status.0) //500
print(http500Status.description) // "Error"
{% endhighlight %}

## Optionals

옵셔녈 번수 선언은 타입에 `?`를 붙여주면 된다.

여기저기 읽어봤는데 정확히는 모르겠고..

`nil`[^3]일수도 있고 `nil`이 아닐수도 있는게 옵셔널 변수인듯하다

일반적인 변수타입의 경우 변수에 nil의 할당이 불가하다 런타임시 할당되면 런타임 에러가 발생

{% highlight swift %}
var serverResponseCode: Int = 404
serverResponseCode = nil
//컴파일 에러
{% endhighlight %}

{% highlight swift %}
var serverResponseCode: Int? = 404
serverResponseCode = nil
//컴파일 가능
{% endhighlight %}

아마 변수를 명확하게 사용하여 에러를 줄이기 위해 그런듯하다

지긋지긋한 `NullPointerException`

## If Statements and Forced Unwrapping

변수가 옵셔널일 경우 변수가 `nil`인지 확인 할 필요가 있다.

그리고 `nil`이 아닐 경우 해당 값을 사용 할때 언래핑(`!`) 하여 사용

{% highlight swift %}
let convertedNumber = Int("1234")
print(convertedNumber)	//Optional(1234)
print(convertedNumber!) //1234
{% endhighlight %}


## Optional Binding

옵셔널 바인딩을 통해 `nil` 체크를 단순하게 할 수 있다.

`if` 나 `where` 절 등에 임시 상수/변수를 사용하여 `nil` 체크나 `where`절을 통해 비교도 가능

{% highlight swift %}
let possibleNumber = "asdf"
if let actualNumber = Int("possibleNumber") {
    print("\"\(possibleNumber)\" has an integer value of \(actualNumber)")
} else {
    print("\"\(possibleNumber)\" could not be converted to an integer")
}
//"asdf" could not be converted to an integer


if let firstNumber = Int("4"), secondNumber = Int("42") where firstNumber < secondNumber {
    print("\(firstNumber) < \(secondNumber)")
}
//4 < 42
{% endhighlight %}

## Implicitly Unwrapped Optionals

이쯤되니 더 헷깔리는데 그냥 몇가지 테스트 후 알아낸 사실은

일반 변수

* `nil`할당 불가
* `nil`비교 불가
* 옵셔녈 변수 할당 불가
* 강제 언래핑(`!`)을 통해 옵셔널 변수 할당 가능

옵셔널 변수

* `nil`할당 가능
* `nil`비교 가능
* 일반, 언래핑 변수 할당 가능

언래핑 변수

* `nil`할당 가능[^4]
* `nil`비교 가능
* 일반, 언래핑 변수 할당 가능

언래핑 변수는 옵셔널변수의 값을 매번 체크하는 번거러움을 없애려고 사용하고 클래스 초기화[^5] 시에 사용한다고 한다.

## Error Handling

이부분은 간단하게 보고 추후에 자세히

{% highlight swift %}
func makeASandwich() throws {
    // ...
}

do {
    try makeASandwich()
    eatASandwich()
} catch Error.OutOfCleanDishes {
    washDishes()
} catch Error.MissingIngredients(let ingredients) {
    buyGroceries(ingredients)
}
{% endhighlight %}

## Debugging with Assertions

자바의 assert 와 동일하게 디버깅이나 test시 사용하는듯 하다

{% highlight swift %}
let age = -3
assert(age >= 0, "A person's age cannot be less than zero")
// assertion failed: A person's age cannot be less than zero:...
{% endhighlight %}

---

[^1]: PHP 같은것도 해보긴 했지만 성격이 다르니 안해본걸로 친다.
[^2]: 잠시 맥이 없는관계로 [여기](https://swiftlang.ng.bluemix.net/){:target="_blank"}를 통해서 연습해 보았다.
[^3]: java의 null과 거의 비슷한 의미인듯 하다.
[^4]: 명시적으로는 `nil`할당은 가능하지만 `nil`을 가진 옵셔널 변수를 언래핑 하면 런타임 에러
[^5]: [여기](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language/AutomaticReferenceCounting.html){:target="_blank"}에 자세한 설명이 있는데.. 추후에 보강
