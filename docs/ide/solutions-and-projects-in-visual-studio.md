---
title: Visual Studio のソリューションおよびプロジェクト
description: Visual Studio のプロジェクトとソリューションの概要、テンプレートから新しいプロジェクトを作成する方法、ソリューション エクスプローラーでプロジェクトを表示および管理する方法について説明します。
ms.custom: SEO-VS-2020, contperf-fy21q2
ms.date: 12/31/2020
ms.topic: conceptual
f1_keywords:
- vs.openproject
- vs.addexistingitem
- vs.addexistingsolutionitem
- vs.environment.projects
- vs.environment.solutions
- VS.SolutionExplorer.Solutions
helpviewer_keywords:
- solutions [Visual Studio]
- projects [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0a186c63cf695184b74780eeb6ab16b85c8aef5e
ms.sourcegitcommit: d3658667e768d7516cbf4461ec47bf24c8fcb7e6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112924969"
---
# <a name="what-are-solutions-and-projects-in-visual-studio"></a>Visual Studio のソリューションおよびプロジェクト

この記事では、Visual Studio の "*プロジェクト*" と "*ソリューション*" について説明します。 また、ソリューション エクスプローラー ツール ウィンドウ、および新しいプロジェクトの作成方法についても簡単に説明します。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac のプロジェクトおよびソリューション](/visualstudio/mac/projects-and-solutions)に関するページを参照してください。

## <a name="projects"></a>プロジェクト

Visual Studio で、アプリまたは Web サイトを作成するときは、"*プロジェクト*" から始めます。 論理的には、実行可能ファイル、ライブラリ、または Web サイトにコンパイルされる、すべてのファイルがプロジェクトに含まれています。 これらのファイルには、ソース コード、アイコン、イメージ、データ ファイルなどを含めることができます。 また、プロジェクトには、プログラムが通信するさまざまなサービスまたはコンポーネントで必要になる可能性がある、コンパイラ設定とその他の構成ファイルも含まれています。

### <a name="project-file"></a>プロジェクト ファイル

Visual Studio では、[MSBuild](../msbuild/msbuild.md) を使用してソリューション内の各プロジェクトをビルドします。各プロジェクトには MSBuild プロジェクト ファイルが含まれています。 ファイル拡張子は、C# プロジェクト (.csproj)、Visual Basic プロジェクト (.vbproj)、またはデータベース プロジェクト (.dbproj) などのプロジェクトの種類を反映しています。 プロジェクト ファイルは、MSBuild がプロジェクトをビルドするために必要なすべての情報と手順が含まれる XML ドキュメントです。これには、コンテンツ、プラットフォーム要件、バージョン管理情報、Web サーバーまたはデータベース サーバーの設定、実行するタスクなどがあります。

プロジェクト ファイルは、[MSBuild XML スキーマ](../msbuild/msbuild-project-file-schema-reference.md)に基づいています。 Visual Studio で新しい [sdk スタイルのプロジェクト ファイル](../msbuild/how-to-use-project-sdk.md)のコンテンツを確認するには、 **[ソリューション エクスプローラー]** 内でプロジェクト ノードを右クリックし、 **[編集]\<projectname\>** を選択します。 .NET フレームワークのコンテンツや、そのスタイルのその他のプロジェクトのコンテンツを確認するには、まずプロジェクトをアンロードします ( **[ソリューション エクスプローラー]** を右クリックして、 **[プロジェクトのアンロード]** を選択します)。 次に、プロジェクトを右クリックして、 **[編集]\<projectname\>** を選択します。

> [!NOTE]
> Visual Studio でソリューションまたはプロジェクトを使用して、コードの編集、ビルド、デバッグを行う必要はありません。 単に Visual Studio でソース ファイルを含むフォルダーを開いて編集を開始できます。 詳細については、「[プロジェクトまたはソリューションを使用せずに Visual Studio でコードを開発する](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)」を参照してください。

### <a name="create-new-projects"></a>新しいプロジェクトの作成

新しいプロジェクトを作成する最も簡単な方法は、目的のプロジェクトの種類に適したプロジェクト テンプレートを使用することです。 プロジェクト テンプレートには、事前に生成されたコード ファイル、構成ファイル、資産、設定の基本セットが含まれています。 **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** を使用して、プロジェクト テンプレートを選択します。 詳細については、[新しいプロジェクトの作成](create-new-project.md)に関するページを参照してください。

また、新しいプロジェクトの作成元として使用できるカスタム プロジェクト テンプレートを作成することもできます。 詳細については、[プロジェクト テンプレートと項目テンプレートの作成](../ide/creating-project-and-item-templates.md)に関するページをご覧ください。

新しいプロジェクトを作成すると、Visual Studio によって、その既定の場所である *%USERPROFILE%\source\repos* に保存されます。 この場所を変更するには、 **[ツール]**  >  **[オプション]**  >  **[プロジェクトおよびソリューション]**  >  **[場所]** に移動します。 詳細については、「[[オプション] ダイアログ ボックス:[プロジェクトおよびソリューション] > [場所]](./reference/projects-solutions-locations-options.md)」を参照してください。

## <a name="solutions"></a>解決策

プロジェクトは *ソリューション* 内に含まれます。 ソリューションは、その名前にもかかわらず、"答え" ではありません。 1 つ以上の関連するプロジェクト、およびビルド情報、Visual Studio ウィンドウの設定、特定のプロジェクトに関連付けられていないその他のファイルに対するコンテナーに過ぎません。

### <a name="solution-file"></a>ソリューション ファイル

Visual Studio では、ソリューションの設定を格納するために、2 種類のファイル ( *.sln* および *.suo*) を使用します。

|拡張子|名前|説明|
|---------------|----------|-----------------|
|.sln|Visual Studio ソリューション|ソリューション内のプロジェクト、プロジェクト項目、およびソリューション項目を整理します。|
|.suo|ソリューション ユーザー オプション|ユーザー レベルの設定やブレークポイントなどのカスタマイズを格納します。|

> [!IMPORTANT]
> ソリューションは独自の形式を持つテキスト ファイル (拡張子 *.sln*) で記述され、手動での編集は想定されていません。 これに対して、 *.suo* ファイルは隠しファイルであり、エクスプローラーの既定の設定では表示されません。 隠しファイルを表示するには、エクスプローラーの **[表示]** メニューで **[非表示項目]** チェックボックスをオンにします。

### <a name="solution-folder"></a>ソリューション フォルダー

"ソリューション フォルダー" は、**ソリューション エクスプローラー** にのみ存在する仮想フォルダーで、ソリューション内のプロジェクトをグループ化するために使用できます。 コンピューター上のソリューション ファイルを検索する場合は、 **[ツール]**  >  **[オプション]**  >  **[プロジェクトおよびソリューション]**  >  **[場所]** にアクセスします。 詳細については、「[[オプション] ダイアログ ボックス:[プロジェクトおよびソリューション] > [場所]](./reference/projects-solutions-locations-options.md)」を参照してください。

> [!TIP]
> ステップ バイ ステップの手順とサンプル コードを備えた、最初から作成したプロジェクトとソリューションの例については、「[プロジェクトとソリューションについて理解する](../get-started/tutorial-projects-solutions.md)」を参照してください。

## <a name="solution-explorer"></a>ソリューション エクスプローラー

新しいプロジェクトを作成した後は、**ソリューション エクスプローラー** を使用して、プロジェクトとソリューション、およびそれらの関連項目を表示して管理できます。 次の図に、2 つのプロジェクトを含む C# ソリューションが表示された **ソリューション エクスプローラー** を示します。

::: moniker range="vs-2017"

![2 つのプロジェクトを含むソリューション エクスプローラーのスクリーンショット。](../ide/media/vs2015_solution_explorer.png)

**ソリューション エクスプローラー** の上部のツールバーには、ソリューション ビューからフォルダー ビューに切り替える、隠しファイルを表示する、すべてのノードを折りたたむためなどのボタンがあります。

::: moniker-end

::: moniker range=">=vs-2019"

![Visual Studio での 2 つのプロジェクトを含むソリューション エクスプローラーのスクリーンショット。](../ide/media/solution-explorer.png)

**ソリューション エクスプローラー** の上部にあるツール バーには、ソリューション ビューからフォルダー ビューへの切り替え、保留中の変更のフィルター処理、すべてのファイルの表示、すべてのノードの表示、[プロパティ](managing-project-and-solution-properties.md) ページの表示、[コード エディター](writing-code-in-the-code-and-text-editor.md)でのコードのプレビューなどを行うためのボタンがあります。

::: moniker-end

多くのメニュー コマンドは、**ソリューション エクスプローラー** で各種項目の右クリックのコンテキスト メニューから使用できます。 これらのコマンドには、プロジェクトのビルド、NuGet パッケージの管理、参照の追加、ファイル名の変更、テストの実行などが含まれます。

ASP.NET Core プロジェクトでは、**ソリューション エクスプローラー** でファイルを入れ子にする方法をカスタマイズできます。 詳細については、[ソリューション エクスプローラーでのファイルの入れ子のカスタマイズ](file-nesting-solution-explorer.md)に関するページを参照してください。

> [!TIP]
> 閉じたソリューション エクスプローラーをもう一度開くには、メニュー バーから **[ビュー]**  >  **[ソリューション エクスプローラー]** を選択するか、**Ctrl**+**Alt**+**L** を押します。 また閉じたサイド タブをそれらの既定の場所に復元するには、メニュー バーの **[ウィンドウ]**  >  **[ウィンドウ レイアウトのリセット]** を選択します。

> [!NOTE]
> Visual Studio に表示されるアプリケーションのイメージおよびアイコンを参照するには、[**Visual Studio Image Library**](https://www.microsoft.com/download/details.aspx?id=35825) を参照してください。

## <a name="see-also"></a>関連項目

- [プロジェクトとソリューションの概要](../get-started/tutorial-projects-solutions.md)
- [プロジェクトおよびソリューションのプロパティの管理](managing-project-and-solution-properties.md)
- [Visual Studio のフィルター処理済みソリューション](filtered-solutions.md)
- [プロジェクトの移植、移行、およびアップグレード](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
- [Visual Studio IDE に関するエラーのトラブルシューティング情報](./reference/resources-for-troubleshooting-integrated-development-environment-errors.md)
- [プロジェクトとソリューション (Visual Studio for Mac)](/visualstudio/mac/projects-and-solutions)
