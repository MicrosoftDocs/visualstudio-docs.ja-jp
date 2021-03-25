---
description: ドキュメントの位置が特定のドキュメントに含まれるかどうかを判断します。
title: 'IDebugDocumentPosition2:: IsPositionInDocument |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2::IsPositionInDocument
helpviewer_keywords:
- IDebugDocumentPosition2::IsPositionInDocument
ms.assetid: d5cf57cb-b93b-4e1d-bec9-185f4fe8668d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ab3d00df9883da93d0d8121433b962d365a408e3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066413"
---
# <a name="idebugdocumentposition2ispositionindocument"></a>IDebugDocumentPosition2::IsPositionInDocument
ドキュメントの位置が特定のドキュメントに含まれるかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsPositionInDocument( 
   IDebugDocument2* pDoc
);
```

```csharp
int IsPositionInDocument( 
   IDebugDocument2 pDoc
);
```

## <a name="parameters"></a>パラメーター
`pDoc`\
からドキュメントの候補を含むを表す [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドは、主に [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) インターフェイスでブレークポイントを設定するときに使用されます。 ドキュメントが読み込まれると、ブレークポイントの位置が呼び出され、ドキュメントにこの位置が含まれているかどうかが判断されます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
