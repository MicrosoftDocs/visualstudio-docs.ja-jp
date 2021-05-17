---
description: 式エバリュエーター (EE) の拡張バージョンを表します。
title: IDebugExpressionEvaluator2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2 interface
ms.assetid: cebe649f-1c77-4d33-854f-30d4f00eceb4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3689f667508f6453f0e4cd4181d14f42ca7b7541
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077305"
---
# <a name="idebugexpressionevaluator2"></a>IDebugExpressionEvaluator2
> [!IMPORTANT]
> Visual Studio 2015 では、この方法での式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)に関する記事と[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 式エバリュエーター (EE) の拡張バージョンを表します。

## <a name="syntax"></a>構文

```
IDebugExpressionEvaluator2 : IDebugExpressionEvaluator
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、式エバリュエーターによって実装されます。

## <a name="methods"></a>メソッド
 このインターフェイスには、[IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md) インターフェイスのメソッドに加えて、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[GetService](../../../extensibility/debugger/reference/idebugexpressionevaluator2-getservice.md)|一意の識別子を指定して、サービス オブジェクトを取得します。|
|[PreloadModules](../../../extensibility/debugger/reference/idebugexpressionevaluator2-preloadmodules.md)|指定したシンボル プロバイダーによって指定されたモジュールをプリロードします。|
|[SetCallback](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setcallback.md)|デバッガー エンジン (DE) でメトリック設定の読み取りに使用するコールバック インターフェイスを、式エバリュエーター (EE) で指定できるようにします。|
|[SetCorPath](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setcorpath.md)|デバッガーに読み込まれる共通言語ランタイム (CLR) へのパスを設定します。|
|[SetIDebugIDECallback](../../../extensibility/debugger/reference/idebugexpressionevaluator2-setidebugidecallback.md)|初期化中にデバッグ エンジンから式エバリュエーターにコールバックを渡すことができるようにします。|
|[Terminate](../../../extensibility/debugger/reference/idebugexpressionevaluator2-terminate.md)|式エバリュエーターを停止してクリーンアップします。|

## <a name="requirements"></a>必要条件
 ヘッダー: Ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
