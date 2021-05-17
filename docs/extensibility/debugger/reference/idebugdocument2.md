---
description: このインターフェイスは、ソース ドキュメントを表します。
title: IDebugDocument2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocument2
helpviewer_keywords:
- IDebugDocument2 interface
ms.assetid: 1bc58426-dbf5-4471-9aad-9d66cd80eef0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b84aa99e1f09bc50c2148b7e03fab9e2a5bb5814
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066842"
---
# <a name="idebugdocument2"></a>IDebugDocument2
このインターフェイスは、ソース ドキュメントを表します。

## <a name="syntax"></a>構文

```
IDebugDocument2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] では通常、このインターフェイスを実装します。 デバッグ エンジン (DE) では、ソース コードを提供する必要があり、ソースがディスク上に存在しない場合にも、このインターフェイスを実装できます。  このような場合、DE では、[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) および [IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md) インターフェイスを実装するほか、[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) および [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md) インターフェイスの追加メソッドのいくつかも実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 `IDebugDocumentContext2`、`IDebugDisassemblyStream2`、`IDebugDocumentPosition2`、`IDebugActivateDocumentEvent2` の各インターフェイスのメソッドは、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugDocument2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)|いくつかの形式のいずれかでドキュメントの名前を取得します。|
|[GetDocumentClassID](../../../extensibility/debugger/reference/idebugdocument2-getdocumentclassid.md)|ドキュメントのクラス識別子を取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、DE がソース コードを提供する場合にのみ実装されます。 たとえば、HTML ページ上のスクリプトをデバッグしている場合、ソースは動的にダウンロードまたは生成され、ディスク ファイルとしては存在しないため、DE がソース コードを提供します。 C++ などの従来の言語をデバッグする場合は、このインターフェイスを実装する必要はありません。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)
