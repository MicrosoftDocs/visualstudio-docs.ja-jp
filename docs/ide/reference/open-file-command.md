---
title: OpenFile コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- file.openfile
helpviewer_keywords:
- Open File command
- File.OpenFile command
- of command
ms.assetid: a51a83fc-e3c6-4fa2-8882-8b7b6c0a6406
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b76db52534f4c264e065152548d49f9773863a29
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62995235"
---
# <a name="open-file-command"></a>Openfile コマンド

既存のファイルを開き、エディターを指定できます。

## <a name="syntax"></a>構文

```cmd
File.OpenFile filename [/e:editorname]
```

## <a name="arguments"></a>引数

`filename`

必須です。 開くファイルの完全パスまたは部分パス、およびファイル名。 パスに空白が含まれる場合は、引用符で囲む必要があります。

## <a name="switches"></a>スイッチ

/e:`editorname`

任意。 ファイルを開くために使用するエディターの名前です。 引数は指定されていても、エディター名がない場合、**[プログラムから開く]** ダイアログ ボックスが表示されます。

/e:`editorname` 引数の構文では、[ファイルを開くアプリケーションの選択] ダイアログ ボックスで表示されるようにエディター名を入力し、引用符で囲みます。

たとえば、ソース コード エディターでファイルを開くには、/e:`editorname` 引数に対して次のように入力します。

```cmd
/e:"Source Code (text) Editor"
```

## <a name="remarks"></a>解説

パスを入力する場合、オート コンプリートによって正しいパス名とファイル名が検索されます。

## <a name="example"></a>例

次の例では、スタイル ファイル "Test1.css" をソース コード エディターで開きます。

```cmd
>File.OpenFile "C:\My Projects\project1\Test1.css" /e:"Source Code (text) Editor"
```

## <a name="see-also"></a>関連項目

- [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [イミディエイト ウィンドウ](../../ide/reference/immediate-window.md)
- [[検索/コマンド] ボックス](../../ide/find-command-box.md)
- [Visual Studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)