---
description: 互換性のために残されています。 このモジュールのシンボルを再読み込みします。
title: IDebugModule2::ReloadSymbols_Deprecated | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2::ReloadSymbols
helpviewer_keywords:
- IDebugModule2::ReloadSymbols method
ms.assetid: 0f9f0133-7d58-4cd9-a6ca-1141e095749d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5dfcd1edd92048cde6da6cc195c3e0ba8f1cd392
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065711"
---
# <a name="idebugmodule2reloadsymbols_deprecated"></a>IDebugModule2::ReloadSymbols_Deprecated
互換性のために残されています。 使用しないでください。 このモジュールのシンボルを再読み込みします。

## <a name="syntax"></a>構文

```cpp
HRESULT ReloadSymbols( 
   LPCOLESTR pszUrlToSymbols,
   BSTR*     pbstrDebugMessage
);
```

```csharp
int ReloadSymbols( 
   string     pszUrlToSymbols,
   out string pbstrDebugMessage
);
```

## <a name="parameters"></a>パラメーター
`pszUrlToSymbols`\
[in] シンボル ストアへのパス。

`pbstrDebugMessage`\
[out] [モジュール] ウィンドウのモジュール名の右側に表示される情報メッセージ (状態やエラー メッセージなど) を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 デバッグ エンジンでは、常に `E_FAIL` を返す必要があります。

## <a name="remarks"></a>解説
 このメソッドはサポートされなくなりました。 代わりに [LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md) メソッドを実装してください。

## <a name="see-also"></a>関連項目
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)
