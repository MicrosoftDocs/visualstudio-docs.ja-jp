---
title: IEnumDebugThreads2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2
helpviewer_keywords:
- IEnumDebugThreads2
ms.assetid: 1854f078-3b49-42c2-b65b-33e3b506fd63
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 76a7267690f359d960a0c5e9b6f6a1c502d5d4f1
ms.sourcegitcommit: 50f0c3f2763a05de8482b3579026d9c76c0e226c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65461175"
---
# <a name="ienumdebugthreads2"></a>IEnumDebugThreads2
このインターフェイスは、現在のデバッグ セッションで実行中のスレッドを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugThreads2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 デバッグ エンジン (DE) は、プログラム内のスレッドの一覧を表すためには、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元のノート
 呼び出す[EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)プロセスで実行されているすべてのプログラムのすべてのスレッドのリストを表す、このインターフェイスを取得します。 呼び出す[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)プログラムで実行中のスレッドのリストを表す、このインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IEnumDebugThreads2`します。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugthreads2-next.md)|指定した列挙体シーケンス内のスレッド数を取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugthreads2-skip.md)|指定する列挙体シーケンス内のスレッド数をスキップします。|
|[Reset](../../../extensibility/debugger/reference/ienumdebugthreads2-reset.md)|先頭に、列挙体シーケンスをリセットします。|
|[Clone](../../../extensibility/debugger/reference/ienumdebugthreads2-clone.md)|現在のものと同じ列挙状態を格納する列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugthreads2-getcount.md)|列挙子では、スレッドの数を取得します。|

## <a name="remarks"></a>Remarks
 Visual Studio が通常を更新するには、このインターフェイスを取得、**スレッド**ウィンドウでもを呼び出すために、リストの最初のスレッドを取得したり[Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md)、[続行](../../../extensibility/debugger/reference/idebugprocess3-continue.md)と[手順](../../../extensibility/debugger/reference/idebugprocess3-step.md)します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
- [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)
- [Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
- [Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md)
