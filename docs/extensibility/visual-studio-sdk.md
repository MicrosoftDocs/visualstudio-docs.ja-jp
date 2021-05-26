---
title: Visual Studio SDK | Microsoft Docs
description: Visual Studio SDK を使用すると、機能を拡張したり、Visual Studio に新機能を追加したりすることができます。 Visual Studio を拡張する方法のいくつかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSSDK.v90.StartPage
helpviewer_keywords:
- Visual Studio SDK
- VS SDK (see Visual Studio SDK)
- Visual Studio, SDK
ms.assetid: 1f7c348a-114c-4243-b392-3531e9c9c6fd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 91411ec183e6c51abd825af1080c4330ca46fc90
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062526"
---
# <a name="visual-studio-sdk"></a>Visual Studio SDK
Visual Studio SDK を使用すると、Visual Studio 機能を拡張したり、Visual Studio に新機能を統合したりすることができます。 拡張機能は、他のユーザーや Visual Studio Marketplace にも配布できます。 Visual Studio を拡張する方法の一部を次に示します。

- コマンド、ボタン、メニュー、およびその他の UI 要素を IDE に追加する

- 新しい機能を使用するためのツール ウィンドウを追加する

- 特定の言語の IntelliSense を拡張するか、新しいプログラミング言語用に IntelliSense を提供する

- 電球を使用して、開発者がより適切なコードを記述するのに役立つヒントと提案を提供する

- 新しい言語のサポートを有効にする

- カスタム プロジェクト タイプを追加する

- Visual Studio Marketplace を通じて何百万もの開発者が参加するコミュニティにアクセスする

  以前に Visual Studio の拡張機能を作成したことがない場合は、これらの機能の詳細情報、および「[Visual Studio 拡張機能の開発を始める](../extensibility/starting-to-develop-visual-studio-extensions.md)」にある情報を確認する必要があります。

## <a name="install-the-visual-studio-sdk"></a>Visual Studio SDK のインストール
 Visual Studio SDK は、Visual Studio セットアップのオプション機能です。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="whats-new-in-the-visual-studio-sdk"></a>Visual Studio SDK の最新情報
 Visual Studio SDK には、同期的に自動読み込みされる拡張機能の警告や VSIX v3 形式、また拡張機能の更新が必要になる可能性がある破壊的変更など、いくつかの新機能があります。 詳細については、「[Visual studio 2019 SDK の新機能](../extensibility/whats-new-visual-studio-2019-sdk.md)」および「[Visual Studio 2017 SDK の新機能](../extensibility/what-s-new-in-the-visual-studio-2017-sdk.md)」を参照してください。

## <a name="visual-studio-user-experience-guidelines"></a>Visual Studio ユーザー エクスペリエンス ガイドライン
 「[Visual Studio のユーザー エクスペリエンス ガイドライン](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)」で、拡張機能の UI を設計するために役立つヒントをご覧ください。

 また、高 DPI デバイスで拡張機能の外観を向上させる方法について、「[DPI の問題に対処する](../extensibility/addressing-dpi-issues2.md)」を参照することもできます。

 優れたイメージ管理および高 DPI とテーマのサポートについては、「[イメージ サービスとカタログ](../extensibility/image-service-and-catalog.md)」を参照してください。

## <a name="find-and-install-existing-visual-studio-extensions"></a>既存の Visual Studio 拡張機能の検索とインストール
 Visual Studio の拡張機能は、 **[ツール]** メニューの **[拡張機能と更新プログラム]** ダイアログで見つけることができます。 詳細については、「[Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)」を参照してください。 また、[Visual Studio Marketplace](https://marketplace.visualstudio.com/) で拡張機能を検索することもできます。

## <a name="visual-studio-sdk-reference"></a>Visual Studio SDK のリファレンス
 Visual studio SDK API のリファレンスについては、「[Visual Studio SDK のリファレンス](../extensibility/visual-studio-sdk-reference.md)」を参照してください。

## <a name="visual-studio-sdk-samples"></a>Visual Studio SDK のサンプル
 GitHub 上の [Visual Studio のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples) ページで、VS SDK 拡張機能のオープン ソースの例を検索できます。 この GitHub リポジトリには、Visual Studio の拡張可能な各種機能を示すサンプルが含まれています。

## <a name="other-visual-studio-sdk-resources"></a>その他の Visual Studio SDK リソース
 VSSDK に関する質問がある場合、または拡張機能の開発経験を共有する場合は、[Visual Studio 機能拡張フォーラム](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx)または [ExtendVS Gitter チャットルーム](https://gitter.im/Microsoft/extendvs)を使用できます。

 詳細については、[VSX Arcana ブログ](/archive/blogs/vsx/)、および Microsoft MVP によって執筆されている多数のブログを参照してください。

- [お気に入りの Visual Studio 拡張機能](https://scottdorman.blog/2014/10/05/favorite-visual-studio-extensions/)

- [Visual Studio 機能拡張](http://www.visualstudioextensibility.com/overview/vs/)

- [Visual Studio の拡張](https://blog.slaks.net/2013-10-18/extending-visual-studio-part-1-getting-started/)

## <a name="see-also"></a>関連項目

- [メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)
- [方法: 機能拡張プロジェクトを Visual Studio 2017 に移行する](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)
- [FAQ: アドインを VSPackage 拡張に変換する](/previous-versions/visualstudio/visual-studio-2015/extensibility/faq-converting-add-ins-to-vspackage-extensions?preserve-view=true&view=vs-2015)
- [方法: マネージド コードの複数のスレッドを管理する](../extensibility/managing-multiple-threads-in-managed-code.md)
- [メニューとコマンドを拡張する](../extensibility/extending-menus-and-commands.md)
- [ツールバーへのコマンドの追加](../extensibility/adding-commands-to-toolbars.md)
- [ツール ウィンドウの拡張とカスタマイズ](../extensibility/extending-and-customizing-tool-windows.md)
- [エディターと言語サービスの拡張機能](../extensibility/editor-and-language-service-extensions.md)
- [プロジェクトを拡張する](../extensibility/extending-projects.md)
- [ユーザー設定とオプションを拡張する](../extensibility/extending-user-settings-and-options.md)
- [プロジェクトと項目のカスタム テンプレートを作成する](../extensibility/creating-custom-project-and-item-templates.md)
- [プロパティとプロパティ ウィンドウを拡張する](../extensibility/extending-properties-and-the-property-window.md)
- [Visual Studio の他の部分を拡張する](../extensibility/extending-other-parts-of-visual-studio.md)
- [サービスの使用と提供](../extensibility/using-and-providing-services.md)
- [VSPackage を管理する](../extensibility/managing-vspackages.md)
- [Visual Studio の分離シェル](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)
- [Visual Studio 拡張機能を配布する](../extensibility/shipping-visual-studio-extensions.md)
- [Visual Studio SDK の内部](../extensibility/internals/inside-the-visual-studio-sdk.md)
- [Visual Studio SDK のサポート](../extensibility/support-for-the-visual-studio-sdk.md)
- [Visual Studio SDK のリファレンス](../extensibility/visual-studio-sdk-reference.md)