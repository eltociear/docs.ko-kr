---
title: F#의 함수형 프로그래밍 소개
description: 에서 F#함수형 프로그래밍에 대 한 기본 사항을 알아봅니다.
ms.date: 10/29/2018
ms.openlocfilehash: e1a0edc61dbe13012c48e166d490e22ebc70d6a0
ms.sourcegitcommit: 14ad34f7c4564ee0f009acb8bfc0ea7af3bc9541
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73424704"
---
# <a name="introduction-to-functional-programming-in-f"></a>F\#의 함수형 프로그래밍 소개

함수형 프로그래밍은 함수 및 변경할 수 없는 데이터의 사용을 강조 하는 프로그래밍의 스타일입니다. 형식화 된 함수형 프로그래밍은 함수형 프로그래밍이와 F#같은 정적 형식과 결합 된 경우입니다. 일반적으로 함수형 프로그래밍에서는 다음 개념을 강조 합니다.

* 사용 하는 기본 구문으로 함수 사용
* 문 대신 식
* 변수에 대 한 변경할 수 없는 값
* 명령적 프로그래밍에 대 한 선언적 프로그래밍

이 시리즈 전체에서를 사용 하 여 F#함수형 프로그래밍의 개념과 패턴을 살펴볼 수 있습니다. 이 과정에서 몇 가지 F# 방법을 배우게 될 것입니다.

## <a name="terminology"></a>용어

다른 프로그래밍 패러다임과 마찬가지로 함수형 프로그래밍에는 결국 학습 해야 하는 어휘가 제공 됩니다. 다음은 전체 시간을 볼 수 있는 몇 가지 일반적인 용어입니다.

* **함수** -함수는 입력이 제공 될 때 출력을 생성 하는 구문입니다. 공식적으로는 한 집합에서 다른 집합으로 항목을 _매핑합니다_ . 특히 데이터 컬렉션에 대해 작동 하는 함수를 사용 하는 경우이 정해진는 구체적으로 구체적으로 리프트 됩니다. 함수형 프로그래밍의 가장 기본적인 (및 중요 한) 개념입니다.
* **식** -식은 값을 생성 하는 코드의 구문입니다. 에서 F#이 값은 바인딩되어야 하거나 명시적으로 무시 해야 합니다. 식은 함수 호출로 일반적으로 바꿀 수 있습니다.
* **순도** -순도는 동일한 인수에 대해 해당 반환 값이 항상 동일 하 고 해당 계산에 부작용이 없도록 하는 함수의 속성입니다. 순수 함수는 해당 인수에 전적으로 종속 됩니다.
* **참조 투명성** -참조 투명성은 프로그램의 동작에 영향을 주지 않고 출력으로 바꿀 수 있도록 식의 속성입니다.
* **불변성** -불변성은 내부에서 값을 변경할 수 없음을 의미 합니다. 이는 현재 위치가 변경 될 수 있는 변수와 대조 됩니다.

## <a name="examples"></a>예제

다음 예에서는 이러한 핵심 개념을 보여 줍니다.

### <a name="functions"></a>함수

함수형 프로그래밍에서 가장 일반적이 고 기본적인 구문은 함수입니다. 1을 정수에 더하는 간단한 함수는 다음과 같습니다.

```fsharp
let addOne x = x + 1
```

해당 형식 시그니처는 다음과 같습니다.

```fsharp
val addOne: x:int -> int
```

시그니처는 "`addOne` `x` `int`를 수락 하 고 `int`를 생성 하는"으로 읽을 수 있습니다. 보다 공식적으로 `addOne` 정수 집합의 값을 정수 집합에 _매핑합니다_ . `->` 토큰은이 매핑을 나타냅니다. F#에서는 일반적으로 함수 시그니처를 확인 하 여 수행 되는 작업에 대 한 의미를 얻을 수 있습니다.

그렇다면 서명이 중요 한 이유는 무엇 인가요? 형식화 된 함수형 프로그래밍에서 함수 구현은 실제 형식 서명 보다 중요 하지 않습니다. 값 1을 정수에 추가 `addOne`는 것은 런타임에 유용 하지만 프로그램을 생성 하는 경우에는이 함수를 사용 하는 방법에 `int` 대 한 정보를 제공 합니다. 또한이 함수를 올바르게 사용 하는 경우 (형식 시그니처를 기준으로) 문제를 진단 하는 작업은 `addOne` 함수 본문 내 에서만 수행할 수 있습니다. 형식화 된 함수형 프로그래밍의 자극 제입니다.

### <a name="expressions"></a>표현식

식은 값으로 계산 되는 구문입니다. 작업을 수행 하는 문과 달리 식은 값을 다시 제공 하는 작업을 수행 하는 것으로 간주할 수 있습니다. 식은 함수형 프로그래밍의 문을 위해 거의 항상 사용 됩니다.

`addOne`이전 함수를 살펴보겠습니다. `addOne`의 본문은 식입니다.

```fsharp
// 'x + 1' is an expression!
let addOne x = x + 1
```

`addOne` 함수의 결과 유형을 정의 하는이 식의 결과입니다. 예를 들어이 함수를 구성 하는 식은 `string`같은 다른 형식으로 변경 될 수 있습니다.

```fsharp
let addOne x = x.ToString() + "1"
```

함수 시그니처는 이제 다음과 같습니다.

```fsharp
val addOne: x:'a -> string
```

의 F# 모든 형식이 `ToString()` 호출 될 수 있으므로 `x`의 형식은 제네릭 ( [자동 일반화](../language-reference/generics/automatic-generalization.md)라고 함)로 설정 되 고 결과 형식은 `string`입니다.

식은 단순히 함수의 본문이 아닙니다. 다른 곳에서 사용 하는 값을 생성 하는 식을 사용할 수 있습니다. 일반적인 항목은 `if`입니다.

```fsharp
// Checks if 'x' is odd by using the mod operator
let isOdd x = x % 2 <> 0

let addOneIfOdd input =
    let result =
        if isOdd input then
            input + 1
        else
            input

    result
```

`if` 식은 `result`라는 값을 생성 합니다. `result`를 완전히 생략 하 여 `if` 식을 `addOneIfOdd` 함수의 본문으로 만들 수 있습니다. 식에 대해 기억해 야 할 중요 한 점은 값을 생성 한다는 것입니다.

반환할 항목이 없을 때 사용 되는 특별 한 형식 `unit`가 있습니다. 예를 들어 다음과 같은 간단한 함수를 살펴보겠습니다.

```fsharp
let printString (str: string) =
    printfn "String is: %s" str
```

시그니처는 다음과 같습니다.

```fsharp
val printString: str:string -> unit
```

`unit` 형식은 반환 되는 실제 값이 없음을 나타냅니다. 이는 해당 작업의 결과로 반환할 값이 없는 경우에도 "작업 수행" 해야 하는 루틴이 있는 경우에 유용 합니다.

이는 동일한 `if` 구문이 문이 고 값을 생성 하는 것이 일반적으로 변경 변수를 사용 하 여 수행 되는 명령형 프로그래밍과 매우 대조 됩니다. 예를 들어에서 C#코드는 다음과 같이 작성 될 수 있습니다.

```csharp
bool IsOdd(int x) => x % 2 != 0;

int AddOneIfOdd(int input)
{
    var result = input;

    if (IsOdd(input))
    {
        result = input + 1;
    }

    return result;
}
```

및 기타 C 스타일 언어 C# 는 식 기반 조건부 프로그래밍을 허용 하는 [삼항 식을](../../csharp/language-reference/operators/conditional-operator.md)지원 합니다.

함수형 프로그래밍에서는 문을 사용 하 여 값을 변경할 경우는 거의 없습니다. 일부 기능 언어는 문과 변형을 지원 하지만 함수형 프로그래밍에서 이러한 개념을 사용 하는 것은 일반적이 지 않습니다.

### <a name="pure-functions"></a>순수 함수

앞에서 설명한 것 처럼 순수 함수는 다음을 수행 하는 함수입니다.

* 항상 동일한 입력에 대해 동일한 값으로 평가 됩니다.
* 부작용이 없습니다.

이 컨텍스트에서 수학 함수를 생각해 보면 유용 합니다. 수학에서 함수는 해당 인수에만 종속 되며 의도 하지 않은 결과가 발생 하지 않습니다. 수치 연산 함수 `f(x) = x + 1``f(x)` 값은 `x`값에만 종속 됩니다. 함수형 프로그래밍의 순수 함수는 동일한 방식입니다.

순수 함수를 작성 하는 경우 함수는 해당 인수에만 종속 되어야 하며 부작용이 발생 하는 작업을 수행 하지 않아야 합니다.

다음은 전역적이 고 변경 가능한 상태에 종속 되기 때문에 비 순수 함수의 예제입니다.

```fsharp
let mutable value = 1

let addOneToValue x = x + value
```

`addOneToValue` 함수는 한 번에 1과 다른 값을 갖도록 변경 될 수 `value` 있으므로 명확 하 게 비 순수형. 전역 값에 따라이 패턴은 함수형 프로그래밍에서 피할 수 있습니다.

다음은 파생 작업을 수행 하기 때문에 비 순수 함수의 또 다른 예입니다.

```fsharp
let addOneToValue x =
    printfn "x is %d" x
    x + 1
```

이 함수는 전역 값에 의존 하지 않지만 `x`의 값을 프로그램의 출력에 씁니다. 이 작업을 수행 하는 경우 기본적으로 잘못 된 것은 아니지만 함수는 순수 하지 않습니다. 프로그램의 다른 부분이 출력 버퍼와 같은 프로그램 외부에 종속 된 경우이 함수를 호출 하면 프로그램의 다른 부분에 영향을 줄 수 있습니다.

`printfn` 문을 제거 하면 함수를 순수 하 게 만들 수 있습니다.

```fsharp
let addOneToValue x = x + 1
```

이 함수는 기본적으로 `printfn` 문을 사용 하는 이전 버전 보다 _더 나은_ 것은 아니지만이 함수는 모든 함수에서 값을 반환 하는 것을 보장 합니다. 이 함수를 여러 번 호출 하면 동일한 결과가 생성 됩니다. 값만 생성 됩니다. 순도로 제공 되는 예측 가능성은 프로그래머가 많은 기능을 제공 합니다.

### <a name="immutability"></a>불변성

마지막으로 형식화 된 함수형 프로그래밍의 가장 기본적인 개념 중 하나는 불변성입니다. 에서 F#모든 값은 기본적으로 변경할 수 없습니다. 즉, 변경 가능한 것으로 명시적으로 표시 하지 않는 한 내부에서 변경할 수 없습니다.

실제로 변경할 수 없는 값을 사용 하 여 작업 하는 방법은 "항목을 변경 해야 합니다."를 "새 값을 생성 해야 합니다."에서 프로그래밍 방식으로 변경 하는 것을 의미 합니다.

예를 들어 값에 1을 추가 하면 기존 값을 변경 하는 것이 아니라 새 값이 생성 됩니다.

```fsharp
let value = 1
let secondValue = value + 1
```

에서 F#다음 코드는 `value` 함수를 변경할 **수** 없습니다. 대신, 같음 검사를 수행 합니다.

```fsharp
let value = 1
value = value + 1 // Produces a 'bool' value!
```

일부 함수형 프로그래밍 언어에서는 변형을 지원 하지 않습니다. F#에서는 지원 되지만 값에 대 한 기본 동작은 아닙니다.

이 개념은 데이터 구조를 더욱 확장 합니다. 함수형 프로그래밍에서 집합 (및 기타)과 같은 변경할 수 없는 데이터 구조에는 처음에는 것과 다른 구현이 있습니다. 개념적으로 집합에 항목을 추가 하는 것과 같은 항목은 집합을 변경 하지 않으며 추가 된 값을 사용 하 여 _새_ 집합을 생성 합니다. 내부적으로는 데이터의 적절 한 표현을 결과로 제공할 수 있도록 값을 효율적으로 추적할 수 있도록 하는 다른 데이터 구조를 통해이 작업을 수행 하는 경우가 많습니다.

이러한 스타일의 값과 데이터 구조를 사용 하는 것이 중요 합니다 .이는 해당 항목의 새 버전을 만드는 것 처럼이를 수정 하는 작업을 강제로 처리 하기 때문입니다. 따라서 프로그램에서 같음 및 작음 비교 가능 같은 작업을 일관 되 게 수행할 수 있습니다.

## <a name="next-steps"></a>다음 단계

다음 섹션에서는 함수 프로그래밍에 사용할 수 있는 다양 한 방법을 탐색 하는 함수를 철저히 설명 합니다.

[첫 번째 클래스 함수](first-class-functions.md) 는 함수를 많이 탐색 하 여 다양 한 컨텍스트에서 사용할 수 있는 방법을 보여 줍니다.

## <a name="further-reading"></a>추가 정보

함수형 [시리즈는를 사용한](https://fsharpforfunandprofit.com/posts/thinking-functionally-intro/) F#함수형 프로그래밍에 대해 배우는 또 다른 유용한 리소스입니다. 개념을 설명 하는 기능을 사용 하 여 F# 실용적이 고 읽기 쉬운 방식으로 함수형 프로그래밍의 기본 사항을 다룹니다.
