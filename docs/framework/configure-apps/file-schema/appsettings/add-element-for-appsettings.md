---
title: <add>에 대한 <appSettings> 요소
ms.date: 05/01/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/appSettings/add
helpviewer_keywords:
- add Element
- <add> Element
ms.assetid: 8734efdc-00f6-4a65-bba6-084c5bc65246
ms.openlocfilehash: 5c7de79ec626966e71d461dd3865b294a8979db2
ms.sourcegitcommit: 9c54866bcbdc49dbb981dd55be9bbd0443837aa2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2020
ms.locfileid: "77214801"
---
# <a name="add-element-for-appsettings"></a>\<appSettings에 대 한 > 요소를 추가 \<>

사용자 지정 응용 프로그램 설정을 추가 합니다.

[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<appSettings>** ](appsettings-element-for-configuration.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<추가**

## <a name="syntax"></a>구문

```xml
<appSettings>
  <add key="Key of custom setting" value="Value of custom setting" />
</appSettings>
```

## <a name="attributes"></a>특성

|           | Description |
| --------- | ----------- |
| **key**   | 필수 특성입니다.<br><br>추가할 키의 이름을 지정 합니다. |
| **value** | 필수 특성입니다.<br><br>추가할 키의 값을 지정 합니다. |

## <a name="parent-element"></a>부모 요소

|     | Description |
| --- | ----------- |
| [ **\<appSettings>** ](appsettings-element-for-configuration.md) | 파일 경로, XML Web services URL 또는 애플리케이션의 기타 사용자 지정 구성 정보와 같은 사용자 지정 애플리케이션 설정이 포함되어 있습니다. |

## <a name="child-elements"></a>자식 요소

None

## <a name="example"></a>예제

다음 예제에서는 응용 프로그램의 이름에 대 한 사용자 지정 구성 설정을 추가 하는 방법을 보여 줍니다.

```xml
<appSettings>
  <add key="ApplicationName" value="MyApplication" />
</appSettings>
```

다음 예제에서는 `<add>` 요소를 사용 하 여 ASP.NET 응용 프로그램에서 두 가지 호환성 설정을 정의 합니다.

```xml
<appSettings>
  <add key="AppContext.SetSwitch:Switch.System.Globalization.NoAsyncCurrentCulture" value="true" />
  <add key="AppContext.SetSwitch:Switch.System.Uri.DontEnableStrictRFC3986ReservedCharacterSets" value="true" />
</appSettings>
```

## <a name="see-also"></a>참고 항목

- [.NET Framework에 대 한 구성 파일 스키마](../index.md)
