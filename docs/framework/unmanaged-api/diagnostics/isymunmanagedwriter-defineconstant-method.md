---
title: ISymUnmanagedWriter::DefineConstant 메서드
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.DefineConstant
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::DefineConstant
helpviewer_keywords:
- DefineConstant method [.NET Framework debugging]
- ISymUnmanagedWriter::DefineConstant method [.NET Framework debugging]
ms.assetid: 9e986986-2223-4d5f-b040-85d716146924
topic_type:
- apiref
ms.openlocfilehash: 200e68abb3f176c267045bf2a5e7e35d18400519
ms.sourcegitcommit: 27db07ffb26f76912feefba7b884313547410db5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83610095"
---
# <a name="isymunmanagedwriterdefineconstant-method"></a>ISymUnmanagedWriter::DefineConstant 메서드
상수 값의 이름을 정의 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT DefineConstant(  
    [in] const WCHAR *name,  
    [in] VARIANT value,  
    [in] ULONG32 cSig,  
    [in, size_is(cSig)] unsigned char signature[]);  
```  
  
## <a name="parameters"></a>매개 변수  
 `name`  
 진행 상수 이름을 정의 하는에 대 한 포인터입니다 `WCHAR` .  
  
 `value`  
 진행 상수의 값입니다.  
  
 `cSig`  
 [in] `signature` 배열의 크기입니다.  
  
 `signature`  
 진행 상수에 대 한 형식 시그니처입니다.  
  
## <a name="return-value"></a>Return Value  
 메서드가 성공 하면이 고, 그렇지 않으면 S_OK입니다. 그렇지 않으면 E_FAIL 또는 일부 다른 오류 코드입니다.  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** CorSym, CorSym  
  
## <a name="see-also"></a>참고 항목

- [ISymUnmanagedWriter 인터페이스](isymunmanagedwriter-interface.md)
- [DefineConstant2 메서드](isymunmanagedwriter2-defineconstant2-method.md)
