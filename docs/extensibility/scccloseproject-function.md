---
description: この関数は、プロジェクトを閉じて、特定のセッションの終了をマークします。
title: SccCloseProject 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccCloseProject
helpviewer_keywords:
- SccCloseProject function
ms.assetid: 259c2069-d349-4814-810f-1c3151b7fb84
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 859b1ddea99e74cc1c1dec999611e50216c3c98a
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904696"
---
# <a name="scccloseproject-function"></a>SccCloseProject 関数
この関数は、プロジェクトを閉じて、特定のセッションの終了をマークします。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccCloseProject (
   LPVOID pvContext
);
```

### <a name="parameters"></a>パラメーター
 pvContext: ソース管理プラグインのコンテキスト構造体。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|プロジェクトが正常に閉じられました。|
|SCC_E_PROJNOTOPEN|現在開いているプロジェクトはありません。|
|SCC_E_NOTAUTHORIZED|ユーザーには、この操作の実行が許可されていません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 この関数の前に常に [SccOpenProject](../extensibility/sccopenproject-function.md) が呼び出されます。 この関数の呼び出しの後に、`SccOpenProject` 関数または [SccUninitialize](../extensibility/sccuninitialize-function.md) の呼び出しが行われます。これにより、ソース管理システムへの接続が完全に終了します。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [SccOpenProject](../extensibility/sccopenproject-function.md)
- [SccInitialize](../extensibility/sccinitialize-function.md)
