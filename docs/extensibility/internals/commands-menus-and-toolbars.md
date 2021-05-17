---
title: コマンド、メニュー、およびツールバー |Microsoft Docs
description: Visual Studio のコマンド、メニュー、およびツールバーについて説明します。その内容と VSPackage での動作が含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- commands [Visual Studio]
- toolbars [Visual Studio], commands
ms.assetid: 07b4ed90-dbbd-40df-b6c9-8395fd6f2ab6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2a1b4cdb95fa5b053bc75efb559ea77b84ae56dd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057157"
---
# <a name="commands-menus-and-toolbars"></a>コマンド、メニュー、およびツール バー
メニューとツールバーは、ユーザーが VSPackage 内のコマンドにアクセスする方法です。 コマンドは、ドキュメントの印刷、ビューの更新、ファイルの新規作成などのタスクを実行する関数です。 メニューとツール バーは、ユーザーにコマンドをグラフィカルに表示する便利な方法です。 通常、関連するコマンドは、同じメニューやツール バーにまとめられます。

- メニューは通常、統合開発環境 (IDE) やツール ウィンドウの上部にある列にまとめられた 1 語の文字列として表示されます。 メニューは、右クリック イベントの結果として表示することもでき、これはそのコンテキストのショートカット メニューと呼ばれます。 クリックすると、メニューが展開して 1 つ以上のコマンドが表示されます。 コマンドをクリックすると、タスクを実行したり、追加のコマンドを含むサブメニューを起動したりすることができます。 よく知られているメニュー名には、 **[ファイル]** 、 **[編集]** 、 **[表示]** 、 **[ウィンドウ]** などがあります。 詳細については、「[メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」を参照してください。

- ツール バーは通常、ボタンと他のコントロール (コンボ ボックス、リスト ボックス、テキスト ボックス、メニュー コント ローラーなど) の行です。 すべてのツール バー コントロールは、コマンドに関連付けられます。 ツール バー ボタンをクリックすると、関連付けられているコマンドがアクティブ化されます。 ツール バー ボタンには、通常、[印刷] コマンド用のプリンターなどの基になるコマンドを示すアイコンがあります。 ドロップダウン リスト コントロールでは、リスト内の各項目は、異なるコマンドに関連付けられています。 メニュー コントローラーは、コントロールの一方の側がツール バー ボタン、もう一方の側が、クリックして追加のコマンドを表示する下矢印の組み合わせです。 詳細については、「[ツール バーにメニューコントローラーを追加する](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)」を参照してください。

- コマンドを作成するときは、コマンド用のイベント ハンドラーも作成する必要があります。 イベント ハンドラーでは、コマンドをいつ表示または有効にするかを決定し、コマンドのテキストを変更し、アクティブ化したときにコマンドが適切に応答する (「ルーティングする」) ようにすることができます。 ほとんどの場合、IDE では <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを使用してコマンドを処理します。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ではコマンドは階層形式でルーティングし、ローカルの選択に基づいて最も内側のコマンド コンテキストから開始し、グローバルの選択に基づいて最も外側のコンテキストに進みます。 メイン メニューに追加したコマンドは、すぐにスクリプトに利用できます。 詳細については、「[Menucommands と OleMenuCommands に比較](/previous-versions/visualstudio/visual-studio-2015/misc/menucommands-vs-olemenucommands?preserve-view=true&view=vs-2015)」および「[選択コンテキスト オブジェクト](../../extensibility/internals/selection-context-objects.md)」を参照してください。

  新しいメニューやツール バーを定義するには、それらを Visual Studio コマンド テーブル ( *.vsct*) ファイルで記述する必要があります。 Visual Studio パッケージ テンプレートでは、このファイルが、テンプレートで選択したすべてのコマンド、ツール バー、エディターをサポートするために必要な要素と共に作成されます。 または、「[VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)」で説明されている XML スキーマを使用して、独自の *.vsct* ファイルを作成することもできます。

  *.vsct* ファイルの操作の詳細については、「[Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)」を参照してください。

  このセクションのトピックでは、VSPackage でのコマンド、メニュー、およびツールバーの動作について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 コマンド テーブル形式の仕様の詳細な説明。

- [Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

 コマンド テーブルの XML ベースの構文とコンパイラについて説明します。

- [既定のコマンド、グループ、およびツール バーの配置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)

 定義済みのコマンド、グループ、メニュー、およびツールバーについて説明します。

- [IDE 定義コマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE で使用できる定義済みのメニュー、コマンド、およびコマンド グループを指定します。

- [コマンド デザイン](../../extensibility/internals/command-design.md)

 コマンドの設計方法について説明します。

- [メニュー、ツール バー コマンドの最適化](../../extensibility/internals/optimizing-menu-and-toolbar-commands.md)

 コマンドに関するガイドラインを示します。

- [コマンドを使用可能にする](../../extensibility/internals/making-commands-available.md)

 Visual Studio でコマンドを使用できるようにする方法について説明します。

- [相互運用機能アセンブリを使用するコマンドとメニュー](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 相互運用機能アセンブリを使用するコマンドを実装する方法について説明します。

## <a name="related-sections"></a>関連項目
- [VSPackage のコマンド ルーティング](../../extensibility/internals/command-routing-in-vspackages.md)

 VSPackage のコマンド ルーティングを説明します。