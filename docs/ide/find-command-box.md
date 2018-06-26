---
title: '[検索/コマンド] ボックス'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.findcommandbox
helpviewer_keywords:
- Find/Command box
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c5e11d83ea0c87bae058f5421c424922fa389a9c
ms.sourcegitcommit: 58052c29fc61c9a1ca55a64a63a7fdcde34668a4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34752412"
---
# <a name="findcommand-box"></a>[検索/コマンド] ボックス

**[検索]** ボックスでは、テキストを検索し、Visual Studio コマンドを検索できます。 **[検索]** ボックスは、ツール バー コントロールとして使用できますが、既定では表示されません。 **[標準]** ツール バーの **[ボタンの追加または削除]** を選択し、**[検索]** を選択すると、**[検索]** ボックスを表示できます。

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] コマンドを実行するには、コマンドの先頭に不等号 (**>**) を付けます。

**[検索]** ボックスでは、最近入力した 20 個のアイテムが記憶され、ドロップダウン リストに表示されます。 **方向キー**を選択すると、一覧を参照できます。

![[検索&#47;コマンド] ボックス](../ide/media/findcommandbox.png)

## <a name="searching-for-text"></a>テキストの検索

既定では、**[検索]** ボックスにテキストを指定して **Enter** キーを押すと、Visual Studio によって、**[フォルダーを指定して検索]** ダイアログ ボックスで指定したオプションが使用され、現在のドキュメント ウィンドウまたはツール ウィンドウで検索されます。 詳細については、「[テキストの検索と置換](../ide/finding-and-replacing-text.md)」を参照してください。

## <a name="entering-commands"></a>コマンドの入力

**[検索]** ボックスを使用して、文字列の検索ではなく、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の単一のコマンドまたはエイリアスを実行するには、コマンドの先頭に不等号 (**>**) を付けます。 例:

```
>File.NewFile c:\temp\MyFile /t:"General\Text File"
```

または、**コマンド** ウィンドウを使って、単一または複数のコマンドを入力して実行することもできます。 コマンドまたはエイリアスには、単独で入力して実行できるものと、構文に引数の指定が必要なものがあります。 引数を持つコマンドの一覧については、「[Visual Studio コマンド](../ide/reference/visual-studio-commands.md)」をご覧ください。

## <a name="escape-characters"></a>エスケープ文字

コマンドにカレット (**^**) 文字があると、その直後の文字は制御文字としてではなくリテラル文字として解釈されます。 したがって、引用符 (**"**)、スペース、先頭のスラッシュ、カレット、その他の任意のリテラル文字をパラメーターまたはスイッチの値に直接埋め込むことができます。ただし、スイッチ名には埋め込むことができません。 例:

```
>Edit.Find ^^t /regex
```

カレットは、引用符の前後のどちらに置かれた場合でも同じ働きをします。 行の最後の文字がカレットの場合は無視されます。

## <a name="see-also"></a>関連項目

- [コマンド ウィンドウ](../ide/reference/command-window.md)
- [テキストの検索と置換](../ide/finding-and-replacing-text.md)