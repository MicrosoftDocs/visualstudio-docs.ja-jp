---
description: この関数は、以前にチェックアウトされたファイルをソース管理システムにチェックインし、変更内容を保存し、新しいバージョンを作成します。
title: SccCheckin 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccCheckin
helpviewer_keywords:
- SccCheckin function
ms.assetid: e3f26ac2-6163-42e1-a764-22cfea5a3bc6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d6864549c6825092b6ad26be199f8c7b5ea6bab6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060433"
---
# <a name="scccheckin-function"></a>SccCheckin 関数
この関数は、以前にチェックアウトされたファイルをソース管理システムにチェックインし、変更内容を保存し、新しいバージョンを作成します。 この関数は、チェックインするファイルの数と、名前の配列を使用して呼び出されます。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccCheckin (
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPSTR*    lpFileNames,
   LPCSTR    lpComment,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] SCC プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 nFiles

[入力] チェックイン対象として選択されたファイルの数。

 lpFileNames

[入力] チェックインするファイルの完全修飾ローカル パス名の配列。

 lpComment

[入力] チェックインされる選択された各ファイルに適用されるコメント。 ソース管理プラグインによってコメントが求められる場合、このパラメーターは `NULL` です。

 fOptions

[入力] コマンドのフラグ (0 または `SCC_KEEP_CHECKEDOUT`)。

 pvOptions

[入力] SCC プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装は、次のいずれかの値を返すことが期待されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|ファイルは正常にチェックインされました。|
|SCC_E_FILENOTCONTROLLED|選択したファイルはソース コード管理下にありません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題が原因になっている可能性があります。 再試行することをお勧めします。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。 ファイルはチェックインされていません。|
|SCC_E_NOTCHECKEDOUT|ユーザーがファイルをチェックアウトしていないので、チェックインできません。|
|SCC_E_CHECKINCONFLICT|次の理由により、チェックインを行うことができませんでした。<br /><br /> -   他のユーザーが既にチェックインしており、`bAutoReconcile` が false でした。<br /><br /> または<br /><br /> -   自動マージを行うことができません (ファイルがバイナリの場合など)。|
|SCC_E_VERIFYMERGE|ファイルは自動マージされましたが、ユーザーの検証が保留中であり、チェックインされていません。|
|SCC_E_FIXMERGE|ファイルは自動マージされましたが、手動で解決する必要があるマージの競合のためにチェックインされませんでした。|
|SCC_E_NOTAUTHORIZED|ユーザーには、この操作の実行が許可されていません。|
|SCC_I_OPERATIONCANCELED|操作が完了前にキャンセルされました。|
|SCC_I_RELOADFILE|ファイルまたはプロジェクトを再度読み込む必要があります。|
|SCC_E_FILENOTEXIST|ローカル ファイルが見つかりませんでした。|

## <a name="remarks"></a>解説
 コメントは、チェックインされるすべてのファイルに適用されます。 コメント引数として `null` 文字列を使用できます。その場合、ソース管理プラグインは、各ファイルのコメント文字列をユーザーに求めることができます。

 ファイルをチェックインしてから再度チェックアウトするというユーザーの意図を指定するには、`fOptions` 引数に `SCC_KEEP_CHECKEDOUT` フラグの値を指定することができます。

## <a name="see-also"></a>こちらもご覧ください
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
