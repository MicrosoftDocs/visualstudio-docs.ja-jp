---
description: 関数を表し、IDebugFunctionObject インターフェイスを拡張します。
title: IDebugFunctionObject2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2 interface
ms.assetid: 56b2fdff-146d-4138-a34c-59a9c65a3ddd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 012cd3dd0068fe69aae8898a408435340c6b22ee
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072846"
---
# <a name="idebugfunctionobject2"></a>IDebugFunctionObject2
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 関数を表し、[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) インターフェイスを拡張します。

## <a name="syntax"></a>構文

```
IDebugFunctionObject2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーター (EE) では、関数を表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスのメソッドでは、次の方法で **IDebugFunctionObject** のメソッドを遅延させます。

- **IDebugEvaluate** メソッドはフラグを受け取ります。

- **CreateObject** メソッドは、フラグとタイムアウトを受け取ります。

- **CreateStringObjectWithLength** メソッドは長さを取ります。

## <a name="methods"></a>メソッド
 このインターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject2-createobject.md)|評価フラグ設定とタイムアウト値を指定したコンストラクターを使用するオブジェクトを作成します。|
|[CreateStringObjectWithLength](../../../extensibility/debugger/reference/idebugfunctionobject2-createstringobjectwithlength.md)|指定された長さの文字列オブジェクトを作成します。|
|[Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject2-evaluate.md)|関数を呼び出し、結果の値をオブジェクトとして返します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
