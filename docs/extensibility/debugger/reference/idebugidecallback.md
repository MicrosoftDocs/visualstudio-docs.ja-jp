---
description: 式エバリュエーター (EE) でデバッガーの出力ウィンドウにメッセージを表示できるようにします。
title: IDebugIDECallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugIDECallback interface
ms.assetid: 8d31adc0-1c44-4658-8d4f-f4b73e35f4a6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 461003f3bdb83e51e8b5c525895d134b717d8fc6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091904"
---
# <a name="idebugidecallback"></a>IDebugIDECallback
> [!IMPORTANT]
> Visual Studio 2015 では、この方法による式エバリュエーターの実装は非推奨です。 CLR 式エバリュエーターの実装については、[CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)および[マネージド式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)に関する記事をご覧ください。

 式エバリュエーター (EE) でデバッガーの出力ウィンドウにメッセージを表示できるようにします。

## <a name="syntax"></a>構文

```
IDebugIDECallback : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このコールバックは、マネージド デバッグ エンジンによって実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 デバッガーの出力ウィンドウに出力を送信するために、式エバリュエーターで使用される可能性があります。

## <a name="methods"></a>メソッド
 このインターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[DisplayMessage](../../../extensibility/debugger/reference/idebugidecallback-displaymessage.md)|指定されたメッセージ文字列をデバッガーの出力ウィンドウに送信します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Ee.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
