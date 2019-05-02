---
title: VSTO アドインのプログラミングを始める
ms.date: 02/02/2017
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7b709012dafe0db3dcc0959908a1e6b4d9e07e21
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788783"
---
# <a name="get-started-programming-vsto-add-ins"></a>VSTO アドインのプログラミングを始める
  VSTO アドインを使用することにより、Microsoft Office アプリケーションを自動化し、アプリケーションの機能を拡張できるほか、アプリケーションのユーザー インターフェイス (UI) をカスタマイズすることもできます。 Visual Studio を使用して作成できる他の種類の Office ソリューションに VSTO アドインの比較については、次を参照してください。 [Office ソリューション開発の概要&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)します。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

## <a name="create-vsto-add-in-projects"></a>VSTO アドイン プロジェクトを作成します。
 VSTO アドイン プロジェクト テンプレートのいずれかを使用して VSTO アドイン プロジェクトを作成、**新しいプロジェクト** ダイアログ ボックス。 これらのテンプレートには必要なアセンブリ参照とプロジェクト ファイルが含まれています。 Visual Studio には、Office のほとんどのアプリケーション用の VSTO アドイン プロジェクト テンプレートが用意されています。

 VSTO アドイン プロジェクトを作成する方法の詳細については、次を参照してください。[方法。Visual Studio で Office プロジェクトを作成する方法](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。 プロジェクト テンプレートの詳細については、「[Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。

## <a name="develop-vsto-add-in-projects"></a>VSTO アドイン プロジェクトを開発します。
 VSTO アドイン プロジェクトを作成すると、Visual Studio は自動的に作成、 *ThisAddIn.vb* (で[!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]) または*ThisAddIn.cs*コード ファイル (で C# の場合)。 このファイルが含まれています、`ThisAddIn`クラスを VSTO アドインの基盤を提供します。 このクラスのメンバーを使用して、VSTO アドインが読み込まれたとき、またはアンロードされたときにコードを実行したり、ホスト アプリケーションのオブジェクト モデルにアクセスしたりすることができます。また、アプリケーションの機能を拡張することも可能です。 詳細については、次を参照してください。[プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)します。

## <a name="automate-applications-by-using-the-object-models"></a>オブジェクト モデルを使用してアプリケーションを自動化します。
 Microsoft Office アプリケーションのオブジェクト モデルは、VSTO アドインでプログラミングに使用できる多くの型を公開します。 それらの型を使用してアプリケーションを自動化できます。 たとえば、Outlook でプログラムによって電子メールを作成および送信することもできれば、Word で文書を開き、コンテンツを追加することも可能です。 コードでは、ホスト アプリケーションのオブジェクト モデルにアクセスする方法の詳細については、次を参照してください。[プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)します。

 特定の Microsoft Office アプリケーションのオブジェクト モデルの詳細については、以下のトピックを参照してください。

- [Excel オブジェクト モデルの概要](../vsto/excel-object-model-overview.md)

- [Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)

- [Outlook オブジェクト モデルの概要](../vsto/outlook-object-model-overview.md)

- [InfoPath ソリューション](../vsto/infopath-solutions.md)

- [PowerPoint ソリューション](../vsto/powerpoint-solutions.md)

- [Project ソリューション](../vsto/project-solutions.md)

- [Visio オブジェクト モデルの概要](../vsto/visio-object-model-overview.md)

## <a name="customize-the-user-interface-of-applications"></a>アプリケーションのユーザー インターフェイスをカスタマイズします。
 VSTO アドインを使用して、ホスト アプリケーションの UI をカスタマイズするいくつかのさまざまな方法はあります。

- Excel や Word の場合、ドキュメントにマネージド コントロールを追加できます。 詳細については、次を参照してください。[拡張 Word 文書や Excel ブックを実行時に VSTO アドインで](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)します。

- アプリケーションでサポートされている場合は、リボンをカスタマイズできます。 詳細については、次を参照してください。[リボンの概要](../vsto/ribbon-overview.md)します。

- アプリケーションでサポートされている場合は、カスタム作業ウィンドウを作成できます。 詳細については、次を参照してください。[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)します。

- Outlook では、カスタム フォーム領域を作成できます。 詳細については、次を参照してください。[作成の Outlook フォーム領域](../vsto/creating-outlook-form-regions.md)します。

- すべての Microsoft Office アプリケーションで、VSTO アドインに Windows フォームを表示できます。

  Microsoft Office の UI アプリケーションをカスタマイズする方法の詳細については、次を参照してください。 [Office UI のカスタマイズ](../vsto/office-ui-customization.md)します。

## <a name="next-steps"></a>次の手順
 VSTO アドインの作成方法については、次のチュートリアルを参照してください。

- [チュートリアル: Excel 用の最初の VSTO アドインの作成します。](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)

- [チュートリアル: 初めて VSTO アドイン Outlook の作成します。](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)

- [チュートリアル: Powerpoint の場合、最初の VSTO アドインの作成します。](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)

- [チュートリアル: 初めて VSTO アドイン プロジェクトの作成します。](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)

- [チュートリアル: Word 用の最初の VSTO アドインの作成します。](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)

  これらのチュートリアルでは、Visual Studio の Office 開発ツール、および VSTO アドインのプログラミング モデルを紹介します。

  Office プロジェクトで、一般的なタスクを解説しているトピックの一覧は、次を参照してください。 [Office プログラミングで一般的なタスク](../vsto/common-tasks-in-office-programming.md)します。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio での Office プロジェクトを作成します。](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [はじめに &#40;Visual Studio での Office 開発&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [Office ソリューションにおけるコードの記述](../vsto/writing-code-in-office-solutions.md)
- [VSTO アドインのアーキテクチャ](../vsto/architecture-of-vsto-add-ins.md)
- [VSTO アドインをプログラミングします。](../vsto/programming-vsto-add-ins.md)
