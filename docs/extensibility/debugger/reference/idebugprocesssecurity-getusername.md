---
description: ポート サプライヤーからユーザー名を取得します。
title: IDebugProcessSecurity::GetUserName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::GetUserName
ms.assetid: c73c60ac-da6e-45ae-8f04-95353a24ca3e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 42a13075b233d5b0fe70b314a4b2d025a2a4c7d3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076304"
---
# <a name="idebugprocesssecuritygetusername"></a>IDebugProcessSecurity::GetUserName
ポート サプライヤーからユーザー名を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetUserName(
    BSTR *pbstrUserName
);
```

```csharp
int GetUserName (
    string pbstrUserName
);
```

## <a name="parameters"></a>パラメーター
`pbstrUserName`\
[out] ユーザー名を含む文字列。

## <a name="return-value"></a>戻り値
 メソッドが成功した場合は `S_OK` を返します。 それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>解説
 `GetUserName` では、 **[プロセスにアタッチ]** ダイアログ ボックスの **[ユーザー名]** 列に表示されるユーザー名を返します。 **[プロセスにアタッチ]** ダイアログ ボックスを表示するには、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) で **[ツール]** メニューの **[プロセスにアタッチ]** をクリックします。

## <a name="see-also"></a>関連項目
- [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
