---
layout: post
title: Swift 정리 - Basic Operators
date: 2016-04-27 17:25:00 +0900
categories: ["dev","swift"]
--- 

연산자들은 여타 언어들이 그렇듯 비슷비슷하다.

`+,-,*,/,%,+=,-=,=,==,!=,>=,<=,<,>`와 논리연산자에 대한 설명은 과감히 생략

단, `question ? answer1 : answer2` 과 같은 삼항연산자의 경우 **Deprecated** 되어 Swift 3.0에서는 삭제될 예정이라고 들었다. 가급적 사용을 자제하자.. 나는 자주쓰는데 이거 ㅠㅠ

---

## Nil Coalescing Operator

`nil` 체크의 단축형


{% highlight swift %}
let defaultColorName = "red"
var userDefinedColorName: String?   // defaults to nil
 
var colorNameToUse = userDefinedColorName ?? defaultColorName
print(colorNameToUse) // red

userDefinedColorName = "green"
colorNameToUse = userDefinedColorName ?? defaultColorName
print(colorNameToUse) // green
{% endhighlight %}

## Closed Range Operator

`a...b`를 사용하면 a 에서 b까지의 범위에 대해서 변수 사용이 가능하다.

{% highlight swift %}
for index in 1...5 {
    print(index)
}
//1
//2
//3
//4
//5
{% endhighlight %}

## Half-Open Range Operator

`a..<b`를 사용하면 a 에서 b-1까지의 범위에 대해서 변수 사용이 가능하다.

`array` 와 같은 `count-1` 해야 할 경우 유용

{% highlight swift %}
for index in 1..<5 {
    print(index)
}
//1
//2
//3
//4
{% endhighlight %}