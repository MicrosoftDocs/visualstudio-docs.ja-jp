---
description: このインターフェイスは、ポインターの型を表します。
title: IDebugPointerField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerField
helpviewer_keywords:
- IDebugPointerField interface
ms.assetid: d51bd5b2-f18e-4e27-b4fb-e6f652fbf635
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 568e442f5294b3aaa4cd8c99d7bbd1f769581ca6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087744"
---
# <a name="idebugpointerfield"></a>IDebugPointerField
このインターフェイスは、ポインターの型を表します。

## <a name="syntax"></a>構文

```
IDebugPointerField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボル プロバイダーでは、ポインターを表すためにこのインターフェイスが実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) が `FIELD_TYPE_POINTER` を返す場合に、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスからこのインターフェイスを取得するには、[QueryInterface](/cpp/atl/queryinterface) を使用します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスでは、`IDebugField` および `IDebugContainerField` インターフェイスのメソッドに加えて、次のメソッドが実装されます。

|メソッド|説明|
|------------|-----------------|
|[GetDereferencedField](../../../extensibility/debugger/reference/idebugpointerfield-getdereferencedfield.md)|ポインターのターゲットが記述された [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) を返します。|

## <a name="remarks"></a>解説
 C/C++ では、配列表記で使用される場合、ポインターをコンテナーにすることができます。 たとえば、`char *pString` を指定した場合、`pString` は `char` へのポインターの型になります。 `pString[3]` は、そのコンテナーの 4 番目の要素を参照する `char` へのポインターであるコンテナーの型になります。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
