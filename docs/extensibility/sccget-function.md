---
description: この関数により、表示とコンパイル用の 1 つ以上のファイルのコピーが取得されますが、編集用はされません。
title: SccGet 関数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- SccGet
helpviewer_keywords:
- SccGet function
ms.assetid: 09a18bd2-b788-411a-9da6-067d806e46f6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 172e0ec5fdba4b91c3cf86ea964b4a98a23a5fa8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060342"
---
# <a name="sccget-function"></a>SccGet 関数
この関数により、表示とコンパイル用の 1 つ以上のファイルのコピーが取得されますが、編集用はされません。 ほとんどのシステムでは、ファイルは読み取り専用としてタグ付けされています。

## <a name="syntax"></a>構文

```cpp
SCCRTN SccGet(
   LPVOID    pvContext,
   HWND      hWnd,
   LONG      nFiles,
   LPCSTR*   lpFileNames,
   LONG      fOptions,
   LPCMDOPTS pvOptions
);
```

### <a name="parameters"></a>パラメーター
 pvContext

[入力] ソース管理プラグインのコンテキスト構造体。

 hWnd

[入力] ソース管理プラグインが、提供するすべてのダイアログ ボックスの親として使用できる IDE ウィンドウへのハンドル。

 nFiles

[入力] `lpFileNames` 配列で指定されているファイルの数。

 lpFileNames

[入力] 取得するファイルの完全修飾名の配列。

 fOptions

[入力] コマンド フラグ (`SCC_GET_ALL`、`SCC_GET_RECURSIVE`)。

 pvOptions

[入力] ソース管理プラグイン固有のオプション。

## <a name="return-value"></a>戻り値
 この関数のソース管理プラグインの実装では、次のいずれかの値を返すことが想定されます。

|値|説明|
|-----------|-----------------|
|SCC_OK|取得操作が成功しました。|
|SCC_E_FILENOTCONTROLLED|ファイルはソース管理されていません。|
|SCC_E_OPNOTSUPPORTED|ソース管理システムでは、この操作はサポートされていません。|
|SCC_E_FILEISCHECKEDOUT|ユーザーが現在チェックアウトしているファイルを取得できません。|
|SCC_E_ACCESSFAILURE|ソース管理システムへのアクセス中に問題が発生しました。ネットワークまたは競合の問題である可能性があります。 再試行することをお勧めします。|
|SCC_E_NOSPECIFIEDVERSION|無効なバージョン、日付または時刻が指定されました。|
|SCC_E_NONSPECIFICERROR|不特定のエラーです。ファイルは同期されませんでした。|
|SCC_I_OPERATIONCANCELED|操作が完了する前にキャンセルされました。|
|SCC_E_NOTAUTHORIZED|ユーザーにはこの操作を実行する権限がありません。|

## <a name="remarks"></a>解説
 この関数は、カウントと、取得するファイルの名前の配列を使用して呼び出されます。 IDE からフラグ `SCC_GET_ALL` が渡された場合、`lpFileNames` 内の項目はファイルではなくディレクトリであり、所与のディレクトリ内のソース管理下にあるすべてのファイルが取得されることを意味します。

 `SCC_GET_ALL` フラグを `SCC_GET_RECURSIVE` フラグと組み合わせて、指定したディレクトリとすべてのサブディレクトリ内のすべてのファイルを取得することもできます。

> [!NOTE]
> 決して `SCC_GET_ALL` を指定せずに `SCC_GET_RECURSIVE` を渡すべきではありません。 また、ディレクトリ *C:\A* と *C:\A\B* の両方が再帰的 Get で渡される場合、*C:\A\B* とそのすべてのサブディレクトリは、実際に 2 回取得されることに注意してください。 このような重複が配列から確実に除かれるようにするのは、ソース管理プラグインではなく、IDE の責任です。

 最後に、ソース管理プラグインで初期化時に `SCC_CAP_GET_NOUI` フラグが指定されており、Get コマンドのユーザー インターフェイスがないことを示す場合でも、ファイルを取得するために IDE によってこの関数が呼び出されることがあります。 フラグは、単に IDE に [Get] メニュー項目が表示されず、プラグインから UI が提供されないことが予想されることを意味します。

## <a name="rename-files-and-sccget"></a>ファイルとディレクトリの名前を変更する
 状況: ユーザーがファイル (*a.txt* など) をチェックアウトし、変更します。 *a.txt* をチェックインできるようになる前に、2 番目のユーザーが *a.txt* の名前をソース管理データベースで *b.txt* に変更し、*b.txt* をチェックアウトして、ファイルに何らかの変更を加え、ファイルをチェックインしました。 最初のユーザーは、2 番目のユーザーによって行われた変更を必要とします。そのため、最初のユーザーは *a.txt* ファイルのローカル バージョンの名前を *b.txt* に変更し、ファイルに対して Get を実行します。 ただし、バージョン番号を追跡するローカル キャッシュでは、*a.txt* の最初のバージョンがローカルに格納されていると判断されるため、ソース管理では相違点を解決できません。

 ソース管理のバージョンのローカル キャッシュがソース管理データベースと同期しなくなる状況を解決するには、次の 2 つの方法があります。

1. 現在チェックアウトされているソース管理データベース内のファイルの名前の変更を許可しません。

2. "古いものを削除" の後に "新しいものを追加" と同様のことを実行します。 次のアルゴリズムは、これを実現する方法の 1 つです。

    1. [SccQueryChanges](../extensibility/sccquerychanges-function.md) 関数を呼び出して、ソース管理データベース内で *a.txt* から *b.txt* への名前変更について把握します。

    2. ローカルの *a.txt* の名前を *b.txt* に変更します。

    3. *a.txt* と *b.txt* の両方に対して `SccGet` 関数を呼び出します。

    4. ソース管理データベースには *a.txt* が存在しないため、ローカル バージョンのキャッシュでは、欠如している *a.txt* バージョン情報が削除されます。

    5. チェックアウトされている *b.txt* ファイルは、ローカル *b.txt* ファイルの内容とマージされます。

    6. 更新された *b.txt* ファイルをチェックインできるようになりました。

## <a name="see-also"></a>関連項目
- [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
- [特定のコマンドで使用されるビットフラグ](../extensibility/bitflags-used-by-specific-commands.md)
