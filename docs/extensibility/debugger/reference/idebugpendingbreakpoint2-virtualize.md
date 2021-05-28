---
description: この保留中のブレークポイントの仮想化状態を切り替えます。
title: IDebugPendingBreakpoint2::Virtualize | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::Virtualize
helpviewer_keywords:
- Virtualize method
- IDebugPendingBreakpoint2::Virtualize method
ms.assetid: 58c8e9a5-4494-47c2-bddb-56f628da6a2d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fa2d3dcab7e5e71140b308dc825417c03e79d356
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084520"
---
# <a name="idebugpendingbreakpoint2virtualize"></a>IDebugPendingBreakpoint2::Virtualize
この保留中のブレークポイントの仮想化状態を切り替えます。 保留中のブレークポイントが仮想化されると、新しいコードがプログラムに読み込まれるたびに、デバッグ エンジンによってブレークポイントのバインドが試みられます。

## <a name="syntax"></a>構文

```cpp
HRESULT Virtualize(
    BOOL fVirtualize
);
```

```cpp
int Virtualize(
    int fVirtualize
);
```

## <a name="parameters"></a>パラメーター
`fVirtualize`\
[入力] 保留中のブレークポイントを仮想化する場合は 0 以外 (`TRUE`) に設定し、仮想化を無効にする場合は 0 (`FALSE`) に設定します。

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 ブレークポイントが削除されている場合は、`E_BP_DELETED` を返します。

## <a name="remarks"></a>解説
仮想化されたブレークポイントは、コードが読み込まれるたびにバインドされます。

## <a name="example"></a>例
次の例は、[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) インターフェイスを公開するシンプルな `CPendingBreakpoint` オブジェクトにこのメソッドを実装する方法を示しています。

```cpp
HRESULT CPendingBreakpoint::Virtualize(BOOL fVirtualize)
{
    HRESULT hr;

    // Verify that the pending breakpoint has not been deleted. If deleted,
    // then return hr = E_BP_DELETED.
    if (m_state.state != PBPS_DELETED)
    {
        if (fVirtualize)
        {
            // Set the PBPSF_VIRTUALIZED flag in the PENDING_BP_STATE_FLAGS
            // structure.
            SetFlag(m_state.flags, PBPSF_VIRTUALIZED);
        }
        else
        {
            // Clear the PBPSF_VIRTUALIZED flag in the PENDING_BP_STATE_FLAGS
            // structure.
            ClearFlag(m_state.flags, PBPSF_VIRTUALIZED);
        }
        hr = S_OK;
    }
    else
    {
        hr = E_BP_DELETED;
    }

    return hr;
}
```

## <a name="see-also"></a>関連項目
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
