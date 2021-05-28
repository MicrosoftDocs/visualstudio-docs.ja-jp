---
description: デバッグ ドキュメントのチェックサムを表し、コンポーネント間でチェックサムを渡せるようにします。
title: IDebugDocumentChecksum2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentChecksum2 interface
ms.assetid: 6d22fa94-21aa-46cb-b5b5-32a6399ebb20
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 518e5b089d0d34e2492297b27dd0829e5f00ef2f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066738"
---
# <a name="idebugdocumentchecksum2"></a>IDebugDocumentChecksum2
デバッグ ドキュメントのチェックサムを表し、コンポーネント間でチェックサムを渡せるようにします。

## <a name="syntax"></a>構文

```
IDebugDocumentChecksum2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) インターフェイスを公開するどのコンポーネントでも実装できます。 しかしながら、これは主に、シンボル ファイル (*.pdb) に埋め込まれているチェックサムを IDE に渡してソースの検索時に使用できるように、デバッグ エンジンによって実装されます。

## <a name="methods"></a>メソッド
 次の表は、`IDebugDocumentChecksum2` のメソッドを示しています。

|メソッド|説明|
|------------|-----------------|
|[GetChecksumAndAlgorithmId](../../../extensibility/debugger/reference/idebugdocumentchecksum2-getchecksumandalgorithmid.md)|使用する最大バイト数を指定して、ドキュメントのチェックサムおよびアルゴリズム識別子を取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg.h

 名前空間: Microsoft.VisualStudio.Debugger.Interop

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
