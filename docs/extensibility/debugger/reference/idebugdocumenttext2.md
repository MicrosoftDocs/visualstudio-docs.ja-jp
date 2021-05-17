---
description: このインターフェイスは、テキスト ドキュメントを表します。
title: IDebugDocumentText2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentText2
helpviewer_keywords:
- IDebugDocumentText2 interface
ms.assetid: e85f50a3-211c-4220-a9f4-789950ba2782
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 557ae68e63280348ab315c3240e05dbfc38a8d4d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066283"
---
# <a name="idebugdocumenttext2"></a>IDebugDocumentText2
このインターフェイスは、テキスト ドキュメントを表します。

## <a name="syntax"></a>構文

```
IDebugDocumentText2 : IDebugDocument2
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグ エンジン (DE) で提供する必要があるソース コードがテキスト形式の場合に、DE でこのインターフェイスを実装します。 これは最も一般的なケースであるため、[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) インターフェイスを実装する場合、DE では `IDebugDocumentText2` インターフェイスも実装する必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 `IDebugDocument2` インターフェイスからこのインターフェイスを取得するには、`QueryInterface` メソッドを使用します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスでは、`IDebugDocument2` インターフェイスのメソッドに加えて、次のメソッドが実装されます。

|メソッド|説明|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugdocumenttext2-getsize.md)|ドキュメント内のこの位置にあるテキストのサイズを取得します。|
|[GetText](../../../extensibility/debugger/reference/idebugdocumenttext2-gettext.md)|ドキュメント内の指定された位置からテキストを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスを実装するオブジェクトは、[IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md) オブジェクトの <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> インターフェイスを提供する <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> インターフェイスも実装する必要があります。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
