---
description: この関数は、ユーザー固有のさまざまなオプションを取得します。
title: SccGetUserOption 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SccGetUserOption
helpviewer_keywords:
- SccGetUserOption function
ms.assetid: 17863747-1901-4c53-a2b3-ed996085e120
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 622abc04609edf410214af6b8acf795f969e2fbc
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901111"
---
# <a name="sccgetuseroption-function"></a>SccGetUserOption 関数
この関数は、ユーザー固有のさまざまなオプションを取得します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGetUserOption(
   LPVOID pContext,
   LONG nOption,
   LPLONG lpVal
);
```

#### <a name="parameters"></a>パラメーター
 pContext

[入力] ソース制御プラグインのコンテキスト ポインター

 nOption

[入力] 取得するオプション (取得可能なオプションについては、「注釈」を参照してください)。

 lpVal

[出力] オプションに関連付けられた値。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値が返されることが予期されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|オプションは正常に取得されました。|
|SCC_E_OPNOTSUPPORTED|オプションはサポートされていません。|
|SCC_E_NONSPECIFICERROR|未指定のエラーが発生しました。|

## <a name="remarks"></a>解説
 このコマンドでは、次のオプションがサポートされています。

|User オプション|説明|
|-----------------|-----------------|
|`SCC_USEROPT_CHECKOUT_LOCALVER`|ユーザーがファイルのローカル バージョンをチェックアウトすることを希望しているかどうかを決定します。 `lpVal` には、`SCC_USEROPT_COLV_YES` (ユーザーはローカル ファイルのチェックアウトを希望している) または `SCC_USEROPT_COLV_NO`が割り当てられます。|

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [エラー コード](../extensibility/error-codes.md)
