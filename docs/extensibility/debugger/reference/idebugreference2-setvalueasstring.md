---
description: 文字列から参照の値を設定します。
title: IDebugReference2::SetValueAsString | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::SetValueAsString
helpviewer_keywords:
- IDebugReference2::SetValueAsString
ms.assetid: 9a508ced-fd54-44f5-bb42-ec15c80384d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9eb557adcd9748f559d0d0c27877b84343c8fc98
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075771"
---
# <a name="idebugreference2setvalueasstring"></a>IDebugReference2::SetValueAsString
文字列から参照の値を設定します。 将来使用するために予約されています。

## <a name="syntax"></a>構文

```cpp
HRESULT SetValueAsString ( 
   LPCOLESTR pszValue,
   DWORD     dwRadix,
   DWORD     dwTimeout
);
```

```csharp
int SetValueAsString ( 
   string pszValue,
   uint   dwRadix,
   uint   dwTimeout
);
```

## <a name="parameters"></a>パラメーター
`pszValue`\
[入力] 文字列としての値。

`dwRadix`\
[入力] 数値情報の書式設定に使用される基数。

`dwTimeout`\
[入力] このメソッドから戻る前に待機する最大時間 (ミリ秒単位)。 無期限に待機するには `INFINITE` を使用します。

## <a name="return-value"></a>戻り値
 常に `E_NOTIMPL` を返します。

## <a name="see-also"></a>関連項目
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
