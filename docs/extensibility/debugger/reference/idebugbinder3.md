---
description: このインターフェイスでは、型、エイリアス、カスタム ビジュアライザー サービスへのアクセスが提供されます。
title: IDebugBinder3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3
helpviewer_keywords:
- IDebugBinder3 interface
ms.assetid: 92353a74-dc74-4f93-8762-61d6b220478c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 29d8b642a66a75dd561b0a87cd5fa083e841139c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085157"
---
# <a name="idebugbinder3"></a>IDebugBinder3
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 このインターフェイスでは、型、エイリアス、カスタム ビジュアライザー サービスへのアクセスが提供されます。

## <a name="syntax"></a>構文

```
IDebugBinder3 : IDebugBinder
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジンでは、このインターフェイスを実装して、エイリアス、カスタム ビジュアライザー サービス、およびオブジェクトの型情報へのアクセスをサポートします。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) インターフェイスでは、[QueryInterface](/cpp/atl/queryinterface) を使用してこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスでは、[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) インターフェイスによって提供されるメソッドに加えて、次のものが実装されます。

|メソッド|説明|
|------------|-----------------|
|[GetMemoryObject](../../../extensibility/debugger/reference/idebugbinder3-getmemoryobject.md)|このオブジェクトのバインド先のメモリを表すメモリ オブジェクトを取得します。|
|[GetExceptionObjectAndType](../../../extensibility/debugger/reference/idebugbinder3-getexceptionobjectandtype.md)|このオブジェクトに関連付けられている例外 (存在する場合) を取得します。|
|[FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)|名前を指定してエイリアスを取得します。|
|[GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)|このオブジェクトのすべてのエイリアスの配列を取得します。|
|[GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)|このオブジェクトに関連付けられている引数の型の数を取得します。|
|[GetTypeArguments](../../../extensibility/debugger/reference/idebugbinder3-gettypearguments.md)|このオブジェクトに関連付けられている引数の型のリストを取得します。|
|[GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)|ビジュアライザー サービスへのインターフェイスを取得します。|
|[GetMemoryContext64](../../../extensibility/debugger/reference/idebugbinder3-getmemorycontext64.md)|オブジェクトの場所または 64 ビットのメモリ アドレスをメモリ コンテキストに変換します。|

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
