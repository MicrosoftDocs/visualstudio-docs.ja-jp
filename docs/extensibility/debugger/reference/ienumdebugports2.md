---
title: IEnumDebugPorts2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2
helpviewer_keywords:
- IEnumDebugPorts2
ms.assetid: 1754eef3-cf62-42e0-b218-1911acba77d4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c24edcd5ef47408cd4c11b3d0548ad34516702a1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66326506"
---
# <a name="ienumdebugports2"></a>IEnumDebugPorts2
このインターフェイスは、コンピューターまたはポートのサプライヤーのポートを列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugPorts2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 カスタム ポート サプライヤーは、供給業者によって作成されたポートの一覧を表すためには、このインターフェイスを実装します。 Visual Studio では、独自のポート サプライヤーをサポートするためには、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元のノート
 呼び出す[EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)ポート サプライヤーによって作成されたポートの一覧を表す、このインターフェイスを取得します。 呼び出す[EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)保存されたポートの一覧を表す、このインターフェイスを取得するディスクにします。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IEnumDebugPorts2`します。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugports2-next.md)|指定された数の列挙体シーケンス内のポートを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugports2-skip.md)|指定された数の列挙体シーケンス内のポートをスキップします。|
|[Reset](../../../extensibility/debugger/reference/ienumdebugports2-reset.md)|先頭に、列挙体シーケンスをリセットします。|
|[Clone](../../../extensibility/debugger/reference/ienumdebugports2-clone.md)|現在の列挙子と同じ列挙状態を格納する列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugports2-getcount.md)|列挙子では、ポートの数を取得します。|

## <a name="remarks"></a>Remarks
 Visual Studio では、このインターフェイスを使用して、プロセスにアタッチするために使用されるポートの一覧を設定します。

 通常、デバッグ エンジンでは、このインターフェイスは使用しません。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)
- [EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)