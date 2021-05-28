---
description: このインターフェイスを使用すると、デバッグ ポートで実行されているプロセスが列挙されます。
title: IEnumDebugProcesses2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugProcesses2
helpviewer_keywords:
- IEnumDebugProcesses2
ms.assetid: 06a1368f-10f0-44eb-af61-e388c2327111
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1272c57b58b4e2656775bf746d470a3514c886ea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064541"
---
# <a name="ienumdebugprocesses2"></a>IEnumDebugProcesses2
このインターフェイスを使用すると、デバッグ ポートで実行されているプロセスが列挙されます。

## <a name="syntax"></a>構文

```
IEnumDebugProcesses : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 カスタム オート サプライヤーは、このインターフェイスを実装して、ポートで実行されているプロセスの一覧を提供します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 Visual Studio では、[EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md) を呼び出して、このインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、`IEnumDebugProcesses2` のメソッドを示しています。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugprocesses2-next.md)|列挙シーケンス内の指定された数のプロセスを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugprocesses2-skip.md)|列挙シーケンス内の指定された数のプロセスをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugprocesses2-reset.md)|列挙型シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugprocesses2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugprocesses2-getcount.md)|列挙子内のプロセスの数を取得します。|

## <a name="remarks"></a>解説
 Visual Studio では、このインターフェイスを使用して、 **[プロセス]** ウィンドウを設定します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumProcesses](../../../extensibility/debugger/reference/idebugport2-enumprocesses.md)
