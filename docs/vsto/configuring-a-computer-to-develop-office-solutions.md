---
title: Office ソリューションを開発できるようにコンピューターを構成する
description: Visual Studio、.NET Framework、Microsoft Office のサポートされているバージョンをインストールして、Microsoft Office の VSTO アドインとカスタマイズを作成できるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, installing tools
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ee8f840aa81d3decfdb96dd2658b758704443347
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910566"
---
# <a name="configure-a-computer-to-develop-office-solutions"></a>Office ソリューションを開発できるようにコンピューターを構成する

Microsoft Office の VSTO アドインおよびカスタマイズを作成するには、Visual Studio、.NET Framework、Microsoft Office のサポートされているバージョンをインストールします。

|ソフトウェア|サポートされているバージョン|
|--------------|------------------------|
|Visual Studio 2017| **Office/SharePoint 開発** ワークロードを含む任意のエディション。|
|.NET Framework|.NET Framework 4 以降。|
|Microsoft Office|<ul><li>エンタープライズ向け Microsoft 365 アプリを含む Office の任意のスイート エディション。</li><li>次のいずれかのスタンドアロン アプリケーション:<br /><br /> <ul><li>Excel</li><li>InfoPath (Office 2013 および Office 2010 のみ)</li><li>Outlook</li><li>PowerPoint</li><li>Project</li><li>Visio</li><li>Word</li></ul></li></ul><br /> Visual Basic for Applications (VBA) は Office の一部としてインストールされている必要があります。 **重要:** Office 2010 アプリケーションのクイック実行バージョンはサポートされていません。|

インストール手順の詳細については、「[方法: Office ソリューションを開発できるようにコンピューターを構成する](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)」を参照してください。

## <a name="if-project-templates-dont-appear-or-they-dont-work-in-visual-studio"></a>プロジェクト テンプレートが表示されない、または Visual Studio で機能しない場合

Visual Studio、.NET Framework、および Microsoft Office のサポートされているバージョンをインストールしても、Visual Studio の **[新しいプロジェクト]** ダイアログ ボックスに Office プロジェクト テンプレートが表示されない、またはプロジェクト テンプレートの使用を試みるとエラーが表示される場合は、以下のことを確認してください。

- 使用するコンピューターに Microsoft Office Developer Tools がインストールされていることを確認します。

     Office Developer Tools は Visual Studio のオプション コンポーネントですが、通常は Visual Studio と共に自動的にインストールされます。 インストールする機能を指定して Visual Studio のインストールをカスタマイズする場合は、各種ツールをインストールするために、セットアップ時に必ず **[Microsoft Office Developer Tools]** を選択してください。

     これらのツールがインストールされていることを確認するには、Visual Studio のセットアップ プログラムを開始し、 **[変更]** ボタンをクリックします。 **[Microsoft Office Developer Tools]** チェック ボックスをオンにして **[更新]** ボタンをクリックします。

- クイック実行で提供された Office のバージョンを実行していないことを確認します。 「[方法: コンピューター上の Outlook がクイック実行アプリケーションかどうかを検証する](/previous-versions/office/developer/office-2010/ff864733(v=office.14))」をご覧ください。

- Microsoft Office の 1 つのバージョンのみを実行していることを確認します。

問題が解決しない場合は、「[Office ソリューションのエラーについての追加サポート](../vsto/additional-support-for-errors-in-office-solutions.md)」をご覧ください。

## <a name="see-also"></a>関連項目
- [はじめに &#40;Visual Studio での Office 開発&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [方法: Office ソリューションを開発できるようにコンピューターを構成する](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [方法: Visual Studio Tools for Office の再頒布可能なランタイムをインストールする](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)
- [方法: Office のプライマリ相互運用機能アセンブリをインストールする](../vsto/how-to-install-office-primary-interop-assemblies.md)
- [Office アプリケーションとプロジェクト タイプ別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)