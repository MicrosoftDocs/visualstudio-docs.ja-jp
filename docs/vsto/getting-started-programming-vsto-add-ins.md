---
title: VSTO アドインのプログラミングの概要
description: VSTO アドインを使用して、Microsoft Office アプリケーションを自動化し、アプリケーションの機能を拡張し、アプリケーションのユーザー インターフェイスをカスタマイズする方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 04/28/2021
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.Outlook
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], getting started
- add-ins [Office development in Visual Studio], getting started
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1757dd6042536b6a042e67a8b3dcd9b12a2ea758
ms.sourcegitcommit: 9cb0097c33755a3e5cbadde3b0a6e9e76cee727d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2021
ms.locfileid: "109848293"
---
# <a name="get-started-programming-vsto-add-ins"></a>VSTO アドインのプログラミングの概要
> [!IMPORTANT]
> VSTO は [.NET Framework](https://docs.microsoft.com/dotnet/framework/get-started/overview) に依存しています。 COM アドインも .NET Framework を使用して記述することができます。 Office アドインは、[.NET Core と .NET 5+](https://docs.microsoft.com/dotnet/core/dotnet-five) (.NET の最新バージョン) では作成できません。 これは、.NET Core と .NET 5+ を .NET Framework と同じプロセスで動作させることができず、アドインの読み込みエラーが発生する可能性があるためです。 引き続き .NET Framework を使用して、Office 用の VSTO アドインと COM アドインを記述できます。 Microsoft が VSTO または COM アドイン プラットフォームを、.NET Core または .NET 5+ を使用するように更新することはありません。 .NET Core と .NET 5+ (ASP.NET Core を含む) を利用して、[Office Web アドイン](https://docs.microsoft.com/office/dev/add-ins/overview/office-add-ins)のサーバー側を作成できます。

  VSTO アドインを使用することにより、Microsoft Office アプリケーションを自動化し、アプリケーションの機能を拡張できるほか、アプリケーションのユーザー インターフェイス (UI) をカスタマイズすることもできます。 VSTO アドインと、Visual Studio を使用して作成できる他の種類の Office ソリューションの比較方法については、「[Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)」を参照してください。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

## <a name="create-vsto-add-in-projects"></a>VSTO アドイン プロジェクトを作成する
 VSTO アドイン プロジェクトを作成するには、 **[新しいプロジェクト]** ダイアログ ボックスにある VSTO アドイン プロジェクト テンプレートのいずれかを使用します。 これらのテンプレートには必要なアセンブリ参照とプロジェクト ファイルが含まれています。 Visual Studio には、Office のほとんどのアプリケーション用の VSTO アドイン プロジェクト テンプレートが用意されています。

 VSTO アドイン プロジェクトを作成する方法の詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。 これらのプロジェクト テンプレートの詳細については、「[Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。

## <a name="develop-vsto-add-in-projects"></a>VSTO アドイン プロジェクトを開発する
 VSTO アドイン プロジェクトを作成すると、Visual Studio によって *ThisAddIn.vb* ([!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] の場合) または *ThisAddIn.cs* (C# の場合) というコード ファイルが自動的に作成されます。 このファイルには、VSTO アドインの基礎となる `ThisAddIn` クラスが含まれています。 このクラスのメンバーを使用して、VSTO アドインが読み込まれたとき、またはアンロードされたときにコードを実行したり、ホスト アプリケーションのオブジェクト モデルにアクセスしたりすることができます。また、アプリケーションの機能を拡張することも可能です。 詳細については、「[VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)」を参照してください。

## <a name="automate-applications-by-using-the-object-models"></a>オブジェクト モデルを使用してアプリケーションを自動化する
 Microsoft Office アプリケーションのオブジェクト モデルは、VSTO アドインでプログラミングに使用できる多くの型を公開します。 それらの型を使用してアプリケーションを自動化できます。 たとえば、Outlook でプログラムによって電子メールを作成および送信することもできれば、Word で文書を開き、コンテンツを追加することも可能です。 コードでホスト アプリケーションのオブジェクト モデルにアクセスする方法の詳細については、「[VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)」を参照してください。

 特定の Microsoft Office アプリケーションのオブジェクト モデルの詳細については、以下のトピックを参照してください。

- [Excel オブジェクト モデルの概要](../vsto/excel-object-model-overview.md)

- [Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)

- [Outlook オブジェクト モデルの概要](../vsto/outlook-object-model-overview.md)

- [InfoPath ソリューション](../vsto/infopath-solutions.md)

- [PowerPoint ソリューション](../vsto/powerpoint-solutions.md)

- [Project ソリューション](../vsto/project-solutions.md)

- [Visio オブジェクト モデルの概要](../vsto/visio-object-model-overview.md)

## <a name="customize-the-user-interface-of-applications"></a>アプリケーションのユーザー インターフェイスをカスタマイズする
 VSTO アドインを使用してホスト アプリケーションの UI をカスタマイズするためのさまざまな方法があります。

- Excel や Word の場合、ドキュメントにマネージド コントロールを追加できます。 詳細については、「[実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

- アプリケーションでサポートされている場合は、リボンをカスタマイズできます。 詳細については、「[リボンの概要](../vsto/ribbon-overview.md)」を参照してください。

- アプリケーションでサポートされている場合は、カスタム作業ウィンドウを作成できます。 詳細については、「[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

- Outlook では、カスタム フォーム領域を作成できます。 詳細については、「[Outlook フォームの領域を作成する](../vsto/creating-outlook-form-regions.md)」を参照してください。

- すべての Microsoft Office アプリケーションで、VSTO アドインに Windows フォームを表示できます。

  Microsoft Office アプリケーションの UI をカスタマイズする方法の詳細については、「[Office UI のカスタマイズ](../vsto/office-ui-customization.md)」を参照してください。

## <a name="next-steps"></a>次の手順
 VSTO アドインの作成方法については、次のチュートリアルを参照してください。

- [チュートリアル : 初めての Excel 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)

- [チュートリアル : 初めての Outlook 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)

- [チュートリアル : 初めての PowerPoint 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)

- [チュートリアル : 初めての Project 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)

- [チュートリアル : 初めての Word 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)

  これらのチュートリアルでは、Visual Studio の Office 開発ツール、および VSTO アドインのプログラミング モデルを紹介します。

  Office プロジェクトの一般的なタスクが解説されているトピックの一覧については、「[Office プログラミングの共通タスク](../vsto/common-tasks-in-office-programming.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [はじめに &#40;Visual Studio での Office 開発&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office ソリューションでコードを書く](../vsto/writing-code-in-office-solutions.md)
- [Architecture of VSTO Add-Ins](../vsto/architecture-of-vsto-add-ins.md)
- [VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)
