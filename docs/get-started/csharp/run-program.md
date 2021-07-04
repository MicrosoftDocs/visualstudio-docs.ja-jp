---
title: プログラム (C#) を実行する方法
description: Visual Studio で C# プログラムを実行するための初心者向けガイド。
ms.custom: vs-acquisition, get-started
ms.date: 10/16/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: ghogen
ms.author: ghogen
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: e20caabb55e65801224177168f5c936f81402bbd
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385228"
---
# <a name="how-to-run-a-c-program-in-visual-studio"></a>方法: Visual Studio で C# プログラムを実行する

プログラムを実行するために必要な作業は、どこから開始しているか、それがどんな種類のプログラム、アプリ、またはサービスであるか、およびそれをデバッガーで実行するかどうかによって異なります。 最も簡単なケースでは、Visual Studio で開いているプロジェクトがある場合、それをビルドして実行するのに、**Ctrl**+**F5** キー (**デバッグなしで開始**) または **F5** キー (**デバッグありで開始**) を押すか、Visual Studio のメイン ツールバーで緑色の矢印 (**スタート ボタン**) を押すかということです。

![スタート ボタンを示しているスクリーンショット](media/vs-start-button.png)

## <a name="starting-from-a-project"></a>プロジェクトから開始する

C# プロジェクト ( *.csproj* ファイル) があり、それが実行可能なプログラムであれば、実行できます。 プロジェクトに `Main` メソッドを含む C# ファイルが含まれていて、その出力が実行可能ファイル (EXE) である場合は、それが正常にビルドされれば実行できる可能性は非常に高くなります。

プログラムのコードが Visual Studio のプロジェクトに既に含まれている場合は、そのプロジェクトを開きます。 プロジェクトを開くには、Windows エクスプローラーで *.csproj* をダブルクリックまたはタップします。または、Visual Studio で **[プロジェクトを開く]** を選択し、プロジェクト ( *.csproj*) ファイルを参照して見つけ、プロジェクト ファイルを選択します。

Visual Studio でプロジェクトが読み込まれたら、**Ctrl**+**F5** キー (**デバッグなしで開始**) を押すか、Visual Studio ツールバーの緑色の **[スタート]** ボタンを使って、プログラムを実行します。  複数のプロジェクトがある場合は、`Main` メソッドを含むプロジェクトをスタートアップ プロジェクトとして設定する必要があります。 スタートアップ プロジェクトを設定するには、プロジェクト ノードを右クリックし、 **[スタートアップ プロジェクトに設定]** を選択します。

![スタートアップ プロジェクトの設定](media/set-as-startup-project.png)

Visual Studio により、プロジェクトのビルドと実行が試行されます。  ビルド エラーが発生した場合は、 **[出力]** ウィンドウにビルド出力が表示され、 **[エラー一覧]** ウィンドウにエラーが表示されます。

ビルドが成功すると、プロジェクトの種類に適した方法でアプリが実行されます。 コンソール アプリはターミナル ウィンドウで実行され、Windows デスクトップ アプリは新しいウィンドウで起動され、Web アプリは (IIS Express でホストされている ) ブラウザーで起動されるといった具合です。

## <a name="starting-from-code"></a>コードから開始する

コード リスト、コード ファイル、または少数のファイルから開始する場合は、まず、実行するコードが信頼できる発行元のものであり、実行可能なプログラムであることを確認します。 `Main` メソッドがある場合、コンソール アプリ テンプレートを使用して Visual Studio で使用するプロジェクトを作成できる実行可能なプログラムである可能性があります。

### <a name="code-listing-for-a-single-file"></a>1 つのファイルのコード リスト

Visual Studio を起動し、空の C# コンソール プロジェクトを開き、プロジェクト内に既にある .cs ファイル内のすべてのコードを選択して、削除します。 次に、コードの内容を .cs ファイルに貼り付けます。 コードを貼り付けるときに、前に存在していたコードを上書きまたは削除します。 元のコードに一致するように、ファイルの名前を変更します。

### <a name="code-listings-for-a-few-files"></a>いくつかのファイルのコード リスト

Visual Studio を起動し、空の C# コンソール プロジェクトを開き、プロジェクト内に既にある .cs ファイル内のすべてのコードを選択して、削除します。 次に、最初のコード ファイルの内容を .cs ファイルに貼り付けます。 元のコードに一致するように、ファイルの名前を変更します。 

2 番目のファイルについては、**ソリューション エクスプローラー** でプロジェクト ノードを右クリックして、プロジェクトのショートカット メニューを開き、 **[追加] > [既存の項目]** を選択 (または **Shift**+**Alt**+**A** キーの組み合わせを使用) して、コード ファイルを選択します。

### <a name="multiple-files-on-disk"></a>ディスク上の複数のファイル

1. 適切な種類の新しいプロジェクトを作成します (よくわからない場合は C# **コンソール アプリ** を使用します)。

2. プロジェクト ノードを右クリックし、 **[追加]**  >  **[既存の項目]** でファイルを選択し、それらをプロジェクトにインポートします。  

### <a name="starting-from-a-folder"></a>フォルダーから開始する

多くのファイルを含むフォルダーを使用している場合は、まず、プロジェクトまたはソリューションがあるかどうかを確認します。  プログラムが Visual Studio で作成された場合は、プロジェクト ファイルまたはソリューション ファイルが見つかるはずです。 Windows エクスプローラーで *.csproj* 拡張子または .sln 拡張子を持つファイルを探し、いずれかのファイルをダブルクリックして Visual Studio で開きます。 「[Visual Studio ソリューションまたはプロジェクトから開始する](#starting-from-a-project)」を参照してください。

コードが別の開発環境で開発された場合など、プロジェクト ファイルがない場合は、Visual Studio の **Open folder** メソッドを使用して最上位フォルダーを開きます。 「[プロジェクトまたはソリューションを使用せずにコードを開発する](../../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)」を参照してください。

## <a name="starting-from-a-github-or-azure-devops-repo"></a>GitHub または Azure DevOps リポジトリから開始する

実行するコードが GitHub または Azure DevOps リポジトリにある場合は、Visual Studio を使用して、リポジトリから直接プロジェクトを開くことができます。 「[リポジトリからプロジェクトを開く](../tutorial-open-project-from-repo.md)」を参照してください。

## <a name="run-the-program"></a>プログラムを実行する

プログラムを開始するには、Visual Studio のメイン ツールバーで緑色の矢印 ( **[スタート]** ボタン) を押すか、**F5** または **Ctrl**+**F5** キーを押してプログラムを実行します。 **[スタート]** ボタンを使用すると、デバッガーで実行されます。  Visual Studio により、プロジェクト内のコードのビルドと実行が試行されます。  成功すれば、終了です。 そうでない場合は、正常にビルドする方法に関するいくつかのアイデアを引き続きお読みください。

## <a name="troubleshooting"></a>トラブルシューティング

コードにエラーがある場合もありますが、コードが適切であっても、他のアセンブリや NuGet パッケージに依存している場合、または別のバージョンの .NET をターゲットにするように記述されている場合は、簡単に修正できる可能性があります。

### <a name="add-references"></a>参照の追加

適切にビルドするには、コードが適切であり、ライブラリまたはその他の依存関係への適切な参照が設定されている必要があります。 赤の波線と **エラー一覧** を見ると、プログラムをコンパイルして実行する前であっても、プログラムにエラーがあるかどうかを確認できます。 未解決の名前に関連するエラーが発生している場合は、参照または using ディレクティブのいずれかまたは両方を追加する必要があります。 コードがアセンブリまたは NuGet パッケージを参照している場合は、それらの参照をプロジェクトに追加する必要があります。

Visual Studio により、不足している参照の識別が容易になります。 名前が解決されない場合は、電球アイコンがエディターに表示されます。 電球をクリックすると、問題の解決方法に関するいくつかの推奨事項が表示されます。 解決方法には次のようなものがあります。

- using ディレクティブを追加する
- アセンブリに参照を追加する
- NuGet パッケージをインストールする

#### <a name="missing-using-directive"></a>using ディレクティブがない

たとえば、次の画面では、コード ファイルの先頭に `using System;` を追加して、未解決の名前 `Console` を解決することができます。

![using ディレクティブを追加する電球のスクリーンショット](media/name-does-not-exist2.png)

#### <a name="missing-assembly-reference"></a>アセンブリ参照がない

.NET 参照は、アセンブリまたは NuGet パッケージの形式にすることができます。 通常、ソース コードが見つかれば、発行元または作成者から必要なアセンブリと、コードが依存しているパッケージが説明されます。 プロジェクトへの参照を手動で追加するには、**ソリューション エクスプローラー** で **[参照]** ノードを右クリックし、 **[参照の追加]** を選択して、必要なアセンブリを見つけます。

![[参照の追加] メニューのスクリーンショット](media/add-reference.png)

アセンブリを検索し、参照を追加するには、「[参照マネージャーを使用して参照を追加または削除する](../../ide/how-to-add-or-remove-references-by-using-the-reference-manager.md)」の手順に従います。

#### <a name="missing-nuget-package"></a>NuGet パッケージがない

不足している NuGet パッケージが Visual Studio によって検出されると、電球が表示され、そのパッケージをインストールするオプションが表示されます。

![パッケージをインストールするための電球のスクリーンショット](media/lightbulb-add-package.png)

それでも問題が解決せず、Visual Studio がパッケージを見つけられない場合は、オンラインで検索してみてください。 「[Visual Studio に NuGet パッケージをインストールして使用する](/nuget/quickstart/install-and-use-a-package-in-visual-studio)」を参照してください。

## <a name="use-the-right-version-of-net"></a>適切なバージョンの .NET を使用する

.NET Framework のさまざまなバージョンにはある程度の下位互換性があるため、新しいフレームワークでは、古いフレームワーク用に記述されたコードを変更せずに実行できる可能性があります。 ただし、特定のフレームワークをターゲットにする必要がある場合もあります。 .NET Framework または .NET Core の特定のバージョンのインストールが必要になることがあります (まだインストールされていない場合)。 [Visual Studio の変更](../../install/modify-visual-studio.md)に関するページを参照してください。

ターゲット フレームワークを変更するには、[ターゲット フレームワークの変更](../../ide/visual-studio-multi-targeting-overview.md#select-a-target-framework-version)に関するセクションを参照してください。 詳細については、「[.NET Framework を対象とするエラーのトラブルシューティング](../../msbuild/troubleshooting-dotnet-framework-targeting-errors.md)」を参照してください。

## <a name="next-steps"></a>次の手順

「[Visual Studio IDE へようこそ](../visual-studio-ide.md)」を読んで、Visual Studio 開発環境を確認します。

## <a name="see-also"></a>関連項目

[C# アプリを初めて作成する](tutorial-console.md)
