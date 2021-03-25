---
description: ドキュメントにテキストが挿入されたことをデバッグパッケージに通知します。
title: 'IDebugDocumentTextEvents2:: onInsertText |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2::OnInsertText
helpviewer_keywords:
- IDebugDocumentTextEvents2::onInsertText
ms.assetid: 6040181f-7288-4a42-953c-d23f74200431
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b98361636e75ee2338cd32cd9782c53a4fb87d98
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066101"
---
# <a name="idebugdocumenttextevents2oninserttext"></a>IDebugDocumentTextEvents2::onInsertText
ドキュメントにテキストが挿入されたことをデバッグパッケージに通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT onInsert( 
   TEXT_POSITION pos,
   DWORD         dwNumToInsert
);
```

```csharp
int onInsert( 
   enum_TEXT_POSITION pos,
   uint               dwNumToInsert
);
```

## <a name="parameters"></a>パラメーター
`pos`\
からテキストが挿入された場所を示す [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 構造体。

`dwNumToInsert`\
から挿入されたテキストの文字数を指定します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
