---
title: ISymUnmanagedWriter3::OpenMethod2 메서드
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter3.OpenMethod2
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter3::OpenMethod2
helpviewer_keywords:
- ISymUnmanagedWriter3::OpenMethod2 method [.NET Framework debugging]
- OpenMethod2 method [.NET Framework debugging]
ms.assetid: 025e358c-448f-4423-a2f2-57acf437c8a5
topic_type:
- apiref
ms.openlocfilehash: e88a844a7f79f14c717a5966b345588b3b3b9f81
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83609419"
---
# <a name="isymunmanagedwriter3openmethod2-method"></a>ISymUnmanagedWriter3::OpenMethod2 메서드
메서드를 열고 이미지의 실제 섹션 오프셋을 제공 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT OpenMethod2(
    [in] mdMethodDef method,  
    [in] ULONG32 isect,  
    [in] ULONG32 offset);  
```  
  
## <a name="parameters"></a>매개 변수  
 `method`  
 진행 열려는 메서드의 메타 데이터 토큰입니다.  
  
 `isect`  
 진행 이미지의 섹션 오프셋입니다.  
  
 `offset`  
 진행 이미지의 오프셋입니다.  
  
## <a name="return-value"></a>Return Value  
 메서드가 성공 하면이 고, 그렇지 않으면 S_OK입니다. 그렇지 않으면 E_FAIL 또는 일부 다른 오류 코드입니다.  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** CorSym, CorSym  
  
## <a name="see-also"></a>참고 항목

- [ISymUnmanagedWriter3 인터페이스](isymunmanagedwriter3-interface.md)
- [OpenMethod 메서드](isymunmanagedwriter-openmethod-method.md)
