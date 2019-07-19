---
title: コマンド、メニューのおよびツールバー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- commands [Visual Studio]
- toolbars [Visual Studio], commands
ms.assetid: 07b4ed90-dbbd-40df-b6c9-8395fd6f2ab6
caps.latest.revision: 61
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 337bc4de9171d2f98bf0be0068b298b7f600b979
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155840"
---
# <a name="commands-menus-and-toolbars"></a>コマンド、メニュー、およびツール バー
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

メニューとツールバーは、ユーザーが、VSPackage のコマンドにアクセスします。 コマンドは、ドキュメントの印刷、ビューの更新、ファイルの新規作成などのタスクを実行する関数です。 メニューとツール バーは、ユーザーにコマンドをグラフィカルに表示する便利な方法です。 通常、関連するコマンドは、同じメニューやツール バーにまとめられます。  
  
- メニューは通常、統合開発環境 (IDE) やツール ウィンドウの上部にある列にまとめられた 1 語の文字列として表示されます。 メニューは、右クリック イベントの結果として表示することもでき、これはそのコンテキストのショートカット メニューと呼ばれます。 クリックすると、メニューが展開して 1 つ以上のコマンドが表示されます。 コマンドをクリックすると、タスクを実行したり、追加のコマンドを含むサブメニューを起動したりすることができます。 よく知られているメニュー名には、[ファイル]、[編集]、[表示]、[ウィンドウ] などがあります。 詳細については、次を参照してください。[拡張メニューとコマンド](../../extensibility/extending-menus-and-commands.md)します。  
  
- ツール バーは通常、ボタンと他のコントロール (コンボ ボックス、リスト ボックス、テキスト ボックス、メニュー コント ローラーなど) の行です。 すべてのツール バー コントロールは、コマンドに関連付けられます。 ツール バー ボタンをクリックすると、関連付けられているコマンドがアクティブ化されます。 ツール バー ボタンには、通常、[印刷] コマンド用のプリンターなどの基になるコマンドを示すアイコンがあります。 ドロップダウン リスト コントロールでは、リスト内の各項目は、異なるコマンドに関連付けられています。 メニュー コントローラーは、コントロールの一方の側がツール バー ボタン、もう一方の側が、クリックして追加のコマンドを表示する下矢印の組み合わせです。 詳細については、次を参照してください。[ツールバーにメニュー コント ローラーの追加](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)します。  
  
- コマンドを作成するときは、コマンド用のイベント ハンドラーも作成する必要があります。 イベント ハンドラーでは、コマンドをいつ表示または有効にするかを決定し、コマンドのテキストを変更し、アクティブ化したときにコマンドが適切に応答する (「ルーティングする」) ようにすることができます。 ほとんどの場合、IDE では <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを使用してコマンドを処理します。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ではコマンドは階層形式でルーティングし、ローカルの選択に基づいて最も内側のコマンド コンテキストから開始し、グローバルの選択に基づいて最も外側のコンテキストに進みます。 メイン メニューに追加したコマンドは、すぐにスクリプトに利用できます。 詳細については、次を参照してください。 [Menucommand とします。OleMenuCommands](../../misc/menucommands-vs-olemenucommands.md)と[コンテキスト オブジェクトの選択](../../extensibility/internals/selection-context-objects.md)します。  
  
  新しいメニューやツール バーを定義するには、それらを Visual Studio コマンド テーブル (.vsct) ファイルで記述する必要があります。 Visual Studio パッケージ テンプレートでは、このファイルが、テンプレートで選択したすべてのコマンド、ツール バー、エディターをサポートするために必要な要素と共に作成されます。 または、独自の .vsct ファイルを記述する、ここで説明されている xml スキーマを使用しています。[VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)します。  
  
  .Vsct ファイルの使用の詳細については、次を参照してください。 [Visual Studio Command Table (します。Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)します。  
  
  このセクションのトピックでは、Vspackage でのコマンド、メニューのおよびツールバーのしくみについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)  
 コマンド テーブル形式の仕様の詳細な説明。  
  
 [Visual Studio Command Table (.Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)  
 XML ベースの構文およびコマンド テーブル コンパイラについて説明します。  
  
 [既定のコマンド、グループ、およびツール バーの配置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)  
 定義済みのコマンド、グループ、メニューのおよびツールバーについて説明します。  
  
 [IDE 定義コマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)  
 定義済みのメニューのコマンド、およびコマンド グループで使用できるように指定します、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE。  
  
 [コマンド デザイン](../../extensibility/internals/command-design.md)  
 コマンドを設計する方法について説明します。  
  
 [メニュー、ツール バー コマンドの最適化](../../extensibility/internals/optimizing-menu-and-toolbar-commands.md)  
 コマンドについてのガイドラインを提供します。  
  
 [コマンドを使用可能にする](../../extensibility/internals/making-commands-available.md)  
 Visual Studio でのコマンドを使用できるようにする方法について説明します。  
  
 [相互運用機能アセンブリを使用するコマンドとメニュー](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)  
 相互運用機能アセンブリを使用するコマンドを実装する方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [Vspackage のコマンド ルーティング](../../extensibility/internals/command-routing-in-vspackages.md)  
 Vspackage でのコマンド ルーティングについて説明します。
