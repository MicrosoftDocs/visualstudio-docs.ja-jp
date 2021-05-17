---
description: このインターフェイスは、ソース ファイル ドキュメント内の位置を表します。
title: IDebugDocumentContext2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2
helpviewer_keywords:
- IDebugDocumentContext2
ms.assetid: 2a446c71-8100-4c09-a1cc-fd446bd74030
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a20473d2076932987ecc352c8719f1d9133ed198
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066517"
---
# <a name="idebugdocumentcontext2"></a>IDebugDocumentContext2
このインターフェイスは、ソース ファイル ドキュメント内の位置を表します。

## <a name="syntax"></a>構文

```
IDebugDocumentContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) では、ソース コード レベルのデバッグに対するサポートの一環としてこのインターフェイスを実装します。 ソース コード内の位置に加えて、このインターフェイスは、コンテキストを比較したり、ソース コード ドキュメントをナビゲートしたりするためのメソッドを提供します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 いくつかのインターフェイス (最も典型的なのは [GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) および [GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md) インターフェイス) のメソッドは、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugDocumentContext2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)|このドキュメント コンテキストを含んでいるドキュメントを取得します。|
|[GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)|このドキュメント コンテキストを含むドキュメントの表示可能な名前を取得します。|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)|このドキュメント コンテキストに関連付けられているすべてのコード コンテキストのリストを取得します。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugdocumentcontext2-getlanguageinfo.md)|このドキュメント コンテキストに関連付けられている言語を取得します。|
|[GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|このドキュメント コンテキストのファイル ステートメントの範囲を取得します。|
|[GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)|このドキュメント コンテキストのファイル ソースの範囲を取得します。|
|[比較](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)|このドキュメント コンテキストを、指定されたドキュメント コンテキストの配列と比較します。|
|[Seek](../../../extensibility/debugger/reference/idebugdocumentcontext2-seek.md)|指定された数のステートメントまたは行だけドキュメント コンテキストを移動します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)
