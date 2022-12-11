---
layout: post
title: defer와 panic()
subtitle: GO
date: '2022-12-11 00:00:01 +0900'
categories: study
tags: go
image:
  path: /assets/img/study_Go/main.PNG
---

# defer와 panic()
defer와 panic()에 대해 알아보자.

<!--more-->

## 지연 처리 defer
---
**Go언어**의 다양한 용법중에서도 '문법'에 해당되는 내용을 학습했습니다. 용법이 문법을 포함하는 뜻이지만, **용법과 문법**은 `사용에 있어서 차이`가 있습니다. <br>
**용법**은 `어떠한 것을 사용하는 방법이자 전체적인 흐름을 고려했을 때 마땅히 해야하는 것`이고, 프로그래밍 언어에서의 **문법**은 `어떠한 기능과 구문을 사용하기 위해 반드시 따라야하는 규칙`을 말합니다. <br>

## 마지막에 꼭 실행하는 defer
---
**defer**는 `함수 앞에 쓰이는 키워드`로써 특정 문장 혹은 함수를 감싸고 있는 `함수 내에서 제일 나중에, 끝나기 직전에 실행하게 하는 용법`입니다. <br>
**Java**를 사용해본 개발자는 `try ~finally 구문과 유사한 기능`을 한다고 하면 감이 올 것입니다. <br>
```java
try {
	메모리 할당 및 구문 실행
} catch {
	예외 처리(논리적 오류)
} finally {
	마지막에 꼭 실행 및 할당된 공간 반납
}
```
보기에도 형식이 확실히 정해져있다는 느낌이 들 것입니다. 하지만 **defer**는 블록이 필요한 것도 아니고 특정 위치나 형식이 필요한 것도 아닙니다. 단지 `함수 앞에 defer를 명시함으로써 사용`하는 것입니다. 
프로그램의 흐름에 분기가 많거나 '예외 처리'가 많아 복잡할 때 유용하게 사용합니다. defer를 사용하면 `흐름 중간에 에러(예외)가 발생해도 마지막에 꼭 실행하고 프로그램을 종료하지 않는 것`입니다. <br>
```go
package main

import "fmt"

func main() {
	defer fmt.Println("world")
    fmt.Println("Hello")
}
```
다시말하지만 defer는 프로그램을 실행하면서 예상하지 못한 에러('panic')가 발생 했을 때 프로그램을 종료하지 않고 defer구문을 실행할 때 유용하게 쓰입니다.
```go
package main

import	"fmt"

func main() {
	var a, b int = 10, 0
	defer fmt.Println("Done")
	
	result := a / b
	fmt.Println(result)	
}
```
어떤 수를 0으로 나누면서 에러가 발생합니다. 이는 **패닉 에러**에 대표적인 예입니다. 코드의 `문법상으로는 전혀 문제 되는 것이 없습니다.` 그런데 `프로그램이 시작되고 연산을 하면 에러가 발생`하게 됩니다. 이때 에러가 발생하고 바로 종료되는 것이 아니라 `미리 선언해두었던 defer 구문이 마지막으로 실행되고 종료`되는 것입니다. 그리고 만약에 **defer 구문**을 에러가 발생하는 코드 뒤에 선언하면 호출되지 않고 프로그램이 종료됩니다. 따라서 `에러가 발생하는 코드 전에 선언`해야합니다. <br>
그럼 `"defer를 사용한 함수들이 여러개면 어떤 함수가 먼저 호출되는걸까?"` 이 궁금증을 해소하기 위해서 아래 코드를 바로 실행해보세요. <br>
```go
package main

import "fmt"

func hello() {
	fmt.Println("Hello")
}

func world() {
	fmt.Println("world")
}

func main() {
	defer world()
	hello()
	
	for i := 0; i <3; i++ {
		defer fmt.Println(i)
	}
}
```
defer를 사용한 함수가 역순으로 실행되는 것을 알 수 있습니다. 이것은 자료구조의 스택(LIFO)과 동일한 것인데, 제일 나중에 지연 호출한 함수가 제일 먼저 실행되는 것입니다. <br>

**다양한 용법** 그중에 `파일에서 주로 사용`됩니다. 왜냐하면 `파일을 열거나 읽어들이면서 에러가 발생하면 파일을 닫을 수 없게 되기 때문`입니다. 물론 다른 부분에도 많이 사용되지만 **파일 입/출력에는 꼭 필요한 '용법'이라는 것**을 알아두기를 바랍니다. <br>
```go
package main
 
import (
	"fmt"
	"os"
)

func Helloworld() {
	file, err := os.Open("test.txt")
	defer file.Close()

	if err != nil { // 열 때
		fmt.Println(err)
		return
	}

	buf := make([]byte, 1024)
	
	if _, err = file.Read(buf); err != nil { // 읽을 때
		fmt.Println(err)
		return
	}

	fmt.Println(string(buf))
}

func main() {
	Helloworld()
	fmt.Println("Done")
}
```
프로그램이 오류가 발생하더라도 defer 키워드를 사용해 파일을 닫고 다음 코드를 실행할 수 있는 것입니다.

![사진](/assets/img/study_Go/221211/1.png)
설치 없이 바로 실행 가능한 클라우드 IDE인 구름IDE를 이용해 디렉터리에 test.txt파일을 생성하고 실행해본 결과입니다. test.txt에 아무것도 입력하지 않고 실행했을 때 "EOF"라고 에러가 출력되고 프로그램이 종료되는 것이 아니라 "Done"이 출력됩니다. 

![사진](/assets/img/study_Go/221211/2.png)
이번엔 test.txt에 "Hello world!"를 입력하고 실행한 결과입니다. 에러 처리가 되지 않았기 때문에 실행된 다음 "Done"이 출력되는 것을 확인할 수 있습니다.

