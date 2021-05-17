---
description: 変数の数値の別名を表します。
title: IDebugAlias | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias
helpviewer_keywords:
- IDebugAlias interface
ms.assetid: 3cc4c9a4-7805-4239-b00e-eb4a024f3c55
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d5eb9f1d4bc493779d9b42a984c8fc1577e2fe66
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059146"
---
# <a name="idebugalias"></a>IDebugAlias
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 変数の数値の別名を表します。 別名とは、単に変数の異なる名前です。

## <a name="syntax"></a>構文

```
IDebugAlias : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーター (EE) により、変数の数値のエイリアスをサポートするために、このインターフェイスが実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
- [CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md) により、特定のオブジェクトの別名が作成されます。 別名を検索するには、[FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md) または [GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md) を使用します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugAlias` インターフェイスでは、次のメソッドが定義されています。

|メソッド|説明|
|------------|-----------------|
|[GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)|この別名が参照するオブジェクトを取得します。|
|[GetName](../../../extensibility/debugger/reference/idebugalias-getname.md)|別名の名前を取得します。|
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugalias-geticordebugvalue.md)|このオブジェクトに関するマネージド コード情報へのアクセスを提供する `ICorDebugValue` インターフェイスを取得します (マネージド コードのみ)。|
|[Dispose](../../../extensibility/debugger/reference/idebugalias-dispose.md)|この別名は使用されなくなったものとしてマークします。|

## <a name="remarks"></a>解説
 別名は、文字列形式の 10 進数の後に # 文字が続いたものです (たとえば、1001#)。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)
- [FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)
- [GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)
