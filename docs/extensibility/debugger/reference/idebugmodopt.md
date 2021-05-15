---
description: デバッグの省略可能な修飾子を表します。
title: IDebugModOpt | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt interface
ms.assetid: ebd525e3-d140-4071-9d8c-41871de4125e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ffb235d58c254d130636da0f4b97961c11f9a372
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087900"
---
# <a name="idebugmodopt"></a>IDebugModOpt
デバッグの省略可能な修飾子を表します。

## <a name="syntax"></a>構文

```
IDebugModOpt : IUnknown
```

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 クラスまたはメソッドを表す [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) オブジェクトから取得されます。

## <a name="methods"></a>メソッド
 このインターフェイスには、次のメソッドが実装されています。

|メソッド|説明|
|------------|-----------------|
|[GetModOpts](../../../extensibility/debugger/reference/idebugmodopt-getmodopts.md)|省略可能な修飾子のリストを取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Sh.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
