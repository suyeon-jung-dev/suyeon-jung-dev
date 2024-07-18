# golang - grammar

- go는 대문자로 시작하는 이름만 export 된다. 외부에서 import 할때는 대문자로 시작하는 이름만 참조 할 수 있다.
  - go는 `factored import` 문을 통해 여러개의 import 문을 관호로 한번에 지정 할 수 있다.
```go
package main

import (
	"fmt"
	"math"
)

func main() {
	fmt.Println(math.Pi)
}
```

- go 는 변수 뒤에 type 을 붙인다.
Ref. https://go.dev/blog/declaration-syntax

```go
package main

import "fmt"

func add(x int, y int) int {
	return x + y
}

func main() {
	fmt.Println(add(12,34))
}

```

- 매개변수가 연속으로 같은 타입일때 마지막 매개변수 하나로 합쳐서 표현 할 수 있다.

```go
package main 

import "fmt"

func add(x, y int) int {
	return x + y
}

func main() {
	fmt.Println(add(12,34))
}
```

- go는 여러개의 리턴값을 가질 수 있다.
```go
package main

import "fmt"

func swap(x, y string) (string, string) { // golang 은 string 이 소문자
	return y, x
}

func main() {
	a, b := swap("1","2") // int - string 간 자동 형변환 안됨
	fmt.Println(a, b)
}
```

- go는 리턴값을 여러개 가질 수 있기 때문에, 'naked' return 값을 가질 수 있다. <br>
naked return 이란, 함수 시그니처에서 리턴값에 대한 변수명을 지정하면, 실제 함수 내에서 return 문 작성시 해당 값을 지정하지 않아도 함수 내에서 선언된 해당 변수명에 할당 된 값이 리턴된다.

> [!IMPORTANT]
> Naked return 문은 몇줄 안되는 간단한 함수에만 적용 되어야 한다. 가독성 때문!!

```go
package main

import "fmt"

func swap(x, y int) (a, b int) {
	a = y
	b = x
	return
}

func main() {
	result1, result2 := swap(1,2)
	fmt.Println(result1, result2)
	// NOTE - fmt.Println(swap(1,2)) 일때 오류 발생하는 것을 볼때, 인자 여럭개인 함수를 파라미터로 받지 못하는 것 같다.. 왜? 
}
```

- go 에서 var 는 변수 목록을 뜻한다.
```go
package main 

import "fmt"

var value1, value2 bool // 전역변수로 사용 가능

var value3, value4 int

func main() {
	fmt.Println(value1, value2, value3, value4)
}
```
- go 는 var 에서도 변수를 한번에 초기화 할 수 있다.
```go
package main

import "fmt"

var value1, value2, value3 int = 1,2,3

func main() {
	fmt.Println(value1, value2, value3)
}
```

- go는 또한 초기화 값이 존재하면, 초기화 값으로 자동으로 type 이 지정되기 때문에 type 생략이 가능하다.
```go
package main

import "fmt"

var value1, value2, value3 = 1,2,3 // int type 이 생략되어 있음

func main() {
	fmt.Println(value1,value2,value3)
}
```
- go 에서는 변수 선언과 type 생략, 초기화 를 동시에 작성하는 경우 `:=` 라는 연산자를 사용하여 짧은 변수 선언을 할 수 있다. <br>
즉, `:=` 짧은 대입 연산자는 `var` 키워드와 동일 하다.
```go
package main

import "fmt"

func main() {
	value := 123
	fmt.Println(value)
}
```

- go 의 기본 자료형
  - bool
  - string
  - 정수형
    - int 
    - int8
    - int16
    - int32
    - int64
    - uint
    - uint8 (== byte)
    - uint16
    - uint32
    - uint64
    - uintptr
  - 실수형
      - float32
      - float64
      - complex64
      - complex128
  - 기타
    - bype (== uint8)
    - rune (== int32. UTF-8 인코딩의 유니코드 포인트를 표시하는 정수)

- type 변환시 T(v) 사용
```go
package main

import "fmt"

func main() {
	value1 := string(123)
	fmt.Println(value1)
	
	//value2 := int(123.123)  // float -> int 와 같은 강제 casting 은 명시적으로 형변환해도 오류 발생. 
	value3 := float64(1111)
	fmt.Println(value3)
}
```
- 추론 타입 Inference Type. 타입 지정없이 초기화 된 값의 타입에 따라 지정되는것. 초기화시 타입추론되면 이후 해당 타입의 값을 다른 타입으로 변경 불가. 처음 지정된 타입이 그대로 유지됨.
```go
package main

import "fmt"

func main() {
	v := 42 // change me!
	//v = 12.12 // NOTE - 타입 변경 불가!!
	fmt.Printf("v is of type %T\n", v)
}
```

- 상수는 `const` 키워드로 선언. `:=` 연산자 사용 불가능.
```go
package main

import "fmt"

const pi = 3.14
//const pi := 3.14 // NOTE - const 키워드는 := 와 함께 사용 불가능

func main() {
	fmt.Println("pi = ", pi)
}
```

- go 의 for문은 조건에 `()` 괄호가 없고, 함수 블록 `{}` 이 필수.
```go
package main

import "fmt"

func main() {
	for i := 0; i<10 ; i++ {
		fmt.Println(i)
    }
	fmt.Println("finish!!")
}
```

- go 의 for문은 초기화 구문, 사후구문은 공백 가능
```go
package main

import "fmt"

func main() {
	const j = 5
	i := 1
	for ; i <= j ; {
		fmt.Println(i)
		i++
    }
	fmt.Println("finish!!")
}
```

- go 에서는 for 문에서 초기화 구문, 사후 구문을 비워둘 수 있으므로 조건문만 선언 가능하다. 따라서 while 문 처럼 for를 사용 할 수 있다.
> 조건을 아무것도 지정하지 않으면 무한루프가 생성되니 주의!!
```go
package main

import "fmt"

func main() {
	i := 1
	for i <= 5 {
		fmt.Println(i)
		i++
    }
	
	fmt.Println("finish!!!")
}
```

- go의 if 문에서 조건 괄호 `()` 는 생략 가능하지만, 블록 괄호 `{}` 는 필수.
```go
package main

import "fmt"

func main() {
    const value = "VALUE"
	
	if value == "VALUE" {
		fmt.Println("equal!!! 👍")
    } else {
		fmt.Println("not equal 🥲")
    }
	fmt.Println("Finish!!!")
}
```

- go 는 if 조건문 앞에서 짧은 초기화 구문을 지정할 수 있다. 여기서 선언된 변수는 if 문 스코프 까지만 적용된다.
```go
package main

import "fmt"

func main() {
	if i:=0; i < 10 {
		fmt.Println(i)
		i++
    }
	//fmt.Println(i) // NOTE - if 조건 문 앞의 짧은 구문에 선언된 변수는 if 문 바깥에서 참조 할 수 없음
	fmt.Println("Finish!!!")
}
```

- go 의 if 문 앞의 짧은 구문에서 선언된 변수들은 해당 if문의 else 까지 참조 가능하다.
```go
package main

import "fmt"

func main() {
	if i := false; i == true {
		fmt.Println("TRUE!! :: i is ", i)
    } else {
		fmt.Println("FALSE!! :: i is ", i)
    }
	fmt.Println("Finish!!!")
}
```

- 실습 [작업중]
```go
package main

import (
  "fmt"
  "math"
)

func Sqrt(x float64) float64 {
  z := 1.0

  try := 5
  for i:=0; i<try; i++ {
    z -= (z*z - x) / (2*z)
    fmt.Printf("try #%v :: z is %v \n", int(i), float64(z))
  }

  return z
}

func main() {
  Sqrt(2)
  fmt.Println("Correct answer is ", math.Sqrt(2))

  Sqrt(4)
  fmt.Println("Correct answer is ", math.Sqrt(4))

  Sqrt(9)
  fmt.Println("Correct answer is ", math.Sqrt(9))
}
```

- 조금 다른 go의 switch문. go의 switch 문은 모든 case 문에 break 가 생략되어 있기 때문에 위에서 케이스가 선택되면 무조건 switch 문을 빠져나옵니다.
```go
package main

import "fmt"

func main() {
	switch i := 0 ; i {
    case 0: 
		fmt.Println(i)
		i++     // NOTE - i 가 1 로 변경이 되었지만, 케이스가 선택되면 다음 케이스는 진행하지 않습니다.
    case 1:
		fmt.Println(i)
		i++
    default:
		fmt.Println("default :: ", i)
    }
	
	fmt.Println("Finish!!")
}
```

