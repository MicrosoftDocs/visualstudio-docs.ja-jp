---
description: この関数は、ソース管理下にある選択された一連のファイルの状態情報を取得します。
title: SccQueryInfo 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccQueryInfo
helpviewer_keywords:
- SccQueryInfo function
ms.assetid: 3973d336-a9b7-41a2-a4e6-bb8184a96aaf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 911219605859025f1877d040b5932714b10f836a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073899"
---
# <a name="sccqueryinfo-function"></a>SccQueryInfo 関数
この関数は、ソース管理下にある選択された一連のファイルの状態情報を取得します。

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

[入力] ソース管理プラグインのコンテキスト構造体。

 nFiles

[入力] `lpFileNames` 配列で指定されているファイルの数および `lpStatus` 配列の長さ。

 lpFileNames

[入力] クエリ対象のファイルの名前の配列。

 lpStatus

[入力、出力] ソース管理プラグインが各ファイルの状態フラグを返す配列。 詳細については、[ファイルの状態コード](../extensibility/file-status-code-enumerator.md)に関するページを参照してください。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値を返すことが想定されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|クエリに成功しました。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセスで問題が発生しました。ネットワークまたは競合の問題が原因になっている可能性があります。 再試行することをお勧めします。|
|SCC_E_PROJNOTOPEN|プロジェクトがソース管理下で開かれていません。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。|

## <a name="remarks"></a>解説
 `lpFileName` が空の文字列の場合、現在更新する状態情報はありません。 それ以外の場合は、状態情報が変更された可能性があるファイルの完全なパス名です。

 戻り値の配列では、`SCC_STATUS_xxxx` ビットのビットマスクを指定できます。 詳細については、[ファイルの状態コード](../extensibility/file-status-code-enumerator.md)に関するページを参照してください。 ソース管理システムで、一部のビット型がサポートされていない場合があります。 たとえば、`SCC_STATUS_OUTOFDATE` が提供されていない場合、ビットは設定されません。

 この関数を使用してファイルをチェックアウトする場合は、次の `MSSCCI` 状態要件に注意してください。

- `SCC_STATUS_OUTBYUSER` は、現在のユーザーがファイルをチェックアウトしたときに設定されます。

- `SCC_STATUS_CHECKEDOUT` は、`SCC_STATUS_OUTBYUSER` が設定されていない場合は設定できません。

- `SCC_STATUS_CHECKEDOUT` は、指定された作業ディレクトリにファイルがチェックアウトされている場合にのみ設定されます。

- ファイルが現在のユーザーによって作業ディレクトリ以外のディレクトリにチェックアウトされている場合、`SCC_STATUS_OUTBYUSER` は設定されますが、`SCC_STATUS_CHECKEDOUT` は設定されません。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [ファイルの状態コード](../extensibility/file-status-code-enumerator.md)
