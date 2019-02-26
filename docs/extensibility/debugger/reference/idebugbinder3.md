---
title: IDebugBinder3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3
helpviewer_keywords:
- IDebugBinder3 interface
ms.assetid: 92353a74-dc74-4f93-8762-61d6b220478c
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 733ede7b7bad73419fc160f4c15b660b50b26b7e
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56707550"
---
# <a name="idebugbinder3"></a>IDebugBinder3
> [!IMPORTANT]
>  Visual Studio 2015 での式エバリュエーターの実装には、この方法は非推奨とされます。 CLR 式エバリュエーターの実装方法の詳細についてを参照してください[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)します。

 このインターフェイスは、型、エイリアス、およびカスタム ビジュアライザー サービスにアクセスを提供します。

## <a name="syntax"></a>構文

```
IDebugBinder3 : IDebugBinder
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 デバッグ エンジンでは、エイリアス、カスタム ビジュアライザー サービス、およびオブジェクトの種類の情報へのアクセスをサポートするためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元のノート
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)インターフェイスを使用してこのインターフェイスを取得する[QueryInterface](/cpp/atl/queryinterface)します。

## <a name="methods-in-vtable-order"></a>Vtable 順序メソッド
 によって提供されるメソッドに加え、 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)インターフェイスでは、このインターフェイスは、次を実装します。

|メソッド|説明|
|------------|-----------------|
|[GetMemoryObject](../../../extensibility/debugger/reference/idebugbinder3-getmemoryobject.md)|このオブジェクトがバインドされているメモリを表すメモリ オブジェクトを取得します。|
|[GetExceptionObjectAndType](../../../extensibility/debugger/reference/idebugbinder3-getexceptionobjectandtype.md)|このオブジェクト (ある場合)、関連付けられた例外を取得します。|
|[FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)|指定した名前、エイリアスを取得します。|
|[GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)|このオブジェクトのすべてのエイリアスの配列を取得します|
|[GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)|このオブジェクトに関連付けられている引数の型の数を取得します。|
|[GetTypeArguments](../../../extensibility/debugger/reference/idebugbinder3-gettypearguments.md)|このオブジェクトに関連付けられている引数の型の一覧を取得します|
|[GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)|ビジュアライザーのサービスへのインターフェイスを取得します。|
|[GetMemoryContext64](../../../extensibility/debugger/reference/idebugbinder3-getmemorycontext64.md)|メモリ コンテキスト オブジェクトの場所または 64 ビットのメモリ アドレスのいずれかに変換します。|

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)