---
description: このインターフェイスには、プロパティの取得と設定を可能にする関数が用意されています。
title: IDebugPropertyField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyField
helpviewer_keywords:
- IDebugPropertyField interface
ms.assetid: b50edb2c-fb8d-4def-993d-17d23d2027c1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 28fbdfc16733b5cce0d1442c98c624f694adbe1d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083779"
---
# <a name="idebugpropertyfield"></a>IDebugPropertyField
このインターフェイスには、プロパティの取得と設定を可能にする関数が用意されています。

## <a name="syntax"></a>構文

```
IDebugPropertyField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボル プロバイダーは、[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) を実装するのと同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、クラスのプロパティの概念をサポートする特殊化です。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) メソッドによって `FIELD_KIND_PROP` が返される場合は、[QueryInterface](/cpp/atl/queryinterface) を使用して、[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスからこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスでは、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) および [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスのメソッドに加えて、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)|プロパティを取得するメソッドを取得します。|
|[GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md)|プロパティを設定するメソッドを取得します。|

## <a name="remarks"></a>解説
 プロパティはマネージド コードの概念であり、変数として扱われるメソッドを表します。 プロパティはアンマネージド C++ には存在しません。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
