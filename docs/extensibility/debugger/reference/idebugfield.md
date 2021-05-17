---
description: このインターフェイスは、フィールド、つまりシンボルまたは型の説明を表します。
title: IDebugField | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField
helpviewer_keywords:
- IDebugField interface
ms.assetid: adecdd1c-b1b9-4027-92da-74cbe910636f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c519ccfe70ba5685dec8230bf3e4fcb0eb768921
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073678"
---
# <a name="idebugfield"></a>IDebugField
このインターフェイスは、フィールド、つまりシンボルまたは型の説明を表します。

## <a name="syntax"></a>構文

```
IDebugField : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボル プロバイダーでは、このインターフェイスをすべてのフィールドの基本クラスとして実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスはすべてのフィールドの基本クラスです。 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) の戻り値に基づいて、このインターフェイスでは [QueryInterface](/cpp/atl/queryinterface) を使用してより特殊なインターフェイスを返す場合があります。 また、多くのインターフェイスでは、さまざまなメソッドから `IDebugField` オブジェクトを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugField` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)|シンボルまたは型に関する表示可能な情報を取得します。|
|[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)|フィールドの種類を取得します。|
|[GetType](../../../extensibility/debugger/reference/idebugfield-gettype.md)|フィールドの型を取得します。|
|[GetContainer](../../../extensibility/debugger/reference/idebugfield-getcontainer.md)|フィールドのコンテナーを取得します。|
|[GetAddress](../../../extensibility/debugger/reference/idebugfield-getaddress.md)|フィールドのアドレスを取得します。|
|[GetSize](../../../extensibility/debugger/reference/idebugfield-getsize.md)|フィールドのサイズ (バイト単位) を取得します。|
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugfield-getextendedinfo.md)|フィールドに関する拡張情報を取得します。|
|[Equal](../../../extensibility/debugger/reference/idebugfield-equal.md)|2 つのフィールドを比較します。|
|[GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)|シンボルまたは型に関して、型に依存しない情報を取得します。|

## <a name="remarks"></a>解説
 型は C 言語の `typedef` に相当します。

 次の C++ 言語の例で、`weather` はクラス型であり、`sunny` と `stormy` はシンボルです。

```cpp
class weather;
weather sunny;
weather stormy;
```

 フィールドがシンボルまたは型を表すかどうかを判断するには、[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) を呼び出し、[FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) の結果を調べます。 `FIELD_KIND_TYPE` ビットが設定されている場合、フィールドは型であり、`FIELD_KIND_SYMBOL` ビットが設定されている場合はシンボルです。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
