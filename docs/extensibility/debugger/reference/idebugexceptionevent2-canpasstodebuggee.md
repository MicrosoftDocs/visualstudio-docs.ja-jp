---
description: 実行の再開時にデバッグ対象のプログラムにこの例外を渡すオプションがデバッグ エンジン (DE) によってサポートされているかどうかを調べます。
title: IDebugExceptionEvent2::CanPassToDebuggee | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::CanPassToDebuggee
helpviewer_keywords:
- IDebugExceptionEvent2::CanPassToDebuggee
ms.assetid: ae4bbe0a-fbe1-49be-a310-ea64279a434b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7fbc5cd55516f018a0a0877a114169a436b97fe1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084845"
---
# <a name="idebugexceptionevent2canpasstodebuggee"></a>IDebugExceptionEvent2::CanPassToDebuggee
実行の再開時にデバッグ対象のプログラムにこの例外を渡すオプションがデバッグ エンジン (DE) によってサポートされているかどうかを調べます。

## <a name="syntax"></a>構文

```cpp
HRESULT CanPassToDebuggee(
   void
);
```

```csharp
int CanPassToDebuggee();
```

## <a name="return-value"></a>戻り値
 `S_OK` (プログラムに例外を渡すことができます) または `S_FALSE` (例外を渡すことはできません) のいずれかを返します。

## <a name="remarks"></a>解説
 DE には、デバッグ対象に渡すための既定のアクションが必要です。 IDE では、[IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) イベントを受け取り、`CanPassToDebuggee` メソッドを呼び出すことなく [Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md) メソッドを呼び出す可能性があります。 そのため、DE には、例外を渡す場合、または渡さない場合の既定のケースが必要です。

## <a name="see-also"></a>関連項目
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [続行](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
