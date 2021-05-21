---
description: このイベントを発生された例外に関する詳細な説明を取得します。
title: IDebugExceptionEvent2::GetException | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::GetException
helpviewer_keywords:
- IDebugExceptionEvent2::GetException
ms.assetid: 7c98f41d-322b-4e72-a514-cbd4823eb70d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 72457b1b8931d028f555e7f9354f34b133fa79bb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084780"
---
# <a name="idebugexceptionevent2getexception"></a>IDebugExceptionEvent2::GetException
このイベントを発生された例外に関する詳細な説明を取得します。

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

## <a name="parameters"></a>パラメーター
`pExceptionInfo`\
[in, out] 例外の説明が入力される [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 構造体。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説

 [C++ のみ] 呼び出し元は、[EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 構造体内の文字列を解放するだけでなく、構造体内の [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) オブジェクトも解放する責任があります。

## <a name="see-also"></a>関連項目
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