## 종료하는 panic(), 복구하는 recover()
---
**panic**은 `겉으로 보이게 아무런 문제가 없는데 실행해보니 에러가 발생`해서 프로그램을 종료하는 기능을 합니다. 반대로 말하자면 문법 자체를 잘못 입력했을 때 발생하는 에러는 panic이 아닙니다. 이것은 바로 '오류'와 '예외'의 **차이**입니다. **오류**는 `프로그램상 허용하지 않는 문법과 같은 비정상적인 상황에 발생`하는 것을 말합니다. 예를 들어, int형 변수에 30.5를 초기화 하면 오류가 발생합니다. 그리고 **예외**는 `프로그램이 실행되면서 논리상으로 부적합한 상황이 발생`하는 것을 말합니다. 예를 들어, 나눗셈을 할 때 10 / 0은 논리적 예외 상황인 것입니다. 따라서 이러한 것들은 프로그램이 오류라고 생각하지 않기 때문에 코드 상에서 따로 예외 처리를 해야합니다. <br>
```go
package main

import	"fmt"

func main() {
	var num int = 10.5 //문법적인 오류
	fmt.Println(num)	
}
```
```go
package main

import	"fmt"

func main() {
	var num1, num2 int = 10, 0
	fmt.Println(num1 / num2) // 나누기 0꼴로 예외 상황
}
```
만약에 panic이 발생한 함수 안에 defer 구문이 있다면 프로그램을 종료하기 전에 defer 구문을 실행하고 종료합니다. <br>
```go
package main

import "fmt"

func panicTest() {
	var a = [4]int{1,2,3,4}
	
	defer fmt.Println("Panic done")
	
	for i := 0; i < 10; i++ {
		fmt.Println(a[i])
	}		
}

func main() {
	panicTest()

	fmt.Println("Hello, world!")
}
```
배열의 개수보다 큰 인덱스 값을 접근함으로써 panic이 발생하고 프로그램이 종료됩니다.
panic 에러가 발생하는 코드 전에 선언되었기 때문에 프로그램이 종료되기 전에 "Panic done"이 출력되고 종료됩니다. 따라서 `"Hello, world!"는 실행되지 않습니다.(panic이 발생해 프로그램이 종료돼서)` <br>
또한, **panic**은 `에러뿐만 아니라 사용자가 panic() 함수를 이용해 예외 상황일때 직접 panic 에러를 발생`시킬수 있습니다. 마치 **다른 언어**에 `throws문 같습니다.` 여기서 panic() 함수 안에 에러 메시지를 사용자 설정으로 출력할 수 있습니다. <br>
```go
package main

import "fmt"

func main() {
    var opt int
    var num1, num2, result float32

    fmt.Print("1.덧셈 2.뺄셈 3.곱셈 4.나눗셈 선택:")
    fmt.Scan(&opt)
	if opt != 1 && opt != 2 && opt != 3 && opt != 4 {
		panic("1, 2, 3, 4중에 하나만 입력해야합니다!")
	}
    fmt.Print("두 개의 실수 입력:")
    fmt.Scan(&num1, &num2)

    if opt == 1 {
        result = num1 + num2
    } else if opt == 2 {
        result = num1 - num2
    } else if opt == 3 {
        result = num1 * num2
    } else if opt == 4 {
        result = num1 / num2
    }
	
    fmt.Printf("결과: %f\n", result)
}
```
이렇게 panic() 함수는 프로그램 흐름에서 에러로 처리하고 싶은 부분에 개발자의 설정으로 사용할 수 있습니다. <br>

## panic을 막는 recover() 함수
---
**recover() 함수**의 역할은 `panic 상황이 생겼을 때 프로그램을 종료하지 않고 예외 처리`를 하는 것입니다. panic() 함수와 recover() 함수를 사용해 프로그램 흐름을 사용자가 미리 예외처리를 할 수 있는데 위에서 언급한 것처럼 panic 상황에서 프로그램이 종료되지 않고 어떤 구문을 실행시키려면 defer 구문을 사용해야합니다. <br>
따라서 예외 처리를 하기 위해서는 `recover() 함수와 defer 구문을 항상 같이 사용`해야합니다.
```go
package main

import "fmt"

func panicTest() {
	defer func() {
		r := recover() //복구 및 에러 메시지 초기화
		fmt.Println(r) //에러 메시지 출력 
	}()
	
    var a = [4]int{1,2,3,4}
    
    for i := 0; i < 10; i++ { //panic 발생
        fmt.Println(a[i])
    }       
}

func main() {
    panicTest()

    fmt.Println("Hello, world!") // panic이 발생했지만 계속 실행됨
}
```
쉽게 말해 recover() 함수는
```
1. panic이 발생해 프로그램이 종료되는 것을 막고 복구합니다.
2. 프로그램이 종료되기 전에 실행되어야 함으로 defer 가 선언된 함수 안에서 쓰입니다.
3. 에러 메시지를 반환합니다. 따라서 변수에 초기화해서 에러 메시지를 출력할 수 있습니다. 변수에 초기화하지 않으면 따로 에러 메시지를 출력하지 않습니다. 
```
```go
package main

import "fmt"

func main() {
	defer func() {
		if r := recover(); r != nil{
			fmt.Println(r)
			
			main()
		}		
	}()
	
	var num1, num2 int
	fmt.Scanln(&num1, &num2)
	
	result := num1 / num2

	fmt.Println(result)
}
```
처음에 말했던 try ~finally 구문을 통해 정리해보자면, 
```go
try(블럭) = 함수 단위,
catch(예외처리) = recover(),
finally(마지막) = defer,
throws(예외) = panic()
```