---
title: IDebugExceptionEvent2::GetException |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::GetException
helpviewer_keywords:
- IDebugExceptionEvent2::GetException
ms.assetid: 7c98f41d-322b-4e72-a514-cbd4823eb70d
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 79385348aa9290f26a34b99dbd2d6f68cb92dc8a
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56680283"
---
# <a name="idebugexceptionevent2getexception"></a>IDebugExceptionEvent2::GetException
このイベントを発生させた例外の詳細な説明を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetException( 
   EXCEPTION_INFO* pExceptionInfo
);
```

```csharp
int GetException( 
   EXCEPTION_INFO[] pExceptionInfo
);
```

#### <a name="parameters"></a>パラメーター
 `pExceptionInfo`

 [入力、出力][EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)構造を例外の説明が入力されます。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks

 [C++ のみ]呼び出し元が内の任意の文字列を解放する、 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)の解放と構造体、 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)構造内のオブジェクト。

## <a name="see-also"></a>関連項目
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)