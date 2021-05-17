---
description: このインターフェイスは、スタック フレーム プロパティ、プログラム ドキュメント プロパティ、またはその他のプロパティを表します。
title: IDebugProperty2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2
helpviewer_keywords:
- IDebugProperty2 interface
ms.assetid: a7d5c70f-a1a5-4120-9f70-184e01c25bff
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c5d20f0bd3727860f32e111baad2d2513590e880
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064801"
---
# <a name="idebugproperty2"></a>IDebugProperty2
このインターフェイスは、スタック フレーム プロパティ、プログラム ドキュメント プロパティ、またはその他のプロパティを表します。 プロパティは通常、式評価の結果です。

> [!NOTE]
> このような "プロパティ" の使用をクラスのメンバー変数と混同しないでください。ただし、`IDebugProperty2` ではこのようなエンティティを表すことができます。

## <a name="syntax"></a>構文

```
IDebugProperty2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE では、特定の種類の値を表すために、このインターフェイスを実装します。 たとえば、値には、式の評価の結果としての数値、メモリの表示に使用されるメモリ コンテキスト、レジスタとその値の一覧などがあります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) または [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) を呼び出して、評価の結果を表すこのインターフェイスを取得します。 `IDebugExpression2::EvaluateAsync` は、後に [GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md) を呼び出してプロパティを取得する [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) インターフェイスを SDM に送信してこのインターフェイスを返します。

- [GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md) は、関連付けられているスクリプト ドキュメントを提供するために、このインターフェイスを返します。

- [GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md) 値は、関数の戻り値を表すために、このインターフェイスを返します。

- [GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md) は、名前やメモリ コンテキストなど、プログラムのさまざまなプロパティを表すために、このインターフェイスを返します。

- [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) は、ローカル変数など、スタック フレームのさまざまなプロパティを表すために、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugProperty2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)|プロパティを記述する [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体を満たします。|
|[SetValueAsString](../../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)|文字列からプロパティの値を設定します。|
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugproperty2-setvalueasreference.md)|指定された参照の値からプロパティの値を設定します。|
|[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)|プロパティの子を列挙します。|
|[GetParent](../../../extensibility/debugger/reference/idebugproperty2-getparent.md)|プロパティの親を返します。|
|[GetDerivedMostProperty](../../../extensibility/debugger/reference/idebugproperty2-getderivedmostproperty.md)|プロパティの最派生プロパティを記述するプロパティを返します。|
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)|プロパティの値を構成するメモリのバイト数を返します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)|プロパティ値のメモリ コンテキストを返します。|
|[GetSize](../../../extensibility/debugger/reference/idebugproperty2-getsize.md)|プロパティの値のサイズをバイト単位で返します。|
|[GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)|このプロパティの値への参照を返します。|
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)|プロパティの拡張情報を返します。|

## <a name="remarks"></a>解説
 `IDebugProperty2` インターフェイスによって表されるプロパティは、名前、型、アドレスを持つ値であると考えることができます。 より一般的な言い方をすると、`IDebugProperty2` は、親と子のノードがある階層構造を持つ要素であれば何でも表すことができます。

 プロパティは通常は一時的なものであり、たとえば、現在のスタック フレームと同じ期間だけ存続します。 一方、[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) インターフェイスによって表される参照は、値がメモリにとどまる限りは存続します。

 IDE で `IDebugProperty2` インターフェイスを使用して、ユーザーが実行時にプロパティを参照および変更できるようにすることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
