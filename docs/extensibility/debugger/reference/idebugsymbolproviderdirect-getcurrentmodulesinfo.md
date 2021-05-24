---
description: シンボル グループ内のモジュールに関する情報を取得します。
title: IDebugSymbolProviderDirect::GetCurrentModulesInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSymbolProviderDirect::GetCurrentModulesInfo
- GetCurrentModulesInfo
ms.assetid: b3b45ed2-ea4e-4389-b78a-11fc9796a6c1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d59c3bd88c82d6f7bacc7ce66c33b36a137d4e8b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081348"
---
# <a name="idebugsymbolproviderdirectgetcurrentmodulesinfo"></a>IDebugSymbolProviderDirect::GetCurrentModulesInfo
シンボル グループ内のモジュールに関する情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCurrentModulesInfo(
   unsigned long * pCount,
   GUID *          ppGuids,
   DWORD *         pADIds,
   DWORD *         pCurrentState,
   IUnknown **     ppCDModItfs
);
```

```csharp
int GetCurrentModulesInfo(
   uint       pCount,
   Guid       ppGuids,
   uint       pADIds,
   uint       pCurrentState,
   out object ppCDModItfs
);
```

## <a name="parameters"></a>パラメーター
`pCount`\
[in] `ppGuids` 配列内のモジュールの数。

`ppGuids`\
[in] モジュールの一意の識別子を格納している配列。

`pADIds`\
[in] アプリケーション ドメインの識別子。

`pCurrentState`\
[in] シンボル グループの現在の状態。

`ppCDModItfs`\
[out] シンボル グループ内のモジュールを含むオブジェクトを返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)
