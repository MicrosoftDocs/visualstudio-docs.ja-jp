---
title: Visual Studio 拡張機能開発の開始 | Microsoft Docs
description: Visual Studio 拡張機能を初めて作成するユーザーからよく寄せられる質問について説明します。
ms.custom: SEO-VS-2020
ms.date: 09/18/2017
ms.topic: conceptual
helpviewer_keywords:
- getting started, Visual Studio integration
- Visual Studio, integration
ms.assetid: 8fe5e2ab-a424-4173-9d39-dd082c4d58d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d8101640ce3e4a998d0a97fa1d85ded27fa746d0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089941"
---
# <a name="starting-to-develop-visual-studio-extensions"></a>Visual Studio 拡張機能の開発を始める

以前に Visual Studio 拡張機能を作成したことがないユーザーからは、よく質問が寄せられます。 ここでは、最も一般的なものをいくつか紹介します。 探している情報が見つからない場合は、フィードバック ボタン (画面の右上にある **[このページは役立ちますか?]** ) を使用して質問をお寄せください。

> [!NOTE]
> この記事は、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、[Visual Studio for Mac の拡張](/visualstudio/mac/extending-visual-studio-mac)に関するページを参照してください。 Visual Studio のコードについては、[Visual Studio Code 拡張機能 API](https://code.visualstudio.com/api) に関するページを参照してください。

## <a name="what-software-do-i-need-to-develop-visual-studio-extensions"></a>Visual Studio 拡張機能を開発するために必要なソフトウェアは何ですか?

Visual Studio 拡張機能を開発するには、Visual Studio の他に Visual Studio SDK をインストールする必要があります。 Visual Studio SDK は、通常のセットアップの一環としてインストールすることも、後でインストールすることもできます。 Visual Studio SDK のインストールの詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="what-kinds-of-things-can-i-do-with-visual-studio-extensions"></a>Visual Studio 拡張機能で、どのような処理を実行できますか?

さまざまな Visual Studio 拡張機能を考えると、実行できる処理は無限にあります。 もちろん、ほとんどの拡張機能にはコードの記述が必要ですが、それは問題ではありません。 ここでは、作成できる拡張機能の例をいくつか示します。

- Visual Studio に含まれていない言語のサポート、構文の色分け、IntelliSense、コンパイラとデバッグのサポート

- 追加のテンプレート、コード リファクタリング、新しいダイアログまたはツール ウィンドウを含む、IDE のコア エクスペリエンスを拡張する生産性向上ツール

- データ設計やクラウド サポートなどのシナリオ向けのドメイン固有のデザイナー

拡張機能の例については、[Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) をご覧ください。 多くの拡張機能はオープンソースであり、Marketplace には、GitHub リポジトリへのリンクが含まれています。

## <a name="which-visual-studio-features-can-i-extend"></a>拡張できるのは、Visual Studio のどの機能ですか?

理論的には、メニュー、ツール バー、コマンド、ウィンドウ、ソリューション、プロジェクト、エディターなど、Visual Studio のあらゆる部分を拡張できます。

実際には、ほとんどの場合に拡張される機能は、コマンド、メニューとツール バー、ウィンドウ、IntelliSense、およびプロジェクトです。 関連するセクションへのリンクを次に示します。

- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md): 独自の項目を、Visual Studio のメニューとツール バーに追加します。 これらの項目を使用して、新しい Visual Studio 機能や、独自の外部ヘルパー アプリケーションを起動することができます。 メニュー項目のカスタム ショートカットを作成することもできます。

- [ツール ウィンドウの拡張とカスタマイズ](../extensibility/extending-and-customizing-tool-windows.md): 既存のツール ウィンドウを拡張するか、独自のツール ウィンドウを作成します。 たとえば、新しいプロパティを **[プロパティ]** に追加したり、新しいツール ウィンドウを作成して機能を追加したりできます。

- [エディターと言語サービスの拡張機能](../extensibility/editor-and-language-service-extensions.md): Visual Studio の言語のために用意されている IntelliSense に独自のカスタマイズを追加したり、新しいプログラミング言語のサポートを作成したりできます。 新しいステートメント入力候補、推奨事項、および新しい QuickInfo ツールヒントを作成できます。 電球アイコンを使用すると、リファクタリング候補とコード修正を追加して、新しいプログラミング言語をサポートすることができます。

