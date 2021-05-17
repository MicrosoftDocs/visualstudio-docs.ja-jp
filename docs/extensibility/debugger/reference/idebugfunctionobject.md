---
description: このインターフェイスは関数を表します。
title: IDebugFunctionObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject
helpviewer_keywords:
- IDebugFunctionObject interface
ms.assetid: 8d94e97c-a9d1-400c-8a98-a44b5385b33a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0fabd43fe6f7d8ee8e5cddc6cc655088bf4a9abf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063553"
---
# <a name="idebugfunctionobject"></a>IDebugFunctionObject
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 このインターフェイスは関数を表します。

## <a name="syntax"></a>構文

```
IDebugFunctionObject : IDebugObject
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターでは、関数を表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスの特殊化であり、`IDebugObject` インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を使用して取得されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugFunctionObject` インターフェイスでは、[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) から継承されたメソッドに加えて以下のメソッドが公開されます。

|メソッド|説明|
|------------|-----------------|
|[CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)|プリミティブ データ オブジェクトを作成します。|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md)|コンストラクターを使用してオブジェクトを作成します。|
|[CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)|コンストラクターを使用せずにオブジェクトを作成します。|
|[CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)|配列オブジェクトを作成します。|
|[CreateStringObject](../../../extensibility/debugger/reference/idebugfunctionobject-createstringobject.md)|文字列オブジェクトを作成します。|
|[Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)|関数を呼び出し、結果の値をオブジェクトとして返します。|

## <a name="remarks"></a>解説
 このインターフェイスは、式エバリュエーターで関数を解析ツリーに表現できるようにします。 このインターフェイスの `Create` メソッドは、メソッドへの入力パラメーターを表すオブジェクトを作成するために使用されます。 その後、関数の戻り値を表すオブジェクトを返す [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) メソッドを呼び出して関数を実行できます。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
