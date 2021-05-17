---
description: このインターフェイスは、現在のデバッグ セッションで実行されているスレッドを列挙します。
title: IEnumDebugThreads2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2
helpviewer_keywords:
- IEnumDebugThreads2
ms.assetid: 1854f078-3b49-42c2-b65b-33e3b506fd63
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 97cb6f4d0425fb75ebaa9375e53e3ba6d5075e00
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082648"
---
# <a name="ienumdebugthreads2"></a>IEnumDebugThreads2
このインターフェイスは、現在のデバッグ セッションで実行されているスレッドを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugThreads2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、プログラム内のスレッドの一覧を表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md) を呼び出して、プロセス内で実行されているすべてのプログラムのすべてのスレッドの一覧を表すこのインターフェイスを取得します。 [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) を呼び出して、プログラム内で実行されているスレッドの一覧を表すこのインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IEnumDebugThreads2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugthreads2-next.md)|列挙型シーケンス内の指定した数のスレッドを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugthreads2-skip.md)|列挙型シーケンス内の指定した数のスレッドをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugthreads2-reset.md)|列挙型シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugthreads2-clone.md)|現在のものと同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugthreads2-getcount.md)|列挙子内のスレッドの数を取得します。|

## <a name="remarks"></a>解説
 通常、Visual Studio では、 **[スレッド]** ウィンドウを更新するためにこのインターフェイスを取得し、[Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md)、[Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)、[Step](../../../extensibility/debugger/reference/idebugprocess3-step.md) を呼び出すために、一覧の最初のスレッドを取得します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
- [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)
- [続行](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
- [実行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)
