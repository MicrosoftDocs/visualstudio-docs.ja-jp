---
title: IDebugDocumentPosition2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2
helpviewer_keywords:
- IDebugDocumentPosition2 interface
ms.assetid: 0e838ced-12bb-4efc-b811-2b7c034b77b0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 36c2fbce0154a5ebefd04ea3614d16db16799510
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333419"
---
# <a name="idebugdocumentposition2"></a>IDebugDocumentPosition2
このインターフェイスは、ソース ファイル内の抽象の位置を表します。

## <a name="syntax"></a>構文

```
IDebugDocumentPosition2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装についてのメモ
 Visual Studio は、通常、このインターフェイスを実装します。 ソース コードを提供する必要がある場合は、デバッグ エンジン (DE) はこのインターフェイスを実装もは (デが実装すると、 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)インターフェイス)。

## <a name="notes-for-callers"></a>呼び出し元のノート
 このインターフェイスへの引数として渡される[EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)します。 一部としても指定した、 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)共用体 (具体的を[BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)構造) の一部で、さらに、 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)構造体保留中のブレークポイントの作成に使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、メソッドの`IDebugDocumentPosition2`します。

|メソッド|説明|
|------------|-----------------|
|[GetFileName](../../../extensibility/debugger/reference/idebugdocumentposition2-getfilename.md)|このドキュメントの位置を含むソース ファイルのファイル名を取得します。|
|[GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)|コンテナーのドキュメントを取得します。|
|[IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)|この位置が特定のドキュメントに含まれているかどうかを決定します。|
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)|このドキュメントの位置の範囲を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ:Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)