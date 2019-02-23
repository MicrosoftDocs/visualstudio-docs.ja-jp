---
title: Find コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- edit.find
helpviewer_keywords:
- Find command
- Edit.Find command
ms.assetid: f0c705dc-2b97-423d-abbf-5584d4827208
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9cd4a50ebf4c27213d288cbab33647931c4a399d
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55953062"
---
# <a name="find-command"></a>Find コマンド
**[検索と置換]** ウィンドウの **[フォルダーを指定して検索]** タブにあるオプションのサブセットを使って、ファイルを検索します。

## <a name="syntax"></a>構文

```cmd
Edit.Find findwhat [/case] [/doc | /proc | /open | /sel]
[/markall] [/options] [/reset] [/up] [/wild | /regex] [/word]
```

## <a name="arguments"></a>引数
 `findwhat` 必須。 検索するテキスト。

## <a name="switches"></a>スイッチ
 /case または /c 省略可能。 `findwhat` 引数で指定されている語句と大文字および小文字の使い分けが正確に一致する場合にのみ、一致と見なします。

 /doc または /d 省略可能。 現現在のドキュメントだけを検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。

 /markall または /m 省略可能。 現在のドキュメント内で、検索一致項目が含まれている各行にグラフィックを配置します。

 /open または /o 省略可能。 開いているすべてのドキュメントを 1 つのドキュメントであるかのように検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。

 /options または /t 省略可能。 現在の検索オプションの設定の一覧を表示し、検索は行いません。

 /proc または /p 省略可能。 現在のプロシージャだけを検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。

 /reset または /e 省略可能。 検索オプションを既定の設定に戻し、検索は行いません。

 /sel または /s 省略可能。 現在の選択項目だけを検索します。 使用可能な検索スコープの中から 1 つだけ指定します (`/doc`、`/proc`、`/open`、または `/sel`)。

 /up または /u 省略可能。 ファイルの現在の位置からファイルの先頭に向かって検索します。 既定では、ファイルの現在位置から検索を開始し、ファイルの末尾に向かって検索されます。

 /regex または /r 省略可能。 `findwhat` 引数に含まれる定義済みの特殊文字を、リテラル文字ではなく、テキストのパターンを表す表記として使います。 正規表現文字の一覧については、「[正規表現](../../ide/using-regular-expressions-in-visual-studio.md)」をご覧ください。

 /wild または /l 省略可能。 `findwhat` 引数に含まれる定義済みの特殊文字を、文字または文字のシーケンスを表す表記として使います。

 /word または /w 省略可能。 単語全体と一致するもののみを検索します。

## <a name="example"></a>例
 次の例では、現在選択されているコード セクションで、"somestring" という語を、大文字と小文字を区別して検索します。

```cmd
>Edit.Find somestring /sel /case
```

## <a name="see-also"></a>関連項目

- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)