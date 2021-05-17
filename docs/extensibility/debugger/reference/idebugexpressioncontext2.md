---
title: IDebugExpressionContext2 | Microsoft Docs
description: このインターフェイスは、式の評価のコンテキストを表します
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2
helpviewer_keywords:
- IDebugExpressionContext2 interface
ms.assetid: 577fdaae-4b2d-4112-9839-ab899535fa6f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f6d8745207f1ab075aedd43815e7a97a4f0721bb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092294"
---
# <a name="idebugexpressioncontext2"></a>IDebugExpressionContext2
このインターフェイスは、式の評価のコンテキストを表します。

## <a name="syntax"></a>構文

```
IDebugExpressionContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) は、式を評価できるコンテキストを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) の呼び出しで、このインターフェイスを返します。 このインターフェイスには、デバッグ中のプログラムが一時停止され、スタック フレームが使用可能な場合にのみアクセスできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugExpressionContext2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugexpressioncontext2-getname.md)|評価コンテキストの名前を取得します。|
|[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)|評価のためにテキストベースの式を解析します。|

## <a name="remarks"></a>解説
 評価コンテキストは、式の評価を実行するためのスコープと考えることができます。

 プログラムが停止されると、セッション デバッグ マネージャー (SDM) は、[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) の呼び出しによって DE からスタック フレームを取得します。 次に、SDM は、[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) を呼び出して、`IDebugExpressionContext2` インターフェイスを取得します。 この後に [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) を呼び出して、評価の準備ができている解析済みの式を表す [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md) インターフェイスを作成します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
