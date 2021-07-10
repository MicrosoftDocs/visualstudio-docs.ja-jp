---
title: '[ソリューション エクスプローラー] ツール ウィンドウについて説明します'
description: Visual Studio で [ソリューション エクスプローラー] ツール ウィンドウを使用して、ファイル、プロジェクト、ソリューションを作成および管理する方法について説明します。
ms.date: 06/29/2021
ms.topic: conceptual
f1_keywords:
- vs.addnewitem
helpviewer_keywords:
- solution explorer [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: fbbae8b974a7e88abffd9a12eb253dfea6c7165b
ms.sourcegitcommit: 8fb1500acb7e6314fbb6b78eada78ef5d61d39bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2021
ms.locfileid: "113280490"
---
# <a name="how-to-use-solution-explorer"></a>ソリューション エクスプローラーの使用方法

[ソリューション エクスプローラー] ツール ウィンドウを使用して、ソリューションとプロジェクトを作成および管理し、コードを表示および操作することができます。 この記事では、そのためのユーザー インターフェイス (UI) オプションについて詳しく説明します。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio にのみ適用されます。

## <a name="solution-explorer-tool-window"></a>[ソリューション エクスプローラー] ツール ウィンドウ

まず、[Visual Studio IDE](../get-started/visual-studio-ide.md) の[ソリューション エクスプローラー] ツール ウィンドウを見てみましょう。ここでは、2 つのプロジェクトを持つ C# コンソール ソリューションを開いています。

[![Visual Studio の [ソリューション エクスプローラー] ツール ウィンドウ。](media/solution-explorer-tool-window.png)](media/solution-explorer-tool-window.png#lightbox)

ツール ウィンドウには、次の UI (ユーザー インターフェイス) 要素があります。

- **メニュー バー**: ファイルの表示方法を制御できます
- **検索バー**: 特定のファイルとファイルの種類を検索することができます
- **メイン ウィンドウ**: ファイル、プロジェクト、ソリューションを表示および管理できます。
- **ソリューション ノード**: ソリューションを管理できます
- **プロジェクト ノード**: 自分のプロジェクトを管理することができます
- **依存関係ノード**: ソリューションとプロジェクトの依存関係を管理できます
- **プログラム ノード**: プログラムまたはアプリケーション (アプリ) を表示、編集、および管理できます
- **[ タブ](../version-control/git-with-visual-studio.md?view=vs-2019&preserve-view=true#git-changes-window)** : Visual Studio 内で Git と GitHub を使用してプロジェクトについてチームと共同作業することができます。

> [!TIP]
> [ソリューション エクスプローラー] ツール ウィンドウが表示されていない場合は、Visual Studio のメニュー バーから **[表示]**  >  **[ソリューション エクスプローラー]** を使用するか、**Ctrl**+**Alt**+**L** キーを押して開くことができます。

## <a name="solution-explorer-menu-bar"></a>[ソリューション エクスプローラー] メニュー バー

次は、[ソリューション エクスプローラー] メニュー バーを詳しく見てみましょう。

![Visual Studio の [ソリューション エクスプローラー] メニュー バー。](media/solution-explorer-menu-bar.png)

メニュー バーには、左から順に以下の UI 要素があります。

- **[戻る]** ボタン: 検索結果を切り替えます
- **[進む]** ボタン: 検索結果を切り替えます
- **[ホーム]** ボタン: 既定のビューに戻ります
- **[切り替え]** ボタン: ソリューションと使用可能なビューを切り替えます
- **[保留中の変更フィルター]** ボタンとドロップダウン メニュー: 開いているファイルや変更が保留されているファイルを表示します
- **[アクティブ ドキュメントとの同期]** ボタン: コード エディターからファイルを検索します
- **[最新の情報に更新]** ボタン: 関数やパッケージなどの依存関係を選択したときにのみ表示されます
- **[すべて折りたたむ]** ボタン: メイン ウィンドウのファイル ビューを折りたたみます
- **[すべてのファイルを表示]** ボタン: [アンロードされたプロジェクト](filtered-solutions.md#toggle-unloaded-project-visibility)を含むすべてのファイルを表示します。
- **[プロパティ]** ボタン: 特定のファイルとコンポーネントの設定を表示および変更します。
- **[選択された項目のプレビュー]** ボタン: 選択されたファイルまたはコンポーネントをコード エディターで表示します。

### <a name="solution-explorer-right-click-context-menu"></a>ソリューション エクスプローラーの右クリック コンテキスト メニュー

ソリューション エクスプローラーには、右クリック コンテキスト メニューを使用して操作できるファイルのプロパティがいくつかあります。 右クリック コンテキスト メニューのオプションの詳細については、「[プロジェクトおよびソリューションのプロパティの管理](managing-project-and-solution-properties.md)」ページを参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio のソリューションおよびプロジェクト](solutions-and-projects-in-visual-studio.md)
- [Visual Studio のウィンドウ レイアウトをカスタマイズする](customizing-window-layouts-in-visual-studio.md)
