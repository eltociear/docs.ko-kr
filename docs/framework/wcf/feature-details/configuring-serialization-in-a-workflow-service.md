---
title: 워크플로 서비스에서 Serialization 구성
ms.date: 03/30/2017
ms.assetid: aa70b290-a2ee-4c3c-90ea-d0a7665096ae
ms.openlocfilehash: f894f2e044e35bb278f975ef2385a6b22a8bea49
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79185341"
---
# <a name="configuring-serialization-in-a-workflow-service"></a>워크플로 서비스에서 Serialization 구성
워크플로 서비스는 WCF(Windows 통신 재단) 서비스이므로 <xref:System.Runtime.Serialization.DataContractSerializer> (기본값) 또는 를 <xref:System.Xml.Serialization.XmlSerializer>사용할 수 있는 옵션이 있습니다. 워크플로가 아닌 서비스를 작성할 때 사용할 직렬화기 형식은 서비스 또는 작업 계약에서 지정됩니다. WCF 워크플로 서비스를 만들 때 코드에서 이러한 계약을 지정 하지 않고 오히려 계약 추론에 의해 런타임에 생성 됩니다. 계약 추론에 대한 자세한 내용은 [워크플로에서 계약 사용](../../../../docs/framework/wcf/feature-details/using-contracts-in-workflow.md)을 참조하십시오.  직렬화기는 <xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> 속성을 사용하여 지정됩니다. 다음 그림과 같이 디자이너에서 이 속성을 설정할 수 있습니다.  
  
 ![속성 창에서 SerializerOption 속성을 설정합니다.](./media/configuring-serialization-in-a-workflow-service/setting-serializer-property.png)  
  
 다음 예제와 같이 코드에서 직렬화기를 설정할 수도 있습니다.  
  
```csharp  
Receive approveExpense = new Receive  
            {  
                OperationName = "ApproveExpense",  
                CanCreateInstance = true,  
                ServiceContractName = "FinanceService",  
                SerializerOption = SerializerOption.DataContractSerializer,  
                Content = ReceiveContent.Create(new OutArgument<Expense>(expense))  
            };  
```  
  
  워크플로 서비스에서 알려진 형식도 지정할 수 있습니다. 알려진 형식에 대한 자세한 내용은 [데이터 계약 알려진 형식을](data-contract-known-types.md)참조하십시오. 디자이너나 코드에서 알려진 형식을 지정할 수 있습니다. 디자이너에서 알려진 형식을 지정하려면 다음 그림과 같이 활동에 대한 **속성 창의** <xref:System.ServiceModel.Activities.Receive> KnownType 속성 옆에 있는 타원 단추를 클릭합니다.
  
 ![알 수 있는 유형 속성 대화 상자의 스크린샷입니다.](./media/configuring-serialization-in-a-workflow-service/known-types-properties.png)  
  
 이렇게 하면 알려진 형식을 검색하고 지정할 수 있는 형식 컬렉션 편집기가 표시됩니다.  
  
 ![형식 컬렉션 편집기의 스크린샷입니다.](./media/configuring-serialization-in-a-workflow-service/type-collection-editor.gif)  
  
 새 **유형 추가** 링크를 클릭하고 드롭다운을 사용하여 알려진 형식 컬렉션에 추가할 유형을 선택하거나 검색합니다. 코드에서 알려진 형식을 지정하려면 다음 예제와 같이 <xref:System.ServiceModel.Activities.Receive.KnownTypes%2A> 속성을 사용합니다.  
  
```csharp
Receive approveExpense = new Receive  
            {  
                OperationName = "ApproveExpense",  
                CanCreateInstance = true,  
                ServiceContractName = "FinanceService",  
                SerializerOption = SerializerOption.DataContractSerializer,  
                Content = ReceiveContent.Create(new OutArgument<Expense>(expense))  
            };  
            approveExpense.KnownTypes.Add(typeof(Travel));  
            approveExpense.KnownTypes.Add(typeof(Meal));  
```
