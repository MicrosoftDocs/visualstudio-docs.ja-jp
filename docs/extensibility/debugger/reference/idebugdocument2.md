---
title: IDebugDocument2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocument2
helpviewer_keywords:
- IDebugDocument2 interface
ms.assetid: 1bc58426-dbf5-4471-9aad-9d66cd80eef0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 23510910fe18c68107e2c497aac5913da1eae963
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310222"
---
# <a name="idebugdocument2"></a>IDebugDocument2
このインターフェイスは、ソース ドキュメントを表します。

## <a name="syntax"></a>構文

```
IDebugDocument2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 一般にこのインターフェイスを実装します。 デバッグ エンジン (DE) は、ソース コードを指定する必要があるあり、ソースがディスクに存在しない場合にも、このインターフェイスに実装できます。  このような場合、DE は実装にも[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)と[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)で追加のメソッドと同様に、インターフェイス、 [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)と[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)インターフェイス。

## <a name="notes-for-callers"></a>呼び出し元のノート
 上のメソッド、 `IDebugDocumentContext2`、 `IDebugDisassemblyStream2`、 `IDebugDocumentPosition2`、および`IDebugActivateDocumentEvent2`インターフェイスは、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IDebugDocument2`します。

|メソッド|説明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)|いくつかの形式のいずれかで、ドキュメントの名前を取得します。|
|[GetDocumentClassID](../../../extensibility/debugger/reference/idebugdocument2-getdocumentclassid.md)|ドキュメントのクラス識別子を取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは、DE、ソース コードを提供する場合にのみ実装されます。 たとえば、HTML ページ上のスクリプトをデバッグする場合、DE を提供ソース コード、ソースをダウンロードまたは動的に生成されるため、ディスク ファイルとして存在しません。 C++ などの従来の言語をデバッグするときに、このインターフェイスを実装する必要はありません。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)