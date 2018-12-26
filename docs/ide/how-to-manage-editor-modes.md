---
title: 全画面表示と仮想空白モード
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- word wrap
- views, virtual space
- line numbers, displaying
- virtual space mode
- line numbers
- Code Editor, view and display options
- full screen mode
- Code Editor, modes
- views, splitting
- views, word wrapping
- fonts and size
- views, creating new windows
- views, line numbers
- views, changing mode
- views, outlining
ms.assetid: 1fb48027-d870-439f-8b72-4a0321390748
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e5250176bee4993f9d01bffcaed71579c17e55c9
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2018
ms.locfileid: "53056309"
---
# <a name="how-to-manage-editor-modes"></a>方法: エディター モードを管理する

Visual Studio のコード エディターは、さまざまな表示モードで表示できます。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、この記事の説明と異なる場合があります。 設定を、たとえば、**[全般]** や **[Visual C++]** に変更するには、**[ツール]**、**[設定のインポートとエクスポート]**、**[すべての設定をリセット]** の順に選択します。

## <a name="enable-full-screen-mode"></a>全画面表示モードを有効にする

**全画面表示**モードを有効にすると、すべてのツール ウィンドウを非表示にして、ドキュメント ウィンドウだけを表示することができます。

-   **全画面表示**モードを開始または終了するには、**Alt**+**Shift**+**Enter** キーを押します。

     または

-   **[コマンド]** ウィンドウで `View.Fullscreen` コマンドを実行します。

## <a name="enable-virtual-space-mode"></a>仮想空白モードを有効にする

**仮想空白**モードでは、各コード行の末尾に空白が挿入されます。 コードの横に一貫してコメントを入れる場合は、このチェック ボックスをオンにします。

1.  **[ツール]** メニューの **[オプション]** を選択します。

2.  **[テキスト エディター]** フォルダーを展開し、**[すべての言語]** を選択してこのオプションをグローバルに設定するか、または特定の言語フォルダーを選択します  たとえば、Visual Basic でのみ行番号を表示するには、**[Basic]** > **[テキスト エディター]** ノードを選択します。

3.  **[全般]** オプションを選択し、**[設定]** で **[仮想空白文字を使用]** を選択します。

    > [!NOTE]
    > **列の選択**モードで**仮想空白文字**が有効になります。 **仮想空白**モードを有効にしないと、挿入ポイントは行の末尾から次の行の先頭文字に直接移動します。

## <a name="see-also"></a>関連項目

- [エディターのカスタマイズ](../ide/customizing-the-editor.md)
- [Visual Studio のウィンドウ レイアウトをカスタマイズする](../ide/customizing-window-layouts-in-visual-studio.md)
- [[フォントおよび色] ([オプション] ダイアログ ボックス - [環境])](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)