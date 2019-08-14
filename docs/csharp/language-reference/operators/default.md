---
title: 기본 연산자 - C# 참조
ms.custom: seodec18
description: 기본 연산자를 사용하여 형식의 기본값을 생성합니다.
ms.date: 08/01/2019
helpviewer_keywords:
- default keyword [C#]
ms.openlocfilehash: 5623cb9dc3790b5bb99635c41cb3f122f4c71d8e
ms.sourcegitcommit: bbfcc913c275885381820be28f61efcf8e83eecc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2019
ms.locfileid: "68796942"
---
# <a name="default-operator-c-reference"></a><span data-ttu-id="2c45a-103">기본 연산자(C# 참조)</span><span class="sxs-lookup"><span data-stu-id="2c45a-103">default operator (C# reference)</span></span>

<span data-ttu-id="2c45a-104">`default` 연산자는 형식의 [기본값](../keywords/default-values-table.md)을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2c45a-104">The `default` operator produces the [default value](../keywords/default-values-table.md) of a type.</span></span> <span data-ttu-id="2c45a-105">`default` 연산자에 대한 인수는 형식 또는 형식 매개 변수의 이름이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c45a-105">The argument to the `default` operator must be the name of a type or a type parameter.</span></span>

<span data-ttu-id="2c45a-106">다음 예제에서는 `default` 연산자의 사용법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c45a-106">The following example shows the usage of the `default` operator:</span></span>

[!code-csharp-interactive[default of T](~/samples/csharp/language-reference/operators/DefaultOperator.cs#WithOperand)]

<span data-ttu-id="2c45a-107">또한 `default` 키워드를 [`switch` 문](../keywords/switch.md) 내의 기본 사례 레이블로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c45a-107">You also use the `default` keyword as the default case label within the [`switch` statement](../keywords/switch.md).</span></span>

## <a name="default-literal"></a><span data-ttu-id="2c45a-108">기본 리터럴</span><span class="sxs-lookup"><span data-stu-id="2c45a-108">default literal</span></span>

<span data-ttu-id="2c45a-109">C# 7.1부터 `default` 리터럴을 사용하여 컴파일러가 식 형식을 유추할 수 있는 경우 형식의 기본값을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c45a-109">Beginning with C# 7.1, you can use the `default` literal to produce the default value of a type when the compiler can infer the expression type.</span></span> <span data-ttu-id="2c45a-110">`default` 리터럴 식은 `T`가 추론된 형식은 `default(T)` 식과 동일한 값을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="2c45a-110">The `default` literal expression produces the same value as the `default(T)` expression where `T` is the inferred type.</span></span> <span data-ttu-id="2c45a-111">다음과 같은 경우에 `default` 리터럴 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c45a-111">You can use the `default` literal in any of the following cases:</span></span>

- <span data-ttu-id="2c45a-112">변수의 할당 또는 초기화에서</span><span class="sxs-lookup"><span data-stu-id="2c45a-112">In the assignment or initialization of a variable.</span></span>
- <span data-ttu-id="2c45a-113">선택적 메서드 매개 변수에 대한 기본값 선언에서</span><span class="sxs-lookup"><span data-stu-id="2c45a-113">In the declaration of the default value for an optional method parameter.</span></span>
- <span data-ttu-id="2c45a-114">인수 값을 제공하기 위한 메서드 호출에서</span><span class="sxs-lookup"><span data-stu-id="2c45a-114">In a method call to provide an argument value.</span></span>
- <span data-ttu-id="2c45a-115">`return` 문에서 또는 식 본문 멤버의 식으로</span><span class="sxs-lookup"><span data-stu-id="2c45a-115">In a `return` statement or as an expression in an expression-bodied member.</span></span>

<span data-ttu-id="2c45a-116">다음 예제에서는 `default` 리터의 사용법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="2c45a-116">The following example shows the usage of the `default` literal:</span></span>

[!code-csharp-interactive[default literal](~/samples/csharp/language-reference/operators/DefaultOperator.cs#DefaultLiteral)]

## <a name="c-language-specification"></a><span data-ttu-id="2c45a-117">C# 언어 사양</span><span class="sxs-lookup"><span data-stu-id="2c45a-117">C# language specification</span></span>

<span data-ttu-id="2c45a-118">자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [기본값 식](~/_csharplang/spec/expressions.md#default-value-expressions) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c45a-118">For more information, see the [Default value expressions](~/_csharplang/spec/expressions.md#default-value-expressions) section of the [C# language specification](~/_csharplang/spec/introduction.md).</span></span>

<span data-ttu-id="2c45a-119">`default` 리터럴에 대한 자세한 내용은 [기능 제안 노트](~/_csharplang/proposals/csharp-7.1/target-typed-default.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c45a-119">For more information about the `default` literal, see the [feature proposal note](~/_csharplang/proposals/csharp-7.1/target-typed-default.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2c45a-120">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2c45a-120">See also</span></span>

- [<span data-ttu-id="2c45a-121">C# 참조</span><span class="sxs-lookup"><span data-stu-id="2c45a-121">C# reference</span></span>](../index.md)
- [<span data-ttu-id="2c45a-122">C# 연산자</span><span class="sxs-lookup"><span data-stu-id="2c45a-122">C# operators</span></span>](index.md)
- [<span data-ttu-id="2c45a-123">기본값 표</span><span class="sxs-lookup"><span data-stu-id="2c45a-123">Default values table</span></span>](../keywords/default-values-table.md)