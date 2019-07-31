---
title: 右端で折り返す
ms.date: 11/07/2018
ms.topic: conceptual
helpviewer_keywords:
- word wrap
- editors, text viewing
- Code Editor, word wrap
ms.assetid: 442f33ef-9f52-4515-b55f-fb816d664645
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bdf19530461d52523bc581835e14fcaabe0e9a76
ms.sourcegitcommit: ce1ab8a25c66a83e60eab80ed8e1596fe66dd85c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2019
ms.locfileid: "68605431"
---
# <a name="how-to-manage-word-wrap-in-the-editor"></a>方法: エディターのワード ラップを管理する

**[右端で折り返す]** オプションを設定および解除できます。 このオプションを設定すると、コード エディター ウィンドウの現在の幅からはみ出した長い行の部分は次の行に表示されます。 たとえば行番号の使用を容易にするためにこのオプションをオフにすると、右にスクロールして長い行の末尾を表示できます。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio にのみ適用されます。 現在、Visual Studio for Mac はワード ラップをサポートしていません。

## <a name="to-set-word-wrap-preferences"></a>ワード ラップ オプションを設定するには

1. **[ツール]** メニューの **[オプション]** を選択します。

2. **[テキスト エディター]** フォルダーで、 **[すべての言語]** サブフォルダーの **[全般]** オプションを選択して、このオプションをグローバルに設定します。

     または

     プログラミングしている言語のサブフォルダーの **[全般]** オプションを選択します。

3. **[設定]** で、 **[右端で折り返す]** オプションをオンまたはオフにします。

     **[右端で折り返す]** オプションをオンにすると、 **[右端の折り返しの記号を表示する]** オプションが有効になります。

4. 長い行が 2 行目に折り返される場合に改行インジケーターを表示するには、 **[折り返しの記号を表示する]** オプションをオンにします。 このオプションをオフにすると、インジケーターは表示されません。

    > [!NOTE]
    > 改行インジケーターはコードには追加されません。表示専用です。

## <a name="known-issues"></a>既知の問題

Notepad++、Sublime Text、Visual Studio Code での行の折り返しに慣れている場合は、Visual Studio の動作が他のエディターと異なる場合の次の問題に注意してください。

* [トリプル クリックで行全体が選択されない](https://developercommunity.visualstudio.com/content/problem/268989/triple-click-doesnt-select-whole-line-when-word-wr.html)
* [切り取りコマンドで行全体が削除されない](https://developercommunity.visualstudio.com/content/problem/138259/cut-command-should-delete-logical-line.html)
* [End キーを 2 回押してもカーソルが行末に移動しない](https://developercommunity.visualstudio.com/content/problem/138274/pressing-end-key-twice-should-move-cursor-to-end-o.html)

## <a name="see-also"></a>関連項目

- [コード エディターの機能](../../ide/writing-code-in-the-code-and-text-editor.md)
