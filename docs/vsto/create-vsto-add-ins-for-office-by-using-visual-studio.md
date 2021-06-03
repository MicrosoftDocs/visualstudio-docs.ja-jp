---
title: Visual Studio を使用して Office 用 VSTO アドインを作成する
description: Visual Studio の Microsoft Office Developer Tools を使用して、Office を拡張する .NET Framework アプリケーションを作成する方法について説明します。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 611feb69dc4c5ebdd340a61c49e76e0d7c33e713
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99947959"
---
# <a name="create-vsto-add-ins-for-office-by-using-visual-studio"></a>Visual Studio を使用して Office 用 VSTO アドインを作成する
  Visual Studio の Microsoft Office Developer Tools を使用して、Office を拡張する .NET Framework アプリケーションを作成できます。 このようなアプリケーションは、 *Office ソリューション* とも呼ばれます。

 Office Developer Tools で提供される機能は、さまざまなビジネス要件に合った Office ソリューションを作成するのに役立ちます。 このツールには、Visual Basic または Visual C# を使用した Office ソリューションの作成に役立つプロジェクト テンプレートや、Office ソリューションで使用するカスタム ユーザー インターフェイスの作成に役立つビジュアルなデザイナーが含まれています。

[!include[Add-ins note](includes/addinsnote.md)]

 Office 開発の最新情報については、「[Microsoft Office デベロッパー センター](https://developer.microsoft.com/office/docs)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
- [作業を始める &#40;Visual Studio での Office 開発&#41;](getting-started-office-development-in-visual-studio.md)

 Office ソリューションの作成用に開発コンピューターを構成する方法、Office ソリューションの作成を開始する方法、および Visual Studio での Office 開発を対象とする新機能に関する情報へのリンクを示します。

- [Office ソリューションのアップグレードと移行](upgrading-and-migrating-office-solutions.md)

 Visual Studio の以前のバージョンを使用して作成されたプロジェクトのアップグレード プロセスに関する情報へのリンクを示します。

- [Visual Studio の Office ソリューションのアーキテクチャ](architecture-of-office-solutions-in-visual-studio.md)

 ドキュメント レベルのカスタマイズと VSTO アドインに関する情報など、Office ソリューションの動作に関する情報へのリンクを示します。

- [Office ソリューションを設計して作成する](designing-and-creating-office-solutions.md)

 Visual Studio で Office プロジェクトを作成し、プロジェクトを構成する方法について説明します。

- [Office ソリューションを開発する](developing-office-solutions.md)

 Office ユーザー インターフェイスをカスタマイズする方法、データを処理する方法、問題のトラブルシューティングを行う方法など、Office ソリューションでマネージド コードを使用する方法について説明します。

- [Excel ソリューション](excel-solutions.md)

 Excel を自動化する方法、Excel ソリューションを作成する方法、および Excel に固有のグローバリゼーションに関する問題を理解する方法について説明します。

- [InfoPath ソリューション](infopath-solutions.md)

 InfoPath のフォーム テンプレートおよび VSTO アドインを作成する方法について説明します。

- [Outlook ソリューション](outlook-solutions.md)

 Outlook を自動化し、Outlook VSTO アドインおよびフォーム領域を作成する方法について説明します。

- [PowerPoint ソリューション](powerpoint-solutions.md)

 PowerPoint を自動化し、PowerPoint VSTO アドインを作成する方法について説明します。

- [Project ソリューション](project-solutions.md)

 Microsoft Office プロジェクトを自動化し、Project VSTO アドインを作成する方法について説明します。

- [Visio ソリューション](visio-solutions.md)

 Visio を自動化し、Visio VSTO アドインを作成する方法について説明します。

- [Word ソリューション](word-solutions.md)

 Word を自動化し、Word ソリューションを作成する方法について説明します。

- [Office ソリューションのビルド](building-office-solutions.md)

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]における、Office プロジェクトのビルドと、その他の種類のプロジェクトのビルドとの間の相違点について説明します。

- [Office プロジェクトのデバッグ](debugging-office-projects.md)

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]における、Office プロジェクトのデバッグと、その他の種類のプロジェクトのデバッグとの間の相違点について説明します。

- [Office ソリューションをセキュリティで保護する](securing-office-solutions.md)

 Office ソリューションにおけるセキュリティ機能のしくみについて説明します。

- [Office ソリューションを配置する](deploying-an-office-solution.md)

 Office ソリューションをユーザーが使用できるようにする方法、および配置方法を選択するときに考慮する主な問題点について説明します。

- [Office 開発のサンプルとチュートリアル](office-development-samples-and-walkthroughs.md)

 サンプル アプリケーション、および一般的なタスクの詳細な手順を説明するトピックへのリンクを示します。

- [全般リファレンス &#40;Visual Studio での Office 開発&#41;](general-reference-office-development-in-visual-studio.md)

 Office プライマリ相互運用機能アセンブリ、マニフェスト、ユーザー インターフェイス要素、およびエラー メッセージに関する詳細情報へのリンクを示します。

- [マネージド リファレンス &#40;Visual Studio での Office 開発&#41;](managed-reference-office-development-in-visual-studio.md)

 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]を対象とする Office プロジェクトで使用される API の名前空間と型に関する情報へのリンクを示します。 .NET Framework 3.5 を対象とする Office プロジェクトで使用される名前空間と型に関する API リファレンス ドキュメントについては、Visual Studio 2008 ドキュメントのリファレンス セクション「[2007 system マネージド参照](managed-reference-office-development-in-visual-studio.md)」をご覧ください。

- [アンマネージド API リファレンス &#40;Visual Studio での Office 開発&#41;](unmanaged-api-reference-office-development-in-visual-studio.md)

 Office アプリケーションでマネージド VSTO アドインのロードとアンロードなどの操作を実行するために使用できる COM インターフェイスに関する情報へのリンクを示します。

## <a name="related-sections"></a>関連項目
- [Visual Studio での Office 開発に関する開発者向けポータル](https://developer.microsoft.com/office/docs) 技術記事、ビデオ、ブログなど、その他のリソースを提供します。

- [Visual Studio デベロッパー センター](https://visualstudio.microsoft.com/) 技術記事、ビデオ、ブログなど、Visual Studio に関するその他のリソースを提供します。

- [MSDN ライブラリの Microsoft Office 開発に関するセクション](/previous-versions/office/office-12/bb726434(v=office.12)) この MSDN ライブラリの領域では、Office の複数のバージョンを対象とするソリューションの開発に関する記事やリファレンス ドキュメントを参照できます (Visual Studio を使用した Office 開発以外のトピックも含まれています)。

- [Visual Studio でのアプリケーション開発](/previous-versions/h8w79z10(v=vs.140)) Visual Studio を使用して、Web アプリケーション、XML Web サービス、および従来のクライアント アプリケーションを設計、開発、デバッグ、および配置する方法に関するトピックへのリンクを示します。

- [Visual Studio での .NET Framework プログラミング](/previous-versions/visualstudio/visual-studio-2010/k1s94fta(v=vs.100)) Visual Basic および Visual C# での .NET Framework を使用したアプリケーション開発について説明します。