---
title: FunctionLeave 함수
ms.date: 03/30/2017
api_name:
- FunctionLeave
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionLeave
helpviewer_keywords:
- FunctionLeave function [.NET Framework profiling]
ms.assetid: 18e89f45-e068-426a-be16-9f53a4346860
topic_type:
- apiref
ms.openlocfilehash: a9ab8c81c995bbec41db217c904e03dd70351aee
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76866886"
---
# <a name="functionleave-function"></a>FunctionLeave 함수
함수가 호출자에 게 반환 될 것 이라고 프로파일러에 알립니다.  
  
> [!NOTE]
> `FunctionLeave` 함수는 2.0 .NET Framework에서 더 이상 사용 되지 않습니다. 계속 작동 하지만 성능이 저하 됩니다. 대신 [FunctionLeave2](functionleave2-function.md) 함수를 사용 해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
void __stdcall FunctionLeave (  
    [in] FunctionID funcID  
);  
```  
  
## <a name="parameters"></a>매개 변수

- `funcID`

  \[in] 반환 되는 함수의 식별자입니다.

## <a name="remarks"></a>주의  
 `FunctionLeave` 함수는 콜백입니다. 구현 해야 합니다. 구현은 `__declspec`(`naked`) 저장소 클래스 특성을 사용 해야 합니다.  
  
 실행 엔진은이 함수를 호출 하기 전에 레지스터를 저장 하지 않습니다.  
  
- 항목에서 FPU (부동 소수점 단위)의 항목을 포함 하 여 사용 하는 모든 레지스터를 저장 해야 합니다.  
  
- 종료 시 호출자에 의해 푸시되는 모든 매개 변수를 팝 하 여 스택을 복원 해야 합니다.  
  
 `FunctionLeave` 구현은 가비지 수집을 지연 시킬 수 있으므로 차단 하면 안 됩니다. 스택이 가비지 컬렉션에 대 한 상태에 있지 않을 수 있기 때문에 구현에서 가비지 수집을 시도 하면 안 됩니다. 가비지 수집을 시도 하면 `FunctionLeave` 반환 될 때까지 런타임이 차단 됩니다.  
  
 또한 `FunctionLeave` 함수는 관리 코드를 호출 하거나 관리 되는 메모리 할당을 발생 시 키 지 않아야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하세요.  
  
 **헤더:** Corprof.idl  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** 1.1, 1.0  
  
## <a name="see-also"></a>참조

- [FunctionEnter2 함수](functionenter2-function.md)
- [FunctionLeave2 함수](functionleave2-function.md)
- [FunctionTailcall2 함수](functiontailcall2-function.md)
- [SetEnterLeaveFunctionHooks2 메서드](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)
- [프로파일링 전역 정적 함수](profiling-global-static-functions.md)
