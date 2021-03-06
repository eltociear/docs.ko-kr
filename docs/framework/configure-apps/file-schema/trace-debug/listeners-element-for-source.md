---
title: <source>에 대한 <listeners> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners
helpviewer_keywords:
- listeners element for <source>
- <listeners> element for <source>
ms.assetid: a2991f43-b4d3-4614-a8e7-da392de9697f
ms.openlocfilehash: 0eee325e01b41a15a19e4f40f479596f9d70f73b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79153414"
---
# <a name="listeners-element-for-source"></a>\<청취자> 소스 \<> 대한 요소
<xref:System.Diagnostics.TraceSource>에 대한 컬렉션의 <xref:System.Diagnostics.TraceSource.Listeners%2A> 리스너를 추가하거나 제거합니다. 수신기는 추적 출력을 로그, 창 또는 텍스트 파일과 같은 적절한 대상으로 지시합니다.  
  
[**\<구성>**](../configuration-element.md)  
&nbsp;&nbsp;[**\<system.진단>**](system-diagnostics-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;[**\<소스>**](sources-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<소스>**](source-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<청취자>**  
  
## <a name="syntax"></a>구문  
  
```xml  
<listeners>
  <add>...</add>  
  <remove ... />  
  <clear/>  
</listeners>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 단원에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|Description|  
|-------------|-----------------|  
|[\<>추가](add-element-for-listeners-for-source.md)|`Listeners` 컬렉션에 수신기를 추가합니다.|  
|[\<>제거](remove-element-for-listeners-for-source.md)|컬렉션에서 수신기를 제거합니다. `Listeners`|  
|[\<클리어>](clear-element-for-listeners-for-source.md)|추적 소스의 `Listeners` 컬렉션을 지웁니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`system.diagnostics`|메시지를 수집하고 저장하고 라우팅하는 추적 수신기를 지정하며, 추적 스위치가 설정되는 수준을 지정합니다.|  
|`sources`|추적 메시지를 시작하는 추적 소스가 포함되어 있습니다.|  
|`source`|추적 메시지를 시작하는 추적 소스를 지정합니다.|  
  
## <a name="remarks"></a>설명  
  
## <a name="configuration-file"></a>구성 파일  
 이 요소는 컴퓨터 구성 파일(Machine.config) 및 응용 프로그램 구성 파일에서 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 `<listeners>` 요소를 사용하여 콘솔 추적 수신기를 소스에 `mySource` 추가하고 기본 추적 리스너를 제거하는 방법을 보여 주며, 이 예제에서는 이 요소를 사용하는 방법을 보여 주며, 이 예제에서는 이 요소를 사용하여 소스에 대한 추적 리스너를 제거하는 방법을 보여 주며, 이 예제에서는 이 요소를 사용하여 소스에 대한 추적 리스너를 제거하는 방법을 보여 주며, 이 예제에서는 이 요소를 사용하여 소스에 콘솔 추적 리스너를 추가하는  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="mySource" switchName="sourceSwitch"
        switchType="System.Diagnostics.SourceSwitch">  
        <listeners>  
          <add name="console"
            type="System.Diagnostics.ConsoleTraceListener">  
            <filter type="System.Diagnostics.EventTypeFilter"
              initializeData="Error"/>  
          </add>  
          <remove name="Default"/>  
        </listeners>  
      </source>  
    </sources>  
    <switches>  
      <add name="sourceSwitch" value="Warning"/>  
    </switches>  
  </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Diagnostics.TraceListener>
- [추적 및 디버그 설정 스키마](index.md)
- [추적 수신기](../../../debug-trace-profile/trace-listeners.md)
