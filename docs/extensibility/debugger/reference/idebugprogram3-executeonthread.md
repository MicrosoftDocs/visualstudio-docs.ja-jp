---
description: デバッガー プログラムを実行します。
title: IDebugProgram3::ExecuteOnThread | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3::ExecuteOnThread
ms.assetid: 2f5211e3-7a3f-47bf-9595-dfc8b4895d0d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a86bca6aa26a6bb364e9d704e79f57cef8f55395
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084390"
---
# <a name="idebugprogram3executeonthread"></a>IDebugProgram3::ExecuteOnThread
デバッガー プログラムを実行します。 プログラムの実行時にユーザーが表示しているスレッドのデバッガー情報を提供するために、スレッドが返されます。

## <a name="syntax"></a>構文

```cpp
HRESULT ExecuteOnThread(
   [in] IDebugThread2* pThread)
```

```csharp
int ExecuteOnThread(
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>パラメーター
`pThread`\
[入力] [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 デバッガーが停止した後に実行を再開するには、次の 3 つの方法があります。

- Execute: 前のステップをキャンセルし、次のブレークポイントまで実行します。

- Step: 以前のステップをキャンセルし、新しいステップが完了するまで実行します。

- Continue: もう一度実行し、以前のステップをアクティブのままにします。

  `ExecuteOnThread` に渡されるスレッドは、キャンセルするステップを決定するときに役立ちます。 スレッドがわからない場合は、Execute を実行すると、すべてのステップがキャンセルされます。 スレッドがわかっている場合は、アクティブなスレッドのステップをキャンセルする必要があるだけです。

## <a name="see-also"></a>関連項目
- [実行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)
- [IDebugProgram3](../../../extensibility/debugger/reference/idebugprogram3.md)
