---
description: ドキュメント内でテキストが置換されていることをデバッグ パッケージに通知します。
title: IDebugDocumentTextEvents2::onReplaceText | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2::OnReplaceText
helpviewer_keywords:
- IDebugDocumentTextEvents2::onReplaceText
ms.assetid: cb39f025-66d8-4dc0-bef6-1bdc8e07db92
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9f57c0a48e523a57582130107a0d8b1012b1232e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054349"
---
# <a name="idebugdocumenttextevents2onreplacetext"></a>IDebugDocumentTextEvents2::onReplaceText
ドキュメント内でテキストが置換されていることをデバッグ パッケージに通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT onReplaceText( 
   TEXT_POSITION pos,
   DWORD         dwNumToReplace
);
```

```csharp
int onReplaceText( 
   enum_TEXT_POSITION pos,
   uint               dwNumToReplace
);
```

## <a name="parameters"></a>パラメーター
`pos`\
[入力] [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) からは、テキストの置換箇所が示されます。

`dwNumToReplace`\
[入力] 置換されたテキストの文字数を指定します。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
