---
title: IDebuggerThreadControl 인터페이스
ms.date: 03/30/2017
api_name:
- IDebuggerThreadControl
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IDebuggerThreadControl
helpviewer_keywords:
- IDebuggerThreadControl interface [.NET Framework hosting]
ms.assetid: 0a270c42-a7d1-45f1-a64d-fa3e84d14532
topic_type:
- apiref
ms.openlocfilehash: 82c6113f4df3334500128df22f7e9ce8d4bf151f
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2020
ms.locfileid: "83805284"
---
# <a name="idebuggerthreadcontrol-interface"></a>IDebuggerThreadControl 인터페이스
디버깅 서비스에서 스레드의 차단 및 차단 해제에 대해 호스트에 알리는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[ThreadIsBlockingForDebugger 메서드](idebuggerthreadcontrol-threadisblockingfordebugger-method.md)|이 콜백을 보내는 스레드가 디버깅 서비스 내에서 차단 됨을 호스트에 알립니다.|  
|[ReleaseAllRuntimeThreads 메서드](idebuggerthreadcontrol-releaseallruntimethreads-method.md)|디버깅 서비스가 차단 된 모든 스레드를 해제 하려고 한다는 사실을 호스트에 알립니다.|  
|[StartBlockingForDebugger 메서드](idebuggerthreadcontrol-startblockingfordebugger-method.md)|디버깅 서비스가 모든 스레드를 차단 하기 시작 했음을 호스트에 알립니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:**[시스템 요구 사항](../../get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** Mscoree.dll  
  
 **라이브러리:** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [호스팅 인터페이스](hosting-interfaces.md)
