---
description: このインターフェイスはポインター オブジェクトを表します。
title: IDebugPointerObject | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject
helpviewer_keywords:
- IDebugPointerObject interface
ms.assetid: 257fa167-b46e-4ffb-9a12-272efbf26702
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: af6b8f6022a9363eb5391d6f0519603fa48668c2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087601"
---
# <a name="idebugpointerobject"></a>IDebugPointerObject
> [!IMPORTANT]
> Visual Studio 2015 では、この方法による式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)および[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 このインターフェイスはポインター オブジェクトを表します。

## <a name="syntax"></a>構文

```
IDebugPointerObject : IDebugObject
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターでは、ポインター オブジェクトを表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスでは、`IDebugObject` がポインターを表す場合、[QueryInterface](/cpp/atl/queryinterface) を使用してこのインターフェイスを取得できます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugPointerObject` インターフェイスでは、[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) から継承されたメソッドに加えて以下のメソッドが公開されます。

|メソッド|説明|
|------------|-----------------|
|[Dereference](../../../extensibility/debugger/reference/idebugpointerobject-dereference.md)|インターフェイスが指すオブジェクトを取得します。|
|[GetBytes](../../../extensibility/debugger/reference/idebugpointerobject-getbytes.md)|インターフェイスが連続する一連のバイトとして指す値を取得します。|
|[SetBytes](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)|連続する一連のバイトからインターフェイスが指す値を設定します。|

## <a name="remarks"></a>解説
 式エバリュエーターではこのインターフェイスを使用して、ポインターを解析ツリーで表現します。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
