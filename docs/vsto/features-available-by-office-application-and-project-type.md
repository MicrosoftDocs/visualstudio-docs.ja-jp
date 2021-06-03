---
title: Office アプリケーションとプロジェクト タイプ別の使用可能な機能
description: Visual Studio に、Microsoft Office アプリケーションのさまざまなビジネス シナリオをサポートするプロジェクト テンプレートがいくつか用意されていることについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio]
- Office development in Visual Studio, features
- Ribbon [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], features available
- document-level customizations [Office development in Visual Studio]
- Office projects [Office development in Visual Studio], features available
- add-ins [Office development in Visual Studio]
- form regions [Office development in Visual Studio], features available
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 05a17b373f409e91f9360cbd3ba92f88bd3f48e8
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99970401"
---
# <a name="features-available-by-office-application-and-project-type"></a>Office アプリケーションとプロジェクト タイプ別の使用可能な機能
  Visual Studio には、次のように、Microsoft Office アプリケーションのさまざまなビジネス シナリオをサポートするプロジェクト テンプレートがいくつか用意されています。

- ドキュメントレベルのカスタマイズ。

- VSTO アドイン。

  すべてのプロジェクトの種類を使用できないアプリケーションもあります。 たとえば、ドキュメントレベルのプロジェクトは、Microsoft Office Word と Microsoft Office Excel でのみ使用できます。 同様に、一部の機能は、特定の種類のプロジェクトまたはアプリケーションでのみ使用できます。 たとえば、操作ウィンドウは、ドキュメントレベルのプロジェクトでのみ使用できます。また、リボンの拡張機能は、一部のアプリケーションでのみ使用できます。 さまざまな種類のプロジェクトの詳細については、「[Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)」を参照してください。

> [!NOTE]
> Office プロジェクト テンプレートは、一部のエディションの [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] でのみ使用できます。 詳細については、「[Office ソリューションを開発できるようにコンピューターを構成する](../vsto/configuring-a-computer-to-develop-office-solutions.md)」を参照してください。

## <a name="project-types-available-for-different-microsoft-office-applications"></a>各 Microsoft Office アプリケーションで使用できるプロジェクトの種類
 プロジェクトの種類ごとに使用できるアプリケーションを次の表に示します。

|プロジェクトの種類|Microsoft Office アプリケーション|
|-------------------|----------------------------------|
|ドキュメント レベルのカスタマイズ|Excel<br /><br /> Word|
|VSTO アドイン|Excel<br /><br /> InfoPath (InfoPath 2013 と InfoPath 2010 のみ)<br /><br /> Outlook<br /><br /> PowerPoint<br /><br /> Project<br /><br /> Visio<br /><br /> Word<br /><br /> Excel|

## <a name="features-available-in-different-project-types"></a>各プロジェクトで使用できる機能
 プロジェクトの種類ごとに異なる機能を次の表に示します。

|機能|機能を提供するプロジェクトの種類|参考資料|
|-------------|--------------------------------------------|---------------------|
|[操作] ウィンドウ。|ドキュメントレベルのプロジェクト。|[操作ウィンドウの概要](../vsto/actions-pane-overview.md)|
|ClickOnce 配置。|VS およびドキュメントレベルのプロジェクト。|[Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)|
|カスタム作業ウィンドウ。|次のアプリケーション用の VSTO アドイン プロジェクト:<br /><br /> -   Excel<br />-   InfoPath (InfoPath 2013 と InfoPath 2010 のみ)<br />-   Outlook<br />-   PowerPoint<br />-   Word|[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)|
|カスタム XML 部分。|ドキュメントレベルのプロジェクト。<br /><br /> 次のアプリケーション用のアプリケーション レベルのプロジェクト:<br /><br /> -   Excel<br />-   PowerPoint<br />-   Word|[カスタム XML 部分の概要](../vsto/custom-xml-parts-overview.md)|
|データ キャッシュ。|ドキュメントレベルのプロジェクト。|[ドキュメント レベルのカスタマイズのキャッシュ データ](../vsto/cached-data-in-document-level-customizations.md)|
|VSTO アドインのオブジェクトを他の Microsoft Office ソリューションに公開します。|VSTO アドイン プロジェクト。|[他の Office ソリューションから VSTO アドインのコードを呼び出す](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)|
|次のホスト コントロール:<br /><br /> -   グラフ<br />-   ListObject<br />-   NamedRange<br />-   コンテンツ コントロール<br />-   ブックマーク|ドキュメントレベルのプロジェクト。<br /><br /> Word と Excel 用の VSTO アドイン プロジェクト。|[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)|
|次のホスト コントロール:<br /><br /> -   XMLMappedRange<br />-   XMLNode<br />-   XMLNodes|ドキュメントレベルのプロジェクト。|[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)|
|複数プロジェクトの配置。|ドキュメントレベルのプロジェクト。<br /><br /> VSTO アドイン プロジェクト。|[チュートリアル: 1 つの ClickOnce インストーラーで複数の Office ソリューションを配置する](/previous-versions/dd465290(v=vs.110))|
|Outlook フォーム領域。|Outlook 用の VSTO アドイン プロジェクト。|[Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)|
|配置後の動作。|ドキュメントレベルのプロジェクト。<br /><br /> VSTO アドイン プロジェクト。|[チュートリアル: ClickOnce のインストール後にドキュメントをエンド ユーザーのコンピューターにコピーする](/previous-versions/dd465291(v=vs.110))|
|リボンのカスタマイズ。|ドキュメントレベルのプロジェクト。<br /><br /> 次のアプリケーション用の VSTO アドイン プロジェクト:<br /><br /> -   Excel<br />-   InfoPath (InfoPath 2013 と InfoPath 2010 のみ)<br />-   Outlook<br />-   PowerPoint<br />-   Project<br />-   Visio<br />-   Word|[リボンの概要](../vsto/ribbon-overview.md)|
|視覚的なドキュメント デザイナー。|ドキュメントレベルのプロジェクト。|[Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)|

## <a name="see-also"></a>関連項目
- [作業を始める &#40;Visual Studio での Office 開発&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [リボンの概要](../vsto/ribbon-overview.md)
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ドキュメント レベルのカスタマイズのキャッシュ データ](../vsto/cached-data-in-document-level-customizations.md)
- [Office ソリューションを配置する](../vsto/deploying-an-office-solution.md)