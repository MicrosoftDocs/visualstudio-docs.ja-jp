---
title: Visual Studio for Mac ツアー
description: Visual Studio for Mac は、iOS、Android、Mac、Xamarin.Forms 用に、ASP.NET Core Web サイトや Xamarin プロジェクトなどの .NET アプリケーションを macOS 上で構築する統合開発環境 (IDE) として利用できます。
author: conceptdev
ms.author: crdun
ms.date: 02/07/2019
ms.assetid: 7DC64A52-AA41-4F3A-A8A1-8A20BCD81CC7
ms.custom: video
ms.openlocfilehash: 2a5b60496a53c35bb67e5cd19d6059212e22ccfd
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2019
ms.locfileid: "55911781"
---
# <a name="visual-studio-2019-for-mac-preview-tour"></a>Visual Studio 2019 for Mac プレビュー ツアー

> [!NOTE]
> Visual Studio 2019 for Mac がプレビューとして[リリース](installation.md)され、テストできるようになりました。

Visual Studio for Mac は、Xamarin のモバイルを中心とした IDE である Xamarin Studio を、Mac 上のモバイル優先、クラウド優先の開発環境へと進化させました。 この開発者向けツールから .NET の機能を使用して、対象ユーザーに必要なすべてのプラットフォーム用アプリケーションを作成できます。

Visual Studio for Mac のユーザー エクスペリエンス (UX) は Windows 版と似ていますが、ネイティブ macOS の操作感もあります。 Windows で Visual Studio を使用したことがあれば、使い慣れた方法でアプリの作成、起動、開発を行うことができます。 また、Visual Studio for Mac は、Windows 版を強力な IDE にしている強力なツールの多くを採用しています。 Roslyn コンパイラ プラットフォームは、リファクタリングと IntelliSense に使用されます。 そのプロジェクト システムとビルド エンジンは MSBuild を使用し、ソース エディターは TextMate バンドルをサポートしています。 Xamarin アプリと .NET Core アプリに同じデバッグ エンジンを使用し、Xamarin.iOS と Xamarin.Android に同じデザイナーを使用しています。

この記事では、Visual Studio for Mac の多様なセクションについて説明し、クロスプラットフォーム アプリケーションを作成する場合に強力なツールになる機能の一部を紹介します。

## <a name="ide-tour"></a>IDE ツアー

Visual Studio for Mac は、アプリケーションのファイルと設定の管理、アプリケーション ノードの作成、およびデバッグのセクションに分かれています。

## <a name="new-start-window"></a>新しいスタート ウィンドウ

Visual Studio 2019 for Mac プレビューを起動すると、新規ユーザーにはサインイン ウィンドウが表示されます。 ご自分の Microsoft アカウントでサインインして、有料ライセンス (ある場合) をアクティブ化するか、Azure サブスクリプションにリンクします。 **[スキップ]** を押して、後で **[Visual Studio] > [サインイン]** メニュー項目を使用してサインインすることができます。

![Microsoft アカウントにサインインする](media/ide-tour-2019-start-signin.png)

サインインしたユーザーには、新しい_スタート ウィンドウ_が表示されます。このウィンドウには、最近使用したプロジェクトの一覧と、既存のプロジェクトを開いたり、新しいプロジェクトを作成するためのボタンが表示されます。

![最近使用したプロジェクトから選択するか、新しいものを作成する](media/ide-tour-2019-start-projects.png)

## <a name="solutions-and-projects"></a>ソリューションとプロジェクト

次の図は、アプリケーションが読み込まれた Visual Studio for Mac を示しています。

![アプリケーションが読み込まれた Visual Studio for Mac](media/ide-tour-image17.png)

以下のセクションでは、Visual Studio for Mac の主な領域について概要を説明します。

## <a name="solution-pad"></a>Solution Pad

Solution Pad では、ソリューション内のプロジェクトが整理されています。

![Solution Pad に整理されているプロジェクト](media/ide-tour-image18.png)

これは、ソース コード、リソース、ユーザー インターフェイス、および依存関係のファイルが、プラットフォーム固有のプロジェクトに整理されている場所です。

