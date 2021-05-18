---
title: コードのコンパイルとビルド
description: この記事では、Visual Studio for Mac でプロジェクトとソリューションをコンパイルおよびビルドする方法について説明します。
ms.topic: overview
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/03/2021
ms.assetid: FB253757-DB00-4889-A6BF-E44722E25BD1
ms.openlocfilehash: a24c57907afedb4f02068a071d2c9f81eb8962bb
ms.sourcegitcommit: dd2fc6e03a789c044f8438096b8f112e4dba5557
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2021
ms.locfileid: "108640975"
---
# <a name="compiling-and-building-in-visual-studio-for-mac"></a>Visual Studio for Mac のコンパイルとビルド

Visual Studio for Mac は、プロジェクトの開発中、アプリケーションをビルドし、アセンブリを作成するために使用できます。 コードを頻繁にビルドして、型の不一致、誤りのある構文、キーワードのスペルミス、その他のコンパイル時エラーをすばやく特定できるようにすることが重要です。 ビルド後にデバッグすることで、ロジック、IO、ゼロ除算エラーなどの実行時エラーを検出して修正することもできます。

ビルドの成功とは、ソース コードの構文が正しいことと、ライブラリやアセンブリなどのコンポーネントへの静的参照をすべて解決できることを意味します。 ビルド プロセスによって、アプリケーションの実行可能ファイルが生成されます。 この実行可能ファイルは、デバッグ、およびさまざまな種類の手動テストと自動テストによって、コードの品質を検証することができます。 アプリケーションのテストが完了したら、リリース バージョンをコンパイルしてユーザーに配置します。

Mac では、次の方法のいずれかを使用してアプリケーションをビルドできます: Visual Studio for Mac、MSBuild コマンドライン ツール、または Azure Pipelines。

| ビルド方法 | メリット |
| --- |--- | --- |
| Visual Studio for Mac |- ビルドを即座に作成してデバッガーでテストできます。<br />- マルチプロセッサ ビルドを実行できます (C# のプロジェクトの場合)。<br />- ビルド システムのさまざまな面をカスタマイズできます。 |
| MSBuild コマンドライン| - Visual Studio for Mac をインストールせずにプロジェクトをビルドできます。<br />- すべてのプロジェクト タイプでマルチ プロセッサ ビルドを実行できます。<br />- ビルド システムのほとんどの部分をカスタマイズできます。|
| Azure Pipelines | - ビルド プロセスを継続的インテグレーション/継続的デリバリー パイプラインの一部として自動化できます。<br />- 自動テストをすべてのビルドに適用します。<br />- クラウド ベースのリソースをほぼ無制限にビルド プロセスに使用できます。<br />- ビルド ワークフローの変更やビルド アクティビティの作成が可能です。実行するタスクを大幅にカスタマイズできます。|

このセクションでは、IDE ベースのビルド プロセスを詳しく解説します。 Visual Studio for Mac をインストールせずにコマンド ラインからアプリケーションをビルドするには、最新の [.NET Core SDK](https://dotnet.microsoft.com/download) をインストールします。 コマンド ラインを使用してアプリケーションをビルドする方法の詳細については、「[MSBuild](/visualstudio/msbuild/msbuild)」を参照してください。 Azure Pipelines を使用したアプリケーションのビルドの詳細については、[Azure Pipelines](/azure/devops/pipelines) に関する記事を参照してください。


> [!NOTE]
> このトピックは、Visual Studio for Mac に適用されます。 Windows での Visual Studio については、「[Visual Studio でのコンパイルとビルド](/visualstudio/ide/compiling-and-building-in-visual-studio)」を参照してください。


## <a name="building-from-the-ide"></a>IDE でのビルド

Visual Studio for Mac を使用すると、ビルドをすぐに作成し、実行できます。また、ビルド機能を制御できます。 プロジェクトを作成すると、Visual Studio for Mac によって、ビルドのコンテキストを設定する既定のビルド構成が定義されます。 既定のビルド構成を編集し、独自に作成することもできます。 構成を作成したり、変更したりすると、プロジェクト ファイルが自動的に更新されます。それが MSBuild で使用され、プロジェクトがビルドされます。

IDE でプロジェクトやソリューションをビルドする方法については、「[プロジェクトとソリューションのビルドおよびクリーン](building-and-cleaning-projects-and-solutions.md)」ガイドを参照してください。

Visual Studio for Mac は以下にも使用できます。

* 出力パスを変更します。 これはプロジェクトのオプションで編集します。

    ![出力パスの変更](media/compiling-and-building-image4.png)

* ビルド出力の詳細度を変更します。

    ![ビルドの詳細度の変更](media/compiling-and-building-image5.png)

* ビルドまたはクリーンの前後に、またはビルドまたはクリーンの最中にカスタム コマンドを追加します。

    ![カスタム コマンドを追加する](media/compiling-and-building-image6.png)


## <a name="see-also"></a>関連項目

- [コンパイルとビルド (Windows の Visual Studio)](/visualstudio/ide/compiling-and-building-in-visual-studio)
