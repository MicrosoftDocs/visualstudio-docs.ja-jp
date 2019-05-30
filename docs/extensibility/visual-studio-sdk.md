---
title: Visual Studio SDK |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSSDK.v90.StartPage
helpviewer_keywords:
- Visual Studio SDK
- VS SDK (see Visual Studio SDK)
- Visual Studio, SDK
ms.assetid: 1f7c348a-114c-4243-b392-3531e9c9c6fd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b713015bc2ee1f42fdf331521a990d89eb6adbcd
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323091"
---
# <a name="visual-studio-sdk"></a>Visual Studio SDK
Visual Studio SDK は Visual Studio の機能を拡張することや、Visual Studio に新しい機能を追加するのに役立ちます。 Visual Studio Marketplace では、あなたが作成した拡張機能を他のユーザーへ配布することができます。 Visual Studio を拡張する方法の一部を次に示します。

- IDE にコマンド、ボタン、メニューおよびその他の UI 要素を追加

- ツール ウィンドウに新しい機能を追加する

- 特定の言語の IntelliSense の拡張または新しいプログラミング言語に対して IntelliSense を提供

- 電球を使用して、優れたコードを記述のヒントと開発者に役立つ提案を提供

- 新しい言語のサポートを有効にする

- カスタム プロジェクトの種類を追加する

- Visual Studio Marketplace で何百万もの開発者に公開する

  以前に Visual Studio 拡張機能を書いたことが無い場合、これらの機能についての詳細については"[Visual Studio 拡張機能の開発を始める](../extensibility/starting-to-develop-visual-studio-extensions.md)"を参照してください。

## <a name="install-the-visual-studio-sdk"></a>Visual Studio SDK のインストール
 Visual Studio SDK は、Visual Studio セットアップで省略可能な機能です。 また、後から VS SDK をインストールすることもできます。 詳細については、"[Visual Studio SDK をインストール](../extensibility/installing-the-visual-studio-sdk.md)"を参照してください。

## <a name="whats-new-in-the-visual-studio-2017-sdk"></a>Visual Studio 2017 SDK の新機能について
 Visual Studio SDK は一部の新機能などで VSIX v3 形式だけでなく互換性の無い変更などがあり、拡張機能を更新する必要がある場合があります 詳細については、[Visual Studio 2017 SDKの新機能](../extensibility/what-s-new-in-the-visual-studio-2017-sdk.md)を参照してください。

## <a name="visual-studio-user-experience-guidelines"></a>Visual Studio ユーザー エクスペリエンス ガイドライン
 [Visual Studio ユーザー エクスペリエンス ガイドライン](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)で拡張機能の UI を設計するための便利なヒントを取得します。

 [DPIの問題の対処方法](../extensibility/addressing-dpi-issues2.md)で高 DPI デバイスに美しく表示拡張機能を作成する方法を確認できます。

 [イメージ サービスとカタログ](../extensibility/image-service-and-catalog.md)を活用して優れた画像の管理や、高DPIとテーマのサポートをします。

## <a name="find-and-install-existing-visual-studio-extensions"></a>既存の Visual Studio 拡張機能の検索とインストール
 **ツール**メニューの**拡張機能と更新**ダイアログでVisual Studio 拡張機能を見つけることができます。 詳細については、"[検索と使用の Visual Studio Extensions](../ide/finding-and-using-visual-studio-extensions.md)"を参照してください。 拡張機能を検索することも、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)

## <a name="visual-studio-sdk-reference"></a>Visual Studio SDK リファレンス
 [Visual Studio SDK リファレンス](../extensibility/visual-studio-sdk-reference.md)でVisual Studio SDK の API リファレンスを検索できます。

## <a name="visual-studio-sdk-samples"></a>Visual Studio SDK のサンプル
 GitHub の[Visual Studio のサンプル](https://aka.ms/vs2015sdksamples)で VS SDK 拡張機能のオープン ソースの例を検索できます。 この GitHub リポジトリには、Visual Studio のさまざまな拡張機能を示すサンプルが含まれています。

## <a name="other-visual-studio-sdk-resources"></a>その他の Visual Studio SDK のリソース
 VSSDK について質問があるか、拡張機能の開発経験を共有する場合、 [Visual Studio 機能拡張フォーラム](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vsx)または[ExtendVS Gitter チャット ルーム](https://gitter.im/Microsoft/extendvs)を利用できます。

 [Visual Studio ブログ](https://blogs.msdn.microsoft.com/vsx/)と Microsoft MVP によって書かれたブログで詳細を確認することができます。

- [お気に入りの Visual Studio 拡張機能](http://geekswithblogs.net/sdorman/archive/2014/10/05/favorite-visual-studio-extensions.aspx)

- [Visual Studio 機能拡張](http://www.visualstudioextensibility.com/overview/vs/)

- [Visual Studio の拡張](http://blog.slaks.net/2013-10-18/extending-visual-studio-part-1-getting-started/)

## <a name="see-also"></a>関連項目
- [メニュー コマンドを使用して拡張機能を作成します。](../extensibility/creating-an-extension-with-a-menu-command.md)
- [方法: 機能拡張プロジェクトを Visual Studio 2017 に移行します。](../extensibility/how-to-migrate-extensibility-projects-to-visual-studio-2017.md)
- [よくあるご質問: アドインを VSPackage 拡張機能に変換します。](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md)
- [マネージ コード内の複数のスレッドを管理します。](../extensibility/managing-multiple-threads-in-managed-code.md)
- [メニューとコマンドを拡張します。](../extensibility/extending-menus-and-commands.md)
- [ツールバーにコマンドを追加します。](../extensibility/adding-commands-to-toolbars.md)
- [拡張し、カスタマイズ ツール ウィンドウ](../extensibility/extending-and-customizing-tool-windows.md)
- [エディターと言語サービス拡張機能](../extensibility/editor-and-language-service-extensions.md)
- [プロジェクトを拡張します。](../extensibility/extending-projects.md)
- [ユーザー設定とオプションを拡張します。](../extensibility/extending-user-settings-and-options.md)
- [カスタム プロジェクトと項目テンプレートを作成します。](../extensibility/creating-custom-project-and-item-templates.md)
- [プロパティと、[プロパティ] ウィンドウを拡張します。](../extensibility/extending-properties-and-the-property-window.md)
- [Visual Studio の他の部分を拡張します。](../extensibility/extending-other-parts-of-visual-studio.md)
- [使用してサービスを提供します。](../extensibility/using-and-providing-services.md)
- [Vspackage を管理します。](../extensibility/managing-vspackages.md)
- [Visual Studio の分離シェル](/visualstudio/extensibility/shell/visual-studio-isolated-shell)
- [Visual Studio 拡張機能を出荷します。](../extensibility/shipping-visual-studio-extensions.md)
- [Visual Studio SDK の内部](../extensibility/internals/inside-the-visual-studio-sdk.md)
- [Visual Studio SDK のサポート](../extensibility/support-for-the-visual-studio-sdk.md)
- [アーカイブ](../extensibility/archive.md)
- [Visual Studio SDK リファレンス](../extensibility/visual-studio-sdk-reference.md)
