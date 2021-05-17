---
description: このインターフェイスにより、モジュールの一覧が列挙されます。
title: IEnumDebugModules2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugModules2
helpviewer_keywords:
- IEnumDebugModules2
ms.assetid: 4fe28074-a960-41ad-b74d-b57f04c0c0ad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 96a35f11346b769a4329b1212a8202e5e5ded006
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058171"
---
# <a name="ienumdebugmodules2"></a>IEnumDebugModules2
このインターフェイスにより、モジュールの一覧が列挙されます。

## <a name="syntax"></a>構文

```
IEnumDebugModules2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、プログラムのために読み込まれたモジュールの一覧を表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 Visual Studio により、このインターフェイスを取得するために [EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md) が呼び出されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IEnumDebugModules2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md)|列挙シーケンス内の指定した数のモジュールを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugmodules2-skip.md)|列挙シーケンス内の指定した数のモジュールをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugmodules2-reset.md)|列挙型シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugmodules2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugmodules2-getcount.md)|モジュールの数を取得します。|

## <a name="remarks"></a>解説
 Visual Studio では、主にこのインターフェイスを使用して **[モジュール]** ウィンドウが更新されます。

 Visual Studio でのデバッグのために、このプログラムはモジュールの境界を越えることができるコード命令の論理的なシーケンスです。そのため、単一の [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスのモジュールの一覧が必要になります。 リスト内の最初のモジュールには、通常、関連付けられているプログラムの最初のエントリ ポイントが含まれています。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)
