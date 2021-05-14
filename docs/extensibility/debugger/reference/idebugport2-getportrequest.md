---
description: 以前にポートの作成に使用されたポートに関する記述を取得します (該当するものがある場合)。
title: IDebugPort2::GetPortRequest | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPort2::GetPortRequest
helpviewer_keywords:
- IDebugPort2::GetPortRequest
ms.assetid: 14abf847-0675-4fa8-872e-971e00c84224
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 77224f98d953b61529ffed083e7be4cee0ed662f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087484"
---
# <a name="idebugport2getportrequest"></a>IDebugPort2::GetPortRequest
以前にポートの作成に使用されたポートに関する記述を取得します (該当するものがある場合)。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPortRequest( 
   IDebugPortRequest2** ppRequest
);
```

```csharp
int GetPortRequest( 
   out IDebugPortRequest2 ppRequest
);
```

## <a name="parameters"></a>パラメーター
`ppRequest`\
[out] ポートの作成に使用された要求を表す [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。  ポートが [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) ポート要求を使用して作成されていない場合は、`E_PORT_NO_REQUEST` を返します。

## <a name="see-also"></a>関連項目
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
