---
title: IDebugSettingsCallback2::GetEEMetricString |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetEEMetricString
ms.assetid: 85e3c093-6a91-4101-ab32-d8ac6eed4918
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a3cad87c74a00f2feac4390921be032ed3f8b6cc
ms.sourcegitcommit: 19ec963ed6d585719cb83ba677434ea6580e0d1f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66212098"
---
# <a name="idebugsettingscallback2geteemetricstring"></a>IDebugSettingsCallback2::GetEEMetricString
指定した名前、式エバリュエーターのメトリックの値の文字列を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEEMetricString(
   REFGUID guidLang,
   REFGUID guidVendor,
   LPCWSTR pszMetric,
   BSTR*   pbstrValue
);
```

```csharp
private int GetEEMetricString(
   ref Guid   guidLang,
   ref Guid   guidVendor,
   string     pszMetric,
   out string pbstrValue
);
```

## <a name="parameters"></a>パラメーター
`guidLang`\
[in]プログラミング言語の一意の識別子。

`guidVendor`\
[in]ベンダーの一意の識別子。

`pszMetric`\
[in]メトリックの名前。

`pbstrValue`\
[out]メトリック値の文字列を返します。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)