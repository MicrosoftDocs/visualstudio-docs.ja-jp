---
title: IDebugExpressionContext2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2
helpviewer_keywords:
- IDebugExpressionContext2 interface
ms.assetid: 577fdaae-4b2d-4112-9839-ab899535fa6f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3ad9c3d6bb1b0a5baccbcf5bf47eb02a8bb5efa5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66325855"
---
# <a name="idebugexpressioncontext2"></a>IDebugExpressionContext2
このインターフェイスは、式の評価のコンテキストを表します。

## <a name="syntax"></a>構文

```
IDebugExpressionContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 デバッグ エンジン (DE) は、式を評価できるコンテキストを表すには、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元のノート
 呼び出し[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md) this を返しますインターフェイス。 このインターフェイスは、デバッグ中のプログラムが一時停止されているし、スタック フレームは、使用可能な場合にのみアクセスできます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IDebugExpressionContext2`します。

|メソッド|説明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugexpressioncontext2-getname.md)|評価コンテキストの名前を取得します。|
|[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)|評価のためのテキスト ベースの式を解析します。|

## <a name="remarks"></a>Remarks
 評価コンテキストは、式の評価を実行するためのスコープとして考えることができます。

 セッション デバッグ マネージャー (SDM) がへの呼び出しで DE からスタック フレームを取得するプログラムが停止されると、 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)します。 SDM を呼び出して[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)を取得する、`IDebugExpressionContext2`インターフェイス。 これがへの呼び出しに続く[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)を作成する、 [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)インターフェイスで、すぐに評価できる解析された式を表します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)