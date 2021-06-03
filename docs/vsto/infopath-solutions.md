---
title: InfoPath ソリューション
description: Visual Studio を使用して、Microsoft Office InfoPath 2013 および InfoPath 2010 の VSTO アドインを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], InfoPath
- templates [Office development in Visual Studio], InfoPath
- InfoPath [Office development in Visual Studio]
- Office development in Visual Studio, InfoPath solutions
- projects [Office development in Visual Studio], InfoPath
- Office solutions [Office development in Visual Studio], InfoPath
- Office projects [Office development in Visual Studio], InfoPath
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b3feab4a4b66ed2d6cf96fbccc8aaf1fb7de3bb6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99962367"
---
# <a name="infopath-solutions"></a>InfoPath ソリューション
  Visual Studio には、Microsoft Office InfoPath 2013 および InfoPath 2010 の VSTO アドインの作成に使用できるプロジェクト テンプレートが用意されています。 InfoPath は、Office 2016 では使用できません。

> [!NOTE]
> Office 2016 をインストールしてある場合でも、InfoPath 用の VSTO アドインを作成することはできます。 InfoPath 2013 または Office 2013 を Office 2016 とサイドバイサイドにインストールするだけです。

 [!INCLUDE[appliesto_infoallapp](../vsto/includes/appliesto-infoallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 InfoPath 用の VSTO アドインは、他の Microsoft Office アプリケーションの VSTO アドインと似ています。 このようなソリューションは、アプリケーションが読み込むアセンブリで構成されます。 エンド ユーザーは、どのフォームまたはフォーム テンプレートが開いているかに関係なく、このアセンブリの機能にアクセスできます。 VSTO アドインの詳細については、「[VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)」および [VSTO アドインのアーキテクチャ](../vsto/architecture-of-vsto-add-ins.md)に関するページを参照してください。

> [!NOTE]
> Visual Studio 2015 には、以前のバージョンの Visual Studio で提供されていた InfoPath フォーム テンプレート プロジェクトは含まれていません。 また、Visual Studio 2015 を使用して、以前のバージョンの Visual Studio で作成した InfoPath フォーム テンプレート プロジェクトを開いて編集することもできません。 ただし、Visual Studio Tools for Applications を使用すると、InfoPath フォーム テンプレート プロジェクトを開いて編集できます。 詳しくは、[InfoPath 2010 での VSTO 2008 プロジェクトの使用](/archive/blogs/infopath/working-with-vsto-2008-projects-in-infopath-2010)に関するページを参照してください。

## <a name="automate-infopath-by-using-an-add-in"></a>アドイン使用による InfoPath の自動化
 Visual Studio の Office 開発ツールを使用して作成した Office VSTO アドインから InfoPath オブジェクト モデルにアクセスするには、プロジェクトの `Application` クラスの `ThisAddIn` フィールドを使用します。 `Application` フィールドは InfoPath の現在のインスタンスを表す <xref:Microsoft.Office.Interop.InfoPath.Application> オブジェクトを返します。 詳細については、「[VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)」を参照してください。

 VSTO アドインから InfoPath オブジェクト モデルを呼び出すときには、InfoPath のプライマリ相互運用機能アセンブリに用意された型を使用します。 プライマリ相互運用機能アセンブリは、VSTO アドインのマネージド コードと InfoPath の COM オブジェクト モデルとの仲介役を果たします。 InfoPath プライマリ相互運用機能アセンブリ内の型は、すべて <xref:Microsoft.Office.Interop.InfoPath> 名前空間に定義されています。 InfoPath プライマリ相互運用機能アセンブリの詳細については、「[Microsoft Office InfoPath プライマリ相互運用機能アセンブリについて](/office/client-developer/infopath/external-automation/about-the-microsoft-office-infopath-primary-interop-assembly)」を参照してください。 プライマリ相互運用機能アセンブリ全般の詳細については、「[Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)」および「[Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)」を参照してください。

## <a name="customize-the-user-interface-of-infopath-by-using-an-add-in"></a>アドイン使用による InfoPath のユーザー インターフェイスのカスタマイズ
 InfoPath の VSTO アドインを作成するときには、さまざまな方法で UI をカスタマイズできます。 次の表は、主なカスタマイズ方法を示しています。

|タスク|詳細情報|
|----------|--------------------------|
|カスタム作業ウィンドウを作成する。|[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)|
|InfoPath のリボンにカスタム タブを追加する。|[InfoPath のリボンのカスタマイズ](../vsto/customizing-a-ribbon-for-infopath.md)|

 InfoPath およびその他の Microsoft Office アプリケーションの UI をカスタマイズする方法の詳細については、[Office UI のカスタマイズ](../vsto/office-ui-customization.md)に関するページを参照してください。

## <a name="see-also"></a>関連項目
- [Microsoft Office InfoPath プライマリ相互運用機能アセンブリについて](/office/client-developer/infopath/external-automation/about-the-microsoft-office-infopath-primary-interop-assembly)
- [VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)
- [Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [Architecture of VSTO Add-Ins](../vsto/architecture-of-vsto-add-ins.md)
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)
- [Office ソリューションでコードを書く](../vsto/writing-code-in-office-solutions.md)
- [Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [Office 開発における InfoPath 2010](/previous-versions/office/developer/office-2010/ff604966(v=office.14))