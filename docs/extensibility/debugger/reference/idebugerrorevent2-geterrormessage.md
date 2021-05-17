---
description: 人間が判読できるエラー メッセージを構築するための情報を返します。
title: IDebugErrorEvent2::GetErrorMessage | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorEvent2::GetErrorMessage
helpviewer_keywords:
- IDebugErrorEvent2::GetErrorMessage
ms.assetid: 9e3b0d74-a2dd-4eaa-bd95-21b2f9c79409
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a0ab15c0f232695dbc017d80f666154e5c35a8fd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065776"
---
# <a name="idebugerrorevent2geterrormessage"></a>IDebugErrorEvent2::GetErrorMessage
人間が判読できるエラー メッセージを構築するための情報を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetErrorMessage(
   MESSAGETYPE* pMessageType,
   BSTR*        pbstrErrorFormat,
   HRESULT*     hrErrorReason,
   DWORD*       pdwType,
   BSTR*        pbstrHelpFileName,
   DWORD*       pdwHelpId
);
```

```csharp
int GetErrorMessage(
   out enum_MESSAGETYPE   pMessageType,
   out string             pbstrErrorFormat,
   out int                phrErrorReason,
   out uint               pdwType,
   out string             pbstrHelpFileName,
   out uint               pdwHelpId
);
```

## <a name="parameters"></a>パラメーター
`pMessageType`\
[出力] メッセージの種類を記述する [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md) 列挙型の値を返します。

`pbstrErrorFormat`\
[出力] ユーザーへの最終的なメッセージの形式 (詳しくは「解説」を参照)。

`hrErrorReason`\
[出力] メッセージで説明しているエラー コード。

`pdwType`\
[出力] エラーの重大度 (`MessageBox` には MB_XXX 定数を使用。例: `MB_EXCLAMATION`、`MB_WARNING`)。

`pbstrHelpFileName`\
[出力] ヘルプ ファイルのパス (ヘルプ ファイルがない場合は null 値に設定)。

`pdwHelpId`\
[出力] 表示するヘルプ トピックの ID (ヘルプ トピックがない場合は 0 に設定)。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 エラー メッセージは、行 `"What I was doing.  %1"` のように書式設定する必要があります。 `"%1"` は呼び出し元によって、(`hrErrorReason` で返された) エラー コードから派生したエラー メッセージに置き換えられます。 `pMessageType` パラメーターは、最終的なエラー メッセージの表示方法を呼び出し元に指示します。

## <a name="see-also"></a>関連項目
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [MESSAGETYPE](../../../extensibility/debugger/reference/messagetype.md)
