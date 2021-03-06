---
title: <bindings>
ms.date: 01/22/2018
ms.assetid: b62cd369-5409-4030-8490-9759a462dd3a
ms.openlocfilehash: fe8f620668e35183890b8bba1f254a74c962f8d3
ms.sourcegitcommit: fbb8a593a511ce667992502a3ce6d8f65c594edf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/16/2019
ms.locfileid: "74139668"
---
# <a name="bindings"></a>\<바인딩 >

`bindings` 요소를 사용 하 여 WCF (Windows Communication Foundation)에 대 한 표준 및 사용자 지정 바인딩의 컬렉션을 구성할 수 있습니다. 각 항목은 고유한 `binding`으로 식별될 수 있는 `name` 요소입니다. 서비스에서는 `name`을 통해 바인딩을 연결하여 바인딩을 사용합니다. .NET Framework 4부터 바인딩과 동작은 이름을 가질 필요가 없습니다. 기본 구성 및 이름이 없는 바인딩 및 동작에 대 한 자세한 내용은 [WCF 서비스에 대 한](../../../wcf/samples/simplified-configuration-for-wcf-services.md) [간소화 된 구성](../../../wcf/simplified-configuration.md) 및 단순화 된 구성을 참조 하세요.

## <a name="system-provided-bindings"></a>시스템 제공 바인딩

시스템 제공 바인딩은 WCF 메시지 스택의 복잡성을 숨깁니다. 시스템 제공 바인딩을 사용하는 애플리케이션은 스택을 완전히 제어할 필요가 없습니다. 각 시스템 제공 바인딩에는 바인딩이 처리하는 사용 시나리오에 가장 적합한 특성이 노출됩니다.

각 시스템 제공 바인딩의 구성 섹션은 바인딩 구성에 사용되는 일부 구성을 정의할 수 있습니다. 각 구성은 고유한 이름으로 식별됩니다.

시스템 제공 바인딩에는 요소나 특성을 추가할 수 없습니다. 이렇게 하려면 [사용자 지정](#custom-bindings) 바인딩 섹션에 설명 된 대로 사용자 지정 바인딩을 구현 해야 합니다. 시스템에서 제공 하는 바인딩을 완벽 하 게 모방 하는 사용자 지정 바인딩을 정의 하 고 사용자 응용 프로그램에서 제어를 원하는 몇 가지 설정을 추가할 수 있습니다.  

시스템 제공 바인딩 목록은 [시스템 제공 바인딩](../../../wcf/system-provided-bindings.md)을 참조 하세요.

## <a name="custom-bindings"></a>사용자 지정 바인딩

사용자 지정 바인딩은 WCF 메시징 스택에 대한 모든 권한을 제공합니다. 개별 바인딩은 스택에 표시 되는 순서 대로 스택 요소에 대 한 구성 요소를 지정 하 여 메시지 스택을 정의 합니다. 각 요소는 스택의 한 요소를 정의 하 고 구성 합니다. 각 사용자 지정 바인딩에는 `transport` 요소가 하나만 있어야 합니다. 이 요소가 없으면 메시징 스택이 완전 하지 않습니다.

스택에서 요소가 표시 되는 순서는 작업이 메시지에 적용 되는 순서 이기 때문에 중요 합니다. 다음과 같은 스택 요소 순서를 사용해야 합니다.  

1. 트랜잭션 (옵션)  

2. 안정적인 메시징 (옵션)  

3. 보안 (선택 사항)  

4. 인코더  

5. 전송  

 사용자 지정 바인딩은 `name` 특성으로 식별됩니다. 사용자 지정 바인딩에 대 한 자세한 내용은 [사용자 지정 바인딩](../../../wcf/extending/custom-bindings.md)을 참조 하세요.

## <a name="see-also"></a>참조

- <xref:System.ServiceModel.Configuration.BindingsSection?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.Binding?displayProperty=nameWithType>
- <xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType>
- [바인딩](../../../wcf/bindings.md)
- [사용자 지정 바인딩](../../../wcf/extending/custom-bindings.md)
- [\<customBinding >](custombinding.md)