Visual Studio for Mac でプロジェクトとソリューションを使用する方法の詳細については、「[プロジェクトおよびソリューション](/visualstudio/mac/projects-and-solutions)」を参照してください。

## <a name="assembly-references"></a>アセンブリ参照

各プロジェクトのアセンブリ参照は、[参照] フォルダーの下に表示されます。

![Solution Pad の [参照] フォルダー](media/ide-tour-image19.png)

その他の参照は、**[参照の編集]** ダイアログを使用して追加されます。このダイアログを表示するには、[参照] フォルダーをダブルクリックするか、コンテキスト メニュー操作で **[参照の編集]** を選択します。

![[参照の編集] ダイアログ](media/ide-tour-image20.png)

Visual Studio for Mac で参照を使用する方法については、「[プロジェクト内の参照の管理](/visualstudio/mac/managing-references-in-a-project)」を参照してください。

## <a name="dependencies--packages"></a>依存関係/パッケージ

アプリで使用されるすべての外部依存関係は、[依存関係] フォルダーまたは [パッケージ] フォルダーに格納されます。格納される場所は、.NET Core プロジェクトか Xamarin.iOS/Xamarin.Android プロジェクトかによって変わります。 通常、NuGet の形式で提供されます。

NuGet は、.NET 開発用の最も人気のあるパッケージ マネージャーです。 Visual Studio は NuGet をサポートしているので、簡単にパッケージを検索し、プロジェクトをアプリケーションに追加できます。

依存関係をアプリケーションに追加するには、[依存関係]/[パッケージ] フォルダーを右クリックし、**[パッケージの追加]** を選択します。

![NuGet パッケージの追加](media/ide-tour-image21.png)

アプリケーションで NuGet パッケージを使用する方法については、「[プロジェクトに NuGet パッケージを含める](/visualstudio/mac/nuget-walkthrough)」を参照してください。

## <a name="refactoring"></a>リファクタリング

Visual Studio for Mac には、コードをリファクターする 2 つの便利な方法があります。コンテキスト アクションとソース分析です。 詳細については、「[リファクタリング](/visualstudio/mac/refactoring)」を参照してください。

## <a name="debugging"></a>デバッグ

Visual Studio for Mac には、Xamarin.iOS、Xamarin.Mac、Xamarin.Android アプリケーションのデバッグをサポートするネイティブ デバッガーが備わっています。 Visual Studio for Mac では、IDE ですべてのプラットフォームでマネージド コードをデバッグするために、Mono ランタイムに実装されている Mono Soft Debugger を使用しています。 デバッグの詳細については、「[Xamarin を使ったデバッグ](/visualstudio/mac/debugging)」を参照してください。

デバッガーには、文字列、色、URL だけでなく、サイズ、座標、ベジエ曲線などの特殊な種類の高機能なビジュアライザーが含まれています。

デバッガーのデータの視覚化の詳細については、「[データの視覚化](/visualstudio/mac/data-visualizations)」を参照してください。

## <a name="version-control"></a>バージョン管理

Visual Studio for Mac は、Git と Subversion ソース管理システムと統合されています。 ソース管理下にあるプロジェクトは、ソリューション名の横にブランチとして一覧表示されます。

![ソース管理下にあるプロジェクトを示すブランチ名](media/ide-tour-image22.png)

コミットされていない変更があるファイルは、次の図に示すように、ソリューション ウィンドウにアイコンで示されます。

![Solution Pad のコミットされていないファイル](media/ide-tour-image23.png)

Visual Studio でバージョン管理を使用する方法については、「[バージョン管理](/visualstudio/mac/version-control)」を参照してください。

## <a name="next-steps"></a>次の手順

- [Visual Studio for Mac をインストールする](installation.md)
- [使用できるワークロードを確認する](/visualstudio/mac/workloads/)

## <a name="related-video"></a>関連ビデオ

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Overview/player]

## <a name="see-also"></a>関連項目

- [Visual Studio IDE (Windows)](/visualstudio/ide/visual-studio-ide)
