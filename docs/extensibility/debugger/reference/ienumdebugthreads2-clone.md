---
description: 現在のスレッド列挙体のコピーを別のオブジェクトとして返します。
title: IEnumDebugThreads2::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2::Clone
helpviewer_keywords:
- IEnumDebugThreads2::Clone
ms.assetid: d774322c-e72d-4df3-b317-928da39dadc5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 82b0895cfabc63fc61c85fd626f8811796532e19
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082726"
---
# <a name="ienumdebugthreads2clone"></a>IEnumDebugThreads2::Clone
現在の列挙のコピーを別のオブジェクトとして返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Clone(
   IEnumDebugThreads2** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugThreads2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
[out] この列挙のコピーを別のオブジェクトとして返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 列挙のコピーは、このメソッドが呼び出された時点での元の列挙と同じ状態になります。 しかし、コピーと元のものの状態は別々であり、個別に変更できます。

## <a name="see-also"></a>関連項目
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)
