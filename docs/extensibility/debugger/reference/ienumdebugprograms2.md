---
description: このインターフェイスは、現在のデバッグ セッションで実行されているプログラムを列挙します。
title: IEnumDebugPrograms2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPrograms2
helpviewer_keywords:
- IEnumDebugPrograms2
ms.assetid: 7fbb8fb7-db64-4546-a364-dc668430c8af
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d7f9a981146d5e024333f17557f4fdbc3d35bc05
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082934"
---
# <a name="ienumdebugprograms2"></a>IEnumDebugPrograms2
このインターフェイスは、現在のデバッグ セッションで実行されているプログラムを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugPrograms2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、DE によってデバッグ中のプログラムの一覧を提供するために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 Visual Studio では、このインターフェイスを取得するために [EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md) を呼び出します。 [EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md) は Visual Studio では使用されません。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IEnumDebugPrograms2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)|列挙型シーケンス内の指定した数のプログラムを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugprograms2-skip.md)|列挙型シーケンス内の指定した数のプログラムをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugprograms2-reset.md)|列挙型シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugprograms2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugprograms2-getcount.md)|列挙子内のプログラムの数を取得します。|

## <a name="remarks"></a>解説
 Visual Studio では、このインターフェイスを使用して次のことを行います。

- **[モジュール]** ウィンドウを設定します ([EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md) を呼び出して、次に各プログラムで [EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md) を呼び出します)。

- **[プロセスにアタッチ]** の一覧を作成します (`IDebugProcess2::EnumPrograms` を呼び出し、次に各 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスで [QueryInterface](/cpp/atl/queryinterface) を呼び出して [IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md) インターフェイスを取得します)。

- プロセス内の各プログラムをデバッグできる DE の一覧を生成します ([GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md) を使用)。

- エディット コンティニュ (ENC) の更新プログラムを各プログラムに適用します (IDebugProcess2::EnumPrograms を呼び出し、次に [GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md) を呼び出します)。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)
- [EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)
