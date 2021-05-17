---
description: このインターフェイスは、ソース ファイル内の抽象位置を表します。
title: IDebugDocumentPosition2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2
helpviewer_keywords:
- IDebugDocumentPosition2 interface
ms.assetid: 0e838ced-12bb-4efc-b811-2b7c034b77b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8b7c4c8e469dff76e2af631c4943305b0e3ee8e7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066400"
---
# <a name="idebugdocumentposition2"></a>IDebugDocumentPosition2
このインターフェイスは、ソース ファイル内の抽象位置を表します。

## <a name="syntax"></a>構文

```
IDebugDocumentPosition2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 通常は、Visual Studio がこのインターフェイスを実装します。 デバッグ エンジン (DE) で [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) インターフェイスを実装する場合のように、DE で独自のソース コードを提供する必要がある場合は、DE でもこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md) への引数としてに渡されます。 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 共用体 (具体的には、保留中のブレークポイントの作成に使用される [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 構造体の一部である [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md) 構造体) の一部としても提供されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、`IDebugDocumentPosition2` のメソッドを示します。

|メソッド|説明|
|------------|-----------------|
|[GetFileName](../../../extensibility/debugger/reference/idebugdocumentposition2-getfilename.md)|このドキュメントの位置が格納されているソース ファイルのファイル名を取得します。|
|[GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)|格納元のドキュメントを取得します。|
|[IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)|この位置が特定のドキュメントに含まれているかどうかを判断します。|
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)|このドキュメントの位置の範囲を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)
