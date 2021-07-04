---
title: SharePoint ソリューションの作成 | Microsoft Docs
description: SharePoint Designer の代わりに Visual Studio で SharePoint アプリケーションを作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: c7a349cb79ca22869038e46d7ee27b2425119997
ms.sourcegitcommit: 1f27f33852112702ee35fbc0c02fba37899e4cf5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2021
ms.locfileid: "112113017"
---
# <a name="create-sharepoint-solutions"></a>SharePoint ソリューションの作成

  SharePoint Designer の代わりに Visual Studio で SharePoint アプリケーションを作成できます。 Visual Studio には、高度なデバッグ ツール、IntelliSense、ステートメント入力候補、プロジェクト テンプレートなど、迅速な SharePoint 開発を促進する機能が用意されています。 さらに、Visual Studio では、高度な .NET Framework ベースのツールと言語も活用されています。 SharePoint プロジェクトは Visual Basic または Visual C# を使用して開発できます。また、SharePoint 用アプリのプロジェクトは JavaScript を使用して開発できます。

> [!NOTE]
> 新しい [SharePoint アドイン モデル](/sharepoint/dev/sp-add-ins/sharepoint-add-ins) を使用してユーザーにとっての SharePoint の操作感を拡張する方法をご覧ください。 これらのアドインのフットプリントは、SharePoint ソリューションと比較して非常に小さく、その作成には、HTML5、JavaScript、CSS3、XML など、ほぼすべての Web プログラミング テクノロジを使用できます。

|コンテンツ領域|[アーティクル]|
|-|-|
|![ドキュメント](../sharepoint/media/vs-icon-documentation.gif "ドキュメント")|**ドキュメント**<br /><br /> -   [はじめに &#40;Visual Studio での SharePoint 開発&#41;](../sharepoint/getting-started-sharepoint-development-in-visual-studio.md)<br />-   [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)<br />-   [SharePoint ソリューションをローカライズする](../sharepoint/localizing-sharepoint-solutions.md)<br />-   [SharePoint ソリューションのビルドとデバッグ](../sharepoint/building-and-debugging-sharepoint-solutions.md)<br />-   [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)<br />-   [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)|
|![ドキュメント](../sharepoint/media/vs-icon-documentation.gif "ドキュメント")|**おすすめのタスク**<br /><br /> -   [チュートリアル: SharePoint のサイト列、コンテンツ タイプ、リストの作成](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)<br />-   [方法: イベント レシーバーを作成する](../sharepoint/how-to-create-an-event-receiver.md)<br />-   [方法: BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)<br />-   [方法: SharePoint Web パーツを作成する](../sharepoint/how-to-create-a-sharepoint-web-part.md)<br />-   [方法: SharePoint アプリケーション ページまたは Web パーツのユーザー コントロールを作成する](../sharepoint/how-to-create-a-user-control-for-a-sharepoint-application-page-or-web-part.md)|
|![チュートリアル](../sharepoint/media/vs-icon-walkthroughs.gif "チュートリアル")|**チュートリアル**<br /><br /> -   [SharePoint 開発のチュートリアル](../sharepoint/sharepoint-development-walkthroughs.md)|
|![コード サンプル](../sharepoint/media/vs-icon-codesamples.gif "コード サンプル")|**コード サンプル**<br /><br /> -   [SharePoint 開発のサンプル](../sharepoint/sharepoint-development-samples.md)<br />-   [SharePoint 開発者向けダウンロード](/sharepoint/dev/)|
|![トレーニング](../sharepoint/media/vs-icon-training.gif "トレーニング")|**トレーニング**<br /><br /> -   [SharePoint の開発者向けトレーニング](/sharepoint/dev/)|
|![フォーラム](../sharepoint/media/vs-icon-forums.gif "フォーラム")|**フォーラム**<br /><br /> -   [Visual Studio を使用した SharePoint 開発](https://social.msdn.microsoft.com/Forums/vstudio/home?forum=vssharepointdevelopment)<br />-   [SharePoint 2010](https://social.msdn.microsoft.com/Forums/sharepoint/home?category=sharepoint2010,sharepoint)|
|![トレーニング](../sharepoint/media/vs-icon-training.gif "トレーニング")|**ブログ**<br /><br /> -   [Visual Studio SharePoint 開発チームのブログ](/archive/blogs/vssharepointtoolsblog/)|
|![操作方法ビデオ](../sharepoint/media/vs-icon-howdoivideos.gif "操作方法のビデオ")|**操作方法ビデオ**<br /><br /> -   [操作方法: Visual Studio 2010 で SharePoint 2010 の視覚的 Web パーツを作成する](https://visualstudio.microsoft.com/)<br />-   [操作方法: Visual Studio 2010 で SharePoint 2010 のコンテンツ タイプを作成する](/previous-versions/visualstudio/visual-studio-2010/dd831853\(v\=vs.100\))<br />-   [操作方法: Visual Studio 2010 で SharePoint 2010 のサイト定義を作成する](/previous-versions/visualstudio/visual-studio-2010/dd831853\(v\=vs.100\))<br />-   [操作方法: Visual Studio 2010 を使用して SharePoint 2010 のビジネス データ接続モデルを作成する](/previous-versions/visualstudio/visual-studio-2010/dd831853\(v\=vs.100\))|
|![Channel 9 のビデオ](../sharepoint/media/vs-icon-channel9videos.gif "Channel 9 ビデオ")|**Channel 9 のビデオ**<br /><br /> -   [Visual Studio 2010 での SharePoint 開発の概要](https://channel9.msdn.com/blogs/funkyonex/overview-of-sharepoint-development-in-visual-studio-2010)<br />-   [Visual Studio 2010 で SharePoint 2010 Web パーツを構築する際のベスト プラクティス](https://channel9.msdn.com/blogs/funkyonex/best-practices-on-building-sharepoint-2010-web-parts-with-visual-studio-2010)<br />-   [Visual Studio 2010 の SharePoint フィーチャー デザイナーとパッケージ デザイナー](https://channel9.msdn.com/blogs/funkyonex/sharepoint-feature-and-package-designers-in-visual-studio-2010)|
|![Developer Center](../sharepoint/media/vs-icon-msdndevcenter.gif "デベロッパー センター")|**デベロッパー センター**<br /><br /> -   [Visual Studio 開発者向け技術情報](https://visualstudio.microsoft.com/)<br />-   [SharePoint デベロッパー センター](/sharepoint/dev/)<br />-   [SharePoint Server デベロッパー センター](/previous-versions/office/fp161348\(v\=office.15\))<br />-   [SharePoint Designer デベロッパー センター](/previous-versions/office/fp161348\(v\=office.15\))<br />-   [ASP.NET デベロッパー センター](/previous-versions/msdn10/aa336522(v=msdn.10))|
|![フィードバックの提供](../sharepoint/media/vs-icon-feedback.gif "ご意見とご感想")|**フィードバックの提供**<br /><br /> Visual Studio に関するフィードバックを送ることができます。<br /><br /> -   [Microsoft Connect](/collaborate/connect-redirect)<br /><br /> Visual Studio のドキュメントに関するフィードバックを送ることができます。<br /><br /> -   **簡易表示:** トピックの上部から、 **[このトピックを評価する]** リンクを選択してトピックの下部に移動します。そこで、 **[この情報は役にたちましたか。]** に対する応答として、 **[はい]** または **[いいえ]** を指定できます。 **[はい]** を選択した場合は、表示される 1 つ以上のチェック ボックスを選択し、テキスト ボックスに詳細情報を入力できます。 終了したら、 **[投稿]** ボタンをクリックします。<br />-   **スクリプトを使用しない表示:** トピックの上部で、 **[フィードバック]** リンクを選択し、TechNet および Expression ライブラリ フィードバック フォーラムにフィードバックを提供します。<br />-   **クラシック ビュー** トピックの上部で、 **[クリックして評価とフィードバックをお寄せください]** のアイコンを選択し、ドキュメント チームにそのトピックについてフィードバックしてください。|
