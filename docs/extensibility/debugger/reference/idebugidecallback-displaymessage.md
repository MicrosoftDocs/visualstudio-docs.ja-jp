---
title: IDebugIDECallback::DisplayMessage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugIDECallback::DisplayMessage
ms.assetid: c19b48ee-b370-4fce-91fe-f82bf1e63179
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4a80fbc6e621e4cf1619aa310e5f7cd8beba47d7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349060"
---
# <a name="idebugidecallbackdisplaymessage"></a>IDebugIDECallback::DisplayMessage
デバッガーの出力ウィンドウには、指定したメッセージ文字列を送信します。

## <a name="syntax"></a>構文

```cpp
HRESULT DisplayMessage (
   LPCOLESTR szMessage
);
```

```csharp
int DisplayMessage (
   string szMessage
);
```

## <a name="parameters"></a>パラメーター
`szMessage`\
[in]デバッガーの出力ウィンドウに表示するメッセージ文字列。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugIDECallback](../../../extensibility/debugger/reference/idebugidecallback.md)