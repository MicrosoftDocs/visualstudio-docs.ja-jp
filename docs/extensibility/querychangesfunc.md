---
title: QUERYCHANGESFUNC |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- QUERYCHANGESFUNC
helpviewer_keywords:
- QUERYCHANGESFUNC callback function
- QUERYCHANGESDATA structure
ms.assetid: 9d383e2c-eee1-4996-973a-0652d4c5951c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8ac0003d26296a25659debbab3352e4e37cbf2ec
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66334399"
---
# <a name="querychangesfunc"></a>QUERYCHANGESFUNC
これで使用されるコールバック関数、 [SccQueryChanges](../extensibility/sccquerychanges-function.md)操作をファイル名のコレクションを列挙し、各ファイルの状態を確認します。

 `SccQueryChanges`関数ポインター、およびファイルの一覧を指定、`QUERYCHANGESFUNC`コールバック。 ソース管理プラグインは、指定されたリストを列挙し、一覧内の各ファイル (このコールバック) を使用して状態を提供します。

## <a name="signature"></a>署名

```cpp
typedef BOOL (*QUERYCHANGESFUNC)(
   LPVOID pvCallerData,
   QUERYCHANGESDATA * pChangesData
);
```

## <a name="parameters"></a>パラメーター
 pvCallerData

[in]`pvCallerData`に呼び出し元 (IDE) によって渡されるパラメーター [SccQueryChanges](../extensibility/sccquerychanges-function.md)します。 ソース管理プラグインには、この値のコンテンツに関する仮定は行いません。

 pChangesData

[in]ポインターを[QUERYCHANGESDATA 構造](#LinkQUERYCHANGESDATA)ファイルに対する変更を記述する構造体。

## <a name="return-value"></a>戻り値
 IDE には、適切なエラー コードが返されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|処理を続行します。|
|SCC_I_OPERATIONCANCELED|処理を停止します。|
|SCC_E_xxx|適切な SCC エラーは、処理を停止する必要があります。|

## <a name="LinkQUERYCHANGESDATA"></a> QUERYCHANGESDATA 構造体
 各ファイルに渡された構造体は、次のようになります。

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

 この構造体をバイト単位でのサイズでない dwSize します。

 lpFileName この項目の元のファイル名。

 dwChangeType ファイルのコードを示す状態。

|コード|説明|
|----------|-----------------|
|`SCC_CHANGE_UNKNOWN`|変更内容を見分けることはできません。|
|`SCC_CHANGE_UNCHANGED`|このファイルの名前が変更されていません。|
|`SCC_CHANGE_DIFFERENT`|別の id を持つファイルがデータベースに同じ名前が存在します。|
|`SCC_CHANGE_NONEXISTENT`|データベース内、またはローカル ファイルは存在しません。|
|`SCC_CHANGE_DATABASE_DELETED`|ファイルは、データベースで削除します。|
|`SCC_CHANGE_LOCAL_DELETED`|ファイルがローカルで削除されましたが、ファイルは、まだデータベースに存在します。 これを特定できない場合に返す`SCC_CHANGE_DATABASE_ADDED`します。|
|`SCC_CHANGE_DATABASE_ADDED`|ファイルは、データベースに追加しますが、ローカルに存在しません。|
|`SCC_CHANGE_LOCAL_ADDED`|ファイルはデータベースに存在しません、新しいローカル ファイルです。|
|`SCC_CHANGE_RENAMED_TO`|ファイルの名前を変更またはとデータベースに移動`lpLatestName`します。|
|`SCC_CHANGE_RENAMED_FROM`|ファイルの名前を変更または内からデータベースを移動`lpLatestName`。 これは、追跡するためにコストが高すぎる場合など、さまざまなフラグを返す`SCC_CHANGE_DATABASE_ADDED`します。|

 lpLatestName この項目の現在のファイル名。

## <a name="see-also"></a>関連項目
- [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)
- [SccQueryChanges](../extensibility/sccquerychanges-function.md)
- [エラー コード](../extensibility/error-codes.md)