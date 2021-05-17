---
description: 実行の再開時にデバッグされるプログラムに例外を渡すか、例外を破棄する必要があるかを指定します。
title: IDebugExceptionEvent2::PassToDebuggee | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::PassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::PassToDebuggee
ms.assetid: a20d0f0b-2ca0-4437-bd22-9213c81d2738
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f81af5686cfc2b99dc3bf5d95e2ec283933297e2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084767"
---
# <a name="idebugexceptionevent2passtodebuggee"></a>IDebugExceptionEvent2::PassToDebuggee
実行の再開時にデバッグされるプログラムに例外を渡すか、例外を破棄する必要があるかを指定します。

## <a name="syntax"></a>構文

```cpp
HRESULT PassToDebuggee(
   BOOL fPass
);
```

```csharp
int PassToDebuggee(
   int fPass
);
```

## <a name="parameters"></a>パラメーター
`fPass`\
[入力] 実行の再開時にデバッグされているプログラムに例外を渡す場合はゼロ以外 (`TRUE`)、または例外を破棄する必要がある場合はゼロ (`FALSE`)。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドを呼び出しても、デバッグされているプログラムでコードが実際に実行されることはありません。 この呼び出しでは、次のコード実行の状態が設定されるだけです。 たとえば、[CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) メソッドを呼び出すと、`S_OK` が返される場合があります ([EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md).`dwState` フィールド に `EXCEPTION_STOP_SECOND_CHANCE` が設定された状態で)。

 IDE では、[IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) イベントを受け取り、[Continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md) メソッドを呼び出すことができます。 デバッグ エンジン (DE) には、`PassToDebuggee` メソッドが呼び出されない場合に、そのケースを処理するための既定の動作が必要です。

## <a name="see-also"></a>関連項目
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)
- [続行](../../../extensibility/debugger/reference/idebugprogram2-continue.md)
