---
description: 式エバリュエーターを停止してクリーンアップします。
title: IDebugExpressionEvaluator2::Terminate | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Terminate
- IDebugExpressionEvaluator2::Terminate
ms.assetid: 38265100-4d80-4902-833a-07bb569f9ba8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cab26c681b621980f1c9220c72bd3107a03c64fb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077318"
---
# <a name="idebugexpressionevaluator2terminate"></a>IDebugExpressionEvaluator2::Terminate
式エバリュエーターを停止してクリーンアップします。

## <a name="syntax"></a>構文

```cpp
HRESULT Terminate (
    void
);
```

```csharp
int Terminate ();
```

## <a name="return-value"></a>戻り値
成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
クリーンアップ中の式エバリュエーターに通知します。

## <a name="example"></a>例
次の例は、[IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md) インターフェイスを公開する **ExpressionEvaluatorPackage** オブジェクトにこのメソッドを実装する方法を示しています。

```cpp
STDMETHODIMP ExpressionEvaluatorPackage::Terminate(void)
{
    // scan the namespaces contained and delete
    EEExtensionMethodCache **ppChild = NULL;
    m_HashExtensionMethodCache.ResetHashIterator();
    while (ppChild = m_HashExtensionMethodCache.IterateHash())
    {
        delete *ppChild;
    }
    return VBEEImplicitVariables::Terminate();
}
```

## <a name="see-also"></a>関連項目
- [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)
