---
title: QUERYCHANGESFUNC | Microsoft Docs
description: QUERYCHANGESFUNC コールバック関数は、ファイル名のコレクションを列挙し、各ファイルの状態を判断するために使用されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- QUERYCHANGESFUNC
helpviewer_keywords:
- QUERYCHANGESFUNC callback function
- QUERYCHANGESDATA structure
ms.assetid: 9d383e2c-eee1-4996-973a-0652d4c5951c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b061fbfb6644f77348574020c0a5cb614691ae6b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899135"
---
# <a name="querychangesfunc"></a>QUERYCHANGESFUNC
これは、ファイル名のコレクションを列挙し、各ファイルの状態を判断するために [SccQueryChanges](../extensibility/sccquerychanges-function.md) 操作で使用されるコールバック関数です。

 `SccQueryChanges` 関数には、ファイルの一覧と `QUERYCHANGESFUNC` コールバックへのポインターが指定されます。 ソース管理プラグインにより、指定された一覧が列挙され、(このコールバックを介して) 一覧内の各ファイルの状態が表示されます。

## <a name="signature"></a>署名

```cpp
typedef BOOL (*QUERYCHANGESFUNC)(
   LPVOID pvCallerData,
   QUERYCHANGESDATA * pChangesData
);
```

## <a name="parameters"></a>パラメーター
 pvCallerData

[入力] 呼び出し元 (IDE) から [SccQueryChanges](../extensibility/sccquerychanges-function.md) に渡される `pvCallerData` パラメーター。 ソース管理プラグイン側では、この値の内容について何も想定しないでください。

 pChangesData

[入力] ファイルへの変更を記述する [QUERYCHANGESDATA 構造体](#LinkQUERYCHANGESDATA)構造体へのポインター。

## <a name="return-value"></a>戻り値
 IDE によって適切なエラー コードが返されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|処理し続けます。|
|SCC_I_OPERATIONCANCELED|処理を停止します。|
|SCC_E_xxx|適切な SCC エラーが発生すると、処理が停止します。|

## <a name="querychangesdata-structure"></a><a name="LinkQUERYCHANGESDATA"></a> QUERYCHANGESDATA 構造体
 各ファイルに渡される構造体は、次のようになります。

```cpp
struct QUERYCHANGESDATA_A
{
    DWORD  dwSize;
    LPCSTR lpFileName;
    DWORD  dwChangeType;
    LPCSTR lpLatestName;
};

typedef struct QUERYCHANGESDATA_A QUERYCHANGESDATA;

struct QUERYCHANGESDATA_W
{
    DWORD   dwSize;
    LPCWSTR lpFileName;
    DWORD   dwChangeType;
    LPCWSTR lpLatestName;
};
```

 この構造体の dwSize サイズ (バイト単位)。

 lpFileName: この項目の元のファイル名。

 ファイルの状態を示す dwChangeType コード:

|コード|説明|
|----------|-----------------|
|`SCC_CHANGE_UNKNOWN`|変更内容を識別できません。|
|`SCC_CHANGE_UNCHANGED`|このファイルの名前は変更されません。|
|`SCC_CHANGE_DIFFERENT`|データベース内に、ID は異なりますが、同じ名前のファイルが存在します。|
|`SCC_CHANGE_NONEXISTENT`|ファイルはデータベース内にもローカルにも存在しません。|
|`SCC_CHANGE_DATABASE_DELETED`|データベース内のファイルは削除されました。|
|`SCC_CHANGE_LOCAL_DELETED`|ローカルでファイルは削除されましたが、データベース内にはまだファイルが存在します。 これを判断できない場合は、`SCC_CHANGE_DATABASE_ADDED` を返します。|
|`SCC_CHANGE_DATABASE_ADDED`|ファイルはデータベースに追加されましたが、ローカルには存在しません。|
|`SCC_CHANGE_LOCAL_ADDED`|ファイルはデータベース内に存在せず、新しいローカル ファイルです。|
|`SCC_CHANGE_RENAMED_TO`|データベース内のファイル名は `lpLatestName` に変更されたか、移動されました。|
|`SCC_CHANGE_RENAMED_FROM`|データベース内のファイル名は `lpLatestName` から変更されたか、移動されました。この追跡にコストがかかりすぎる場合は、`SCC_CHANGE_DATABASE_ADDED` などの別のフラグを返します。|

 lpLatestName: この項目の現在のファイル名。

## <a name="see-also"></a>こちらもご覧ください
- [IDE で実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccQueryChanges](../extensibility/sccquerychanges-function.md)
- [エラー コード](../extensibility/error-codes.md)