- [プロジェクトの拡張](../extensibility/extending-projects.md)

- [ユーザー設定とオプションの拡張](../extensibility/extending-user-settings-and-options.md)

- [プロパティとプロパティ ウィンドウの拡張](../extensibility/extending-properties-and-the-property-window.md)

- [Visual Studio の他の部分の拡張](../extensibility/extending-other-parts-of-visual-studio.md)

- [Visual Studio の分離シェル](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

## <a name="what-project-templates-are-provided-by-the-vssdk"></a><a name="BKMK_ProjectTemplate"></a> VSSDK には、どのようなプロジェクト テンプレートが用意されていますか?
 拡張機能には、Vspackage と MEF という 2 つの主な種類があります。 一般に、VSPackage の拡張機能は、コマンド、ツール ウィンドウ、およびプロジェクトを使用したり、拡張したりする拡張機能として使用されます。 MEF 拡張機能は、Visual Studio エディターの拡張またはカスタマイズのために使用されます。

 Visual C# および Visual Basic の拡張機能の場合は、空の VSIX プロジェクト テンプレートが VSSDK に用意されており、メニュー コマンド、ツール ウィンドウ、およびエディターの拡張機能を作成する新しい項目テンプレートと共に使用できます。 このテンプレートを使用して、プロジェクト テンプレート、コード スニペット、および他のユーザーに配布するためのその他の成果物をパッケージ化することもできます。

 C++ の場合は、メニュー コマンド、ツール ウィンドウ、およびカスタム エディターを追加するためのコードが VSPackage ウィザードに用意されています。

 分離シェル テンプレートを使用すると、Visual Studio シェルのバージョンに拡張機能をパッケージ化し、独自にブランド化して配布することができます。 以降のトピックでは、拡張機能の各種類の使用を開始する方法を説明します。

- メニュー コマンド: [メニュー コマンドによる拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)

- ツール ウィンドウ: [ツール ウィンドウによる拡張機能の作成](../extensibility/creating-an-extension-with-a-tool-window.md)

- エディター拡張機能: [エディター項目テンプレートによる拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)

- 基本的な VSPackage: [VSPackage による拡張機能の作成](../extensibility/creating-an-extension-with-a-vspackage.md)

- VSIX プロジェクト テンプレート: [VSIX プロジェクト テンプレートの概要](../extensibility/getting-started-with-the-vsix-project-template.md)

## <a name="how-do-i-get-my-extension-to-look-like-visual-studio"></a>どうすれば、Visual Studio と同様に拡張機能が表示されますか?
 「[Visual Studio のユーザー エクスペリエンス ガイドライン](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)」で、拡張機能の UI を設計するために役立つヒントをご覧ください。

## <a name="where-can-i-find-examples-of-vssdk-code"></a>VSSDK コードの例は、どこで入手できますか?
 前の各セクションに記載されている各リンクで、特定の機能の実装方法をわかりやすく示したチュートリアルを参照できます。 また、[Visual Studio のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)のページで、GitHub のオープンソース VSSDK のサンプルを見つけることもできます。

## <a name="how-can-i-distribute-my-extension"></a>どうすれば、拡張機能を配布できますか?
 拡張機能は、別のコンピューターにインストールしたり、.vsix ファイルとして友人に送信したりでき、このファイルをダブルクリックするとインストールできます。 VSIX パッケージの詳細については、「[Visual Studio 拡張機能の配布](../extensibility/shipping-visual-studio-extensions.md)」を参照してください。

 また、Visual Studio Marketplace で拡張機能を公開することもできます。こうすると、Visual Studio の多くのユーザーに表示されます。 Marketplace 向けの拡張機能のパッケージ化の例については、「[チュートリアル: Visual Studio の拡張機能を公開する](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)」を参照してください。 Marketplace で公開するために必要な作業の詳細については、[Visual Studio の製品と拡張機能](/azure/devops/extend/overview?view=vsts&preserve-view=true)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [Visual Studio for Mac の拡張](/visualstudio/mac/extending-visual-studio-mac)
- [Visual Studio Code の拡張](https://code.visualstudio.com/api)に関するページ