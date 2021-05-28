---
description: 表示するメッセージを取得します。
title: IDebugMessageEvent2::GetMessage | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMessageEvent2::GetMessage
helpviewer_keywords:
- GetMessage method
- IDebugMessageEvent2::GetMessage method
ms.assetid: 9fca7285-f7f1-422d-8565-92bf0e0db60a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dc9b1747a504b761b369b2995dfef4c28ff3d012
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058470"
---
# <a name="idebugmessageevent2getmessage"></a>IDebugMessageEvent2::GetMessage
表示するメッセージを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMessage( 
   MESSAGETYPE* pMessageType,
   BSTR*        pbstrMessage,
   DWORD*       pdwType,
   BSTR*        pbstrHelpFileName,
   DWORD*       pdwHelpId
);
```

```csharp
int GetMessage( 
   out enum_MESSAGETYPE pMessageType,
   out string           pbstrMessage,
   out uint             pdwType,
   out string           pbstrHelpFileName,
   out uint             dwHelpId
);
```

## <a name="parameters"></a>パラメーター
`pMessageType`\
[出力] メッセージの種類を説明する [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md) 列挙体の値を返します。

`pbstrMessage`\
[出力] メッセージを返します。

`pdwType`\
[出力] Win32 `MessageBox` 関数の規約を使用して、メッセージの種類を返します。 詳細については、[AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox) 関数を参照してください。

`pbstrHelpFileName`\
[入力、出力] ヘルプ ファイル名を返します。 ヘルプ ファイルがない場合は、null 値 (C++) または空の値 (C#) になります。

`pdwHelpId`\
[入力、出力] ヘルプ識別子を返します。 このメッセージに関連付けられたヘルプがない場合は、0 になります。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)
- [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)
- [AfxMessageBox](/cpp/mfc/reference/cstring-formatting-and-message-box-display#afxmessagebox)
