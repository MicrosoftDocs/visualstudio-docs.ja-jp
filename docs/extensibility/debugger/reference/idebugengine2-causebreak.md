---
description: は、このデバッグエンジン (DE) によってデバッグされているすべてのプログラムが、次にそのスレッドの実行を試行したときに実行を停止することを要求します。
title: 'IDebugEngine2:: CauseBreak |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::CauseBreak
helpviewer_keywords:
- IDebugEngine2::CauseBreak
ms.assetid: 17fe4698-b04e-4798-8412-80e0da60c387
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 74a320cbe9f2414de754b5844aa645bffb857568
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105093900"
---
# <a name="idebugengine2causebreak"></a>IDebugEngine2::CauseBreak
は、このデバッグエンジン (DE) によってデバッグされているすべてのプログラムが、次にそのスレッドの実行を試行したときに実行を停止することを要求します。

## <a name="syntax"></a>構文

```cpp
HRESULT CauseBreak( 
   void 
);
```

```csharp
int CauseBreak();
```

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドは非同期です。 [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) イベントは、このメソッドが呼び出された後にプログラムが次に実行を試行したときに送信されます。

## <a name="see-also"></a>こちらもご覧ください
- [CauseBreak](../../../extensibility/debugger/reference/idebugprogram2-causebreak.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
