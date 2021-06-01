---
description: 指定されたデバッグ エンジンのオート アタッチを有効にします。
title: IDebugCoreServer3::EnableAutoAttach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::EnableAutoAttach
helpviewer_keywords:
- IDebugCoreServer3::EnableAutoAttach
ms.assetid: 06aa633b-263b-4e08-8844-9a52d5120b94
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0e3b78744d67183c368345af8c6c26e57edec8d1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058678"
---
# <a name="idebugcoreserver3enableautoattach"></a>IDebugCoreServer3::EnableAutoAttach
指定されたデバッグ エンジンのオート アタッチを有効にします。

## <a name="syntax"></a>構文

```cpp
HRESULT EnableAutoAttach(
   GUID*     rgguidSpecificEngines,
   DWORD     celtSpecificEngines,
   LPCOLESTR pszStartPageUrl,
   BSTR*     pbstrSessionId
);
```

```csharp
int EnableAutoAttach(
   Guid[]     rgguidSpecificEngines,
   uint       celtSpecificEngines,
   string     pszStartPageUrl,
   out string pbstrSessionId
);
```

## <a name="parameters"></a>パラメーター
`rgguidSpecificEngines`\
[入力] オートアタッチとしてマークする各デバッグ エンジンの GUID の配列。

`celtSpecificEngines`\
[入力] `rgguidSpecificEngines` で指定されたエンジンの数。

`pszStartPageUrl`\
[入力] オートアタッチ時に使用する開始 URL。

`pbstrSessionID`\
[出力] オートアタッチされたセッションの ID。

## <a name="return-value"></a>戻り値
 成功した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。 エラー コードの 1 つは `E_AUTO_ATTACH_NOT_REGISTERED` です。これは、オートアタッチのクラス ファクトリが登録されていないことを示します。

## <a name="remarks"></a>解説
 指定された URL に関連付けられているプログラムが起動されると、指定されたデバッグ エンジンが自動的に起動され、アタッチされます。

## <a name="see-also"></a>関連項目
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
