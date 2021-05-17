---
description: このインターフェイスでは、デバッグ セッション、あるいは特定のプログラムまたはドキュメントに関連付けられたコード コンテキストが列挙されます。
title: IEnumDebugCodeContexts2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2
helpviewer_keywords:
- IEnumDebugCodeContexts2
ms.assetid: 72915146-215f-4c99-a034-131b2b474e0e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 72addd1bd5a71f8d6051d1a7100d2d34dab57a24
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086574"
---
# <a name="ienumdebugcodecontexts2"></a>IEnumDebugCodeContexts2
このインターフェイスでは、デバッグ セッション、あるいは特定のプログラムまたはドキュメントに関連付けられたコード コンテキストが列挙されます。

## <a name="syntax"></a>構文

```
IEnumDebugCodeContexts2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、このインターフェイスを実装して、プログラム内の特定のテキスト位置のコード コンテキストのリスト、または特定のドキュメント コンテキストのコード コンテキストのリストを表します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 プログラムのソース ドキュメント内の特定のテキスト位置のコード コンテキストのリストを表すこのインターフェイスを取得するには、[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md) を呼び出します。

 特定のソース ドキュメント内のすべてのコード コンテキストのリストを表すこのインターフェイスを取得するには、[EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IEnumDebugCodeContexts2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)|列挙シーケンス内の指定した数のコード コンテキストを取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-skip.md)|列挙シーケンス内の指定した数のコード コンテキストをスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-reset.md)|列挙型シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-getcount.md)|列挙子内のコード コンテキストの数を取得します。|

## <a name="remarks"></a>解説
 Visual Studio では、次のステートメントを設定するとき、またはソース ファイルの逆アセンブリを表示するときに、[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md) を呼び出して、ユーザーが選択できるコード コンテキストのリストを事前設定します。 複数のコード コンテキストが発生する可能性があります。たとえば、C++ スタイルのテンプレートが複数インスタンスある場合です。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)
