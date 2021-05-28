---
description: 指定したバインド ブレークポイントの作成元である、保留中のブレークポイントを取得します。
title: IDebugBoundBreakpoint2::GetPendingBreakpoint | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::GetPendingBreakpoint
helpviewer_keywords:
- IDebugBoundBreakpoint2::GetPendingBreakpoint method
- GetPendingBreakpoint method
ms.assetid: 22f94f81-f8d9-46de-96e9-fae6f3c24903
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 15b053515268c16bfacdeee08e40390950542e38
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095837"
---
# <a name="idebugboundbreakpoint2getpendingbreakpoint"></a>IDebugBoundBreakpoint2::GetPendingBreakpoint
指定したバインド ブレークポイントの作成元である、保留中のブレークポイントを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetPendingBreakpoint( 
    IDebugPendingBreakpoint2** ppPendingBreakpoint
);
```

```csharp
int GetPendingBreakpoint( 
    out IDebugPendingBreakpoint2 ppPendingBreakpoint
);
```

## <a name="parameters"></a>パラメーター
`ppPendingBreakpoint`\
[出力] このバインド ブレークポイントの作成に使用された保留中のブレークポイントを表す [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
保留中のブレークポイントは、1 つまたは複数のプログラムに適用できるコードにブレークポイントをバインドするために必要なすべての情報のコレクションと考えることができます。

## <a name="example"></a>例
次の例は、[IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md) インターフェイスを公開するシンプルな `CBoundBreakpoint` オブジェクトにこのメソッドを実装する方法を示しています。

```
HRESULT CBoundBreakpoint::GetPendingBreakpoint(
    IDebugPendingBreakpoint2** ppPendingBreakpoint)
{
    HRESULT hr;

    // Check for valid IDebugPendingBreakpoint2 interface pointer.
    if (ppPendingBreakpoint)
    {
        // Be sure that the bound breakpoint has not been deleted. If
        // deleted, then return hr = E_BP_DELETED.
        if (m_state != BPS_DELETED)
        {
            // Query for the IDebugPendingBreakpoint2 interface.
            hr = m_pPendingBP->QueryInterface(IID_IDebugPendingBreakpoint2,
                                              (void**)ppPendingBreakpoint);
        }
        else
        {
            hr = E_BP_DELETED;
        }
    }
    else
    {
        hr = E_INVALIDARG;
    }

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
