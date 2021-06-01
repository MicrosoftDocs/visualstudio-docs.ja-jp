---
description: プロセスで実行されているすべてのスレッドのリストを取得します。
title: IDebugProcess2::EnumThreads | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::EnumThreads
helpviewer_keywords:
- IDebugProcess2::EnumThreads
ms.assetid: 05677385-7a7f-4545-8438-af00dde85db0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6c502504b3a31f3e4689db34f907f9596b214877
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071611"
---
# <a name="idebugprocess2enumthreads"></a>IDebugProcess2::EnumThreads
プロセスで実行されているすべてのスレッドのリストを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumThreads(
   IEnumDebugThreads2** ppEnum
);
```

```csharp
int EnumThreads(
   out IEnumDebugThreads2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
[出力] プロセス内のすべてのプログラムのすべてのスレッドのリストを含む [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 このメソッドでは、各プログラムで実行されているスレッドが列挙され、それらがスレッドのプロセス ビューに結合されます。 1 つのスレッドが複数のプログラムで実行される場合があります。そのようなスレッドは、このメソッドによって 1 回だけ列挙されます。

 このメソッドでは、プロセス内の重複しないスレッドのリストが表示されます。 そうではなく、特定のプログラムで実行されているスレッドを列挙するには、[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) メソッドを使用します。

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
