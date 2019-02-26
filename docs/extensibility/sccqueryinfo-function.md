---
title: SccQueryInfo 関数 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccQueryInfo
helpviewer_keywords:
- SccQueryInfo function
ms.assetid: 3973d336-a9b7-41a2-a4e6-bb8184a96aaf
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e01c76f5696e029cd7d15be75786b1009af4a673
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56678632"
---
# <a name="sccqueryinfo-function"></a>SccQueryInfo 関数
この関数は、一連のソース管理下で選択したファイルの状態情報を取得します。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccQueryInfo(
   LPVOID  pvContext,
   LONG    nFiles,
   LPCSTR* lpFileNames,
   LPLONG  lpStatus
);
```

#### <a name="parameters"></a>パラメーター
 pvContext

[in]ソース管理プラグイン コンテキスト構造体。

 nFiles

[in]指定されたファイルの数、`lpFileNames`配列との長さ、`lpStatus`配列。

 lpFileNames

[in]クエリを実行するファイルの名前の配列。

 lpStatus

[入力、出力]配列をソース管理プラグインは各ファイルの状態フラグを返します。 詳細については、次を参照してください。[ファイルの状態コード](../extensibility/file-status-code-enumerator.md)します。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグイン実装は、次の値のいずれかを返すが必要です。

|[値]|説明|
|-----------|-----------------|
|SCC_OK|クエリが正常に完了しました。|
|SCC_E_ACCESSFAILURE|ソース管理システム、ネットワークまたは競合の問題である可能性のアクセスに問題が発生しました。 再試行をお勧めします。|
|SCC_E_PROJNOTOPEN|プロジェクトでは、ソース管理下にある開いていません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>Remarks
 場合`lpFileName`は空の文字列を更新するステータス情報は現在ありません。 それ以外の場合、状態情報の変更を可能性がありますが、ファイルの完全なパス名になります。

 戻り値の配列は、ビットマスクの`SCC_STATUS_xxxx`ビット。 詳細については、次を参照してください。[ファイルの状態コード](../extensibility/file-status-code-enumerator.md)します。 ソース管理システムはすべてのビットの種類をサポートしていません。 たとえば場合、`SCC_STATUS_OUTOFDATE`が提供されていない、ビットが設定されていないだけです。

 ファイルをチェック アウトをこの関数を使用する場合は、次に注意してください`MSSCCI`状態の要件。

-   `SCC_STATUS_OUTBYUSER` 現在のユーザーがチェック アウトするファイルと設定されます。

-   `SCC_STATUS_CHECKEDOUT` 設定できません`SCC_STATUS_OUTBYUSER`設定されます。

-   `SCC_STATUS_CHECKEDOUT` ときに、ファイルがチェック アウトを指定された作業ディレクトリにのみ設定されます。

-   ファイルがチェック アウトされて現在のユーザーが、作業ディレクトリ以外のディレクトリに場合、`SCC_STATUS_OUTBYUSER`設定されているが、`SCC_STATUS_CHECKEDOUT`はありません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [ファイルの状態コード](../extensibility/file-status-code-enumerator.md)