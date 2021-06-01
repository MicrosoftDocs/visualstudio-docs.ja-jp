---
description: このインターフェイスはコード パスの一覧を表します。
title: IEnumCodePaths2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCodePaths2
helpviewer_keywords:
- IEnumCodePaths2 interface
ms.assetid: 17ec9f9e-dc06-4532-b5db-da52efcc8630
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e8ff8b4532ab67a969c8270eeb83bdf715e0b1c0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091735"
---
# <a name="ienumcodepaths2"></a>IEnumCodePaths2
このインターフェイスはコード パスの一覧を表します。

## <a name="syntax"></a>構文

```
IEnumCodePaths2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、コード パスの一覧を表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、[EnumCodePaths](../../../extensibility/debugger/reference/idebugprogram2-enumcodepaths.md) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に `IEnumCodePaths2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumcodepaths2-next.md)|列挙シーケンス内の指定した数のコード パスを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumcodepaths2-skip.md)|列挙シーケンス内の指定した数のコード パスをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumcodepaths2-reset.md)|列挙型シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumcodepaths2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumcodepaths2-getcount.md)|列挙子内のコード パスの数を取得します。|

## <a name="remarks"></a>解説
 コード パスは、プログラム内の分岐点または関数呼び出しを表します。 コード パスの一覧は、コードが実行されたパスを表します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
