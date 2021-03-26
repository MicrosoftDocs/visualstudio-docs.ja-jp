---
description: この関数は、さまざまなユーザー固有のオプションを取得します。
title: SccGetUserOption 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 262a15069f840c048f574396d5a7ec076760d77e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063956"
---
# <a name="sccgetuseroption-function"></a>SccGetUserOption 関数
この関数は、さまざまなユーザー固有のオプションを取得します。

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

からソース管理プラグインのコンテキストポインター。

 いいえ

から取得するオプション (使用可能なオプションについては、「解説」を参照してください)。

 lpVal

入出力オプションに関連付けられている値。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。

|値|説明|
|-----------|-----------------|
|SCC_OK|オプションが正常に取得されました。|
|SCC_E_OPNOTSUPPORTED|オプションはサポートされていません。|
|SCC_E_NONSPECIFICERROR|未指定のエラーが発生しました。|

## <a name="remarks"></a>注釈
 このコマンドでは、次のオプションがサポートされています。

|ユーザーオプション|Description|
|-----------------|-----------------|
|`SCC_USEROPT_CHECKOUT_LOCALVER`|ユーザーがローカルバージョンのファイルをチェックアウトするかどうかを指定します。 `lpVal` が割り当てられている `SCC_USEROPT_COLV_YES` (ユーザーがローカルファイルをチェックアウトする) か、または `SCC_USEROPT_COLV_NO` 。|

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [エラー コード](../extensibility/error-codes.md)
