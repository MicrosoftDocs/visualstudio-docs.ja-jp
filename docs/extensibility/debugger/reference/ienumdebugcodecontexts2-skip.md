---
title: IEnumDebugCodeContexts2::Skip |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2::Skip
helpviewer_keywords:
- IEnumDebugCodeContexts2::Skip
ms.assetid: 3451a3eb-bf5b-4ec5-acc9-aa5a24363801
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a7e06fdd48b131073862742d26de6abfeea20844
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56716117"
---
# <a name="ienumdebugcodecontexts2skip"></a>IEnumDebugCodeContexts2::Skip
指定した要素数をスキップします。

## <a name="syntax"></a>構文

```cpp
HRESULT Skip(
   ULONG celt
);
```

```csharp
int Skip(
   uint celt
);
```

#### <a name="parameters"></a>パラメーター
 `celt`

 [in]スキップする要素の数。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 返します`S_FALSE`場合`celt`が残りの要素の数より大きい。 それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>Remarks
 場合`celt`数より大きい値を指定します。 残りの要素の列挙体が最後に設定し、`S_FALSE`が返されます。

## <a name="see-also"></a>関連項目
- [IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)