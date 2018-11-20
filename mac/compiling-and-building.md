---
title: コードのコンパイルとビルド
description: この記事では、Visual Studio for Mac でプロジェクトとソリューションをコンパイルおよびビルドする方法について説明します。
author: conceptdev
ms.author: crdun
ms.date: 05/06/2018
ms.assetid: FB253757-DB00-4889-A6BF-E44722E25BD1
ms.openlocfilehash: fece226d9e7fd7ba023369928171553c393b46d5
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2018
ms.locfileid: "51294319"
---
# <a name="compiling-and-building-in-visual-studio-for-mac"></a>Visual Studio for Mac のコンパイルとビルド

Visual Studio for Mac は、プロジェクトの開発中、アプリケーションをビルドし、アセンブリを作成するために使用できます。 型の不一致やその他のコンパイル時エラーが見つかるように、コードは早い段階で頻繁にコンパイルし、ビルドすることが重要です。

## <a name="building-from-the-ide"></a>IDE でのビルド

Visual Studio for Mac を使用すると、ビルドをすぐに作成し、実行できます。また、ビルド機能を制御できます。 Visual Studio for Mac では、基礎ビルド システムとして MSBuild が使用されます。

IDE で作成されたすべてのプロジェクトとソリューションに既定のビルド構成が与えられます。この構成がビルドのコンテキストを定義します。 構成は編集可能です。独自の構成を作成するともできます。 構成を作成したり、変更したりすると、プロジェクト ファイルが自動的に更新されます。それが MSBuild で使用され、プロジェクトがビルドされます。

IDE でプロジェクトやソリューションをビルドする方法については、「[プロジェクトとソリューションのビルドおよびクリーン](building-and-cleaning-projects-and-solutions.md)」ガイドを参照してください。

Visual Studio for Mac は以下にも使用できます。

* 出力パスを変更します。 これはプロジェクトのオプションで編集します。

    ![出力パスの変更](media/compiling-and-building-image4.png)

* ビルド出力の詳細度を変更します。

    ![ビルドの詳細度の変更](media/compiling-and-building-image5.png)

* ビルドまたはクリーンの前後に、またはビルドまたはクリーンの最中にカスタム コマンドを追加します。

    ![カスタム コマンドを追加する](media/compiling-and-building-image6.png)

## <a name="building-from-command-line"></a>コマンド ラインからビルドする

MSBuild Build Engine を使用し、コマンド ラインからアプリケーションをビルドできます。

MSBuild の使用方法については、[MSBuild](/visualstudio/msbuild/msbuild) コンテンツをご覧ください。

## <a name="building-from-azure-pipelines"></a>Azure Pipelines からビルドする

* [Xamarin アプリをビルドする](/vsts/pipelines/apps/mobile/xamarin?view=vsts&tabs=vsts)
* [Xamarin との継続的な統合](https://developer.xamarin.com/guides/cross-platform/ci/)

## <a name="see-also"></a>関連項目

- [コンパイルとビルド (Windows の Visual Studio)](/visualstudio/ide/compiling-and-building-in-visual-studio)