---
title: IDebugFunctionObject2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2 interface
ms.assetid: 56b2fdff-146d-4138-a34c-59a9c65a3ddd
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 972cc9af0453668e4d5393a00bb80f34e2594273
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388441"
---
# <a name="idebugfunctionobject2"></a>IDebugFunctionObject2
> [!IMPORTANT]
> Visual Studio 2015 での式エバリュエーターの実装には、この方法は非推奨とされます。 CLR 式エバリュエーターの実装方法の詳細についてを参照してください[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)します。

 関数を表し、強化、 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)インターフェイス。

## <a name="syntax"></a>構文

```
IDebugFunctionObject2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 式エバリュエーター (EE) は、関数を表すためには、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元のノート
 このインターフェイスのメソッドを遅延の**IDebugFunctionObject**次のようにします。

- **IDebugEvaluate**メソッドはフラグを受け取ります。

- **CreateObject**フラグとタイムアウトを受け取ります。

- **CreateStringObjectWithLength**メソッドは、長さを受け取ります。

## <a name="methods"></a>メソッド
 このインターフェイスは、次のメソッドを実装します。

|メソッド|説明|
|------------|-----------------|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject2-createobject.md)|評価のフラグ設定、およびタイムアウト値を指定されたコンス トラクターを使用するオブジェクトを作成します。|
|[CreateStringObjectWithLength](../../../extensibility/debugger/reference/idebugfunctionobject2-createstringobjectwithlength.md)|指定した長さの文字列オブジェクトを作成します。|
|[Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject2-evaluate.md)|関数の呼び出しをオブジェクトとして結果の値を返します。|

## <a name="requirements"></a>必要条件
 ヘッダー:Ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll