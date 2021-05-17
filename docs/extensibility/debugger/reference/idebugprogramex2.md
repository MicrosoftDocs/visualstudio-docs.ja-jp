---
description: このインターフェイスを使用すると、セッション デバッグ マネージャー (SDM) をプログラムにアタッチし、プログラムに関連付けられたプログラム ノードを取得できます。
title: IDebugProgramEx2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2
helpviewer_keywords:
- IDebugProgramEx2 interface
ms.assetid: 663359ed-635a-4539-addb-0cc52f19d1bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e39a469d04ac14f3ed36366d035bf4ca01a9d2ef
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087328"
---
# <a name="idebugprogramex2"></a>IDebugProgramEx2
このインターフェイスを使用すると、セッション デバッグ マネージャー (SDM) をプログラムにアタッチし、プログラムに関連付けられたプログラム ノードを取得できます。

## <a name="syntax"></a>構文

```
IDebugProgramEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタム ポート サプライヤーでは、[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスと同じオブジェクトにこのインターフェイスを実装して、SDM がプログラムにアタッチされるようにします。同時に、ポート サプライヤーでそのプログラムにアタッチされているすべてのセッションを追跡できるようにします。 カスタム ポート サプライヤーでは、このインターフェイスを実装できます (選択した場合)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 SDM では、プログラムにアタッチされたセッションを追跡するために、`IDebugProgram2` インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出してこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugProgramEx2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[[アタッチ]](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)|セッションにプログラムをアタッチします。|
|[GetProgramNode](../../../extensibility/debugger/reference/idebugprogramex2-getprogramnode.md)|プログラムに関連付けられているプログラム ノードを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、SDM とプログラムの間でプライベートです。

## <a name="requirements"></a>必要条件
 ヘッダー: Portpriv.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
