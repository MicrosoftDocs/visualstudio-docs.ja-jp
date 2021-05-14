---
description: ドキュメントのクラス識別子を取得します。
title: IDebugDocument2::GetDocumentClassID | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocument2::GetDocumentClassID
helpviewer_keywords:
- IDebugDocument2::GetDocumentClassID
ms.assetid: 111c2b85-ebfa-487f-b896-2ec4a3eac4d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 829f0002a79f2fd5ec69f31ef4b59068bc5b5c05
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066855"
---
# <a name="idebugdocument2getdocumentclassid"></a>IDebugDocument2::GetDocumentClassID
ドキュメントのクラス識別子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDocumentClassID( 
   CLSID* pclsid
);
```

```csharp
int GetDocumentClassID( 
   out Guid pclsid
);
```

## <a name="parameters"></a>パラメーター
`pclsid` [出力] ドキュメントのクラス ID である GUID を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 クラス GUID を使用すれば、それぞれがドキュメントを表す個々のクラスをインスタンス化することができます。

## <a name="see-also"></a>関連項目
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
