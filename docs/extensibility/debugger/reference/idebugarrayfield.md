---
description: このインターフェイスでは、配列のシンボルまたは型を説明します。
title: IDebugArrayField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField
helpviewer_keywords:
- IDebugArrayField interface
ms.assetid: 9667b0a5-4295-46cc-9388-b75c1350be15
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 073438a99531b278a148b6eb19ff6e5af88004e9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058938"
---
# <a name="idebugarrayfield"></a>IDebugArrayField
このインターフェイスでは、配列のシンボルまたは型を説明します。

## <a name="syntax"></a>構文

```
IDebugArrayField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、シンボル プロバイダーにより、[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスが実装されるオブジェクトと同じオブジェクトに実装されます。 このインターフェイスは、配列オブジェクトを表す特殊化です。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) によってフラグ `FIELD_TYPE_ARRAY` が返される場合は、[QueryInterface](/cpp/atl/queryinterface) を使用して、[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスからこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) および [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスのメソッドに加えて、次を実装します。

|メソッド|説明|
|------------|-----------------|
|[GetNumberOfElements](../../../extensibility/debugger/reference/idebugarrayfield-getnumberofelements.md)|配列内の要素の数を取得します。|
|[GetElementType](../../../extensibility/debugger/reference/idebugarrayfield-getelementtype.md)|配列に含まれる要素の型を取得します。|
|[GetRank](../../../extensibility/debugger/reference/idebugarrayfield-getrank.md)|配列のランクを取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
