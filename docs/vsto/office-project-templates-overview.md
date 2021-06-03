---
title: Office プロジェクト テンプレートの概要
description: Visual Studio の Microsoft Office Developer Tools には、さまざまの種類の Office ソリューションの作成に使用できるプロジェクト テンプレートが含まれていることを説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- templates [Office development in Visual Studio], about project templates
- Excel Workbook project template
- Word Template project template
- Excel [Office development in Visual Studio], project templates
- Project [Office development in Visual Studio], project templates
- project templates [Office development in Visual Studio]
- project templates, Word
- InfoPath [Office development in Visual Studio], project templates
- Excel Template project template
- project templates, 2007 Microsoft Office system
- project templates, Excel
- PowerPoint [Office development in Visual Studio], project templates
- Word [Office development in Visual Studio], Word project templates
- Office projects [Office development in Visual Studio], templates
- Excel projects in Visual Studio
- Word Document project template
- Visio [Office development in Visual Studio], project templates
- Word projects in Visual Studio
- Outlook [Office development in Visual Studio], project templates
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: af01bf165c823ce34957e4a9eba38ef90c5344a2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99892035"
---
# <a name="office-project-templates-overview"></a>Office プロジェクト テンプレートの概要
  Visual Studio の Microsoft Office Developer Tools には、次の種類の Office ソリューションの作成に使用できるプロジェクト テンプレートが含まれています。

- [ドキュメント レベルのカスタマイズ](#DocLevel)

- [VSTO アドイン](#AppLevel)

  これらの Office ソリューションの詳細な比較については、「[Office ソリューションの開発の概要 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)」を参照してください。

  Office プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログ ボックスの **[Visual C#]** 言語ノードおよび **[Visual Basic]** 言語ノードの下の **[Office]** ノードで使用できます。 各テンプレートでは、アセンブリ参照、デバッグ設定など、対象アプリケーションに適した構成を持つプロジェクトが生成されます。

  各プロジェクトには、特定の種類のソリューションの作成に使用できるファイルおよびコードが用意されています。 プロジェクトごとに生成されるコードには、スタートアップ イベントおよびシャットダウン イベントのハンドラーが含まれます。 これらのイベント ハンドラーにコードを追加して、読み込まれるときにはソリューションを初期化し、アンロードされるときにはソリューションをクリーンアップすることができます。 詳細については、「[Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)」および「[Office プロジェクトのイベント](../vsto/events-in-office-projects.md)」を参照してください。

> [!NOTE]
> Office 開発ツールは、Visual Studio の一部のエディションに付属しています。 詳細については、「[Office ソリューションを開発できるようにコンピューターを構成する](../vsto/configuring-a-computer-to-develop-office-solutions.md)」を参照してください。

## <a name="document-level-customizations"></a><a name="DocLevel"></a> ドキュメントレベルのカスタマイズ
 **[新しいプロジェクト]** ダイアログ ボックスの **[Office]** ノードには、Word および Excel のドキュメント レベルのカスタマイズの作成に使用できる次のプロジェクト テンプレートが用意されています。

- **Word 2013 および 2016 VSTO ドキュメント**

- **Word 2013 および 2016 VSTO テンプレート**

- **Excel 2013 および 2016 VSTO ブック**

- **Excel 2013 および 2016 VSTO テンプレート**

- **Word 2010 VSTO ドキュメント**

- **Word 2010 VSTO テンプレート**

- **Excel 2010 VSTO ブック**

- **Excel 2010 VSTO テンプレート**

  Word ドキュメントと Excel ブックのプロジェクト テンプレートには、特定の文書またはブックに基づくソリューションを作成するためのコードが用意されています。 これらの種類のソリューションでは、関連付けられたドキュメントが Word または Excel で開かれている場合にのみコードが実行されます。

  Word テンプレートと Excel テンプレートのプロジェクト テンプレートは、Word ドキュメントと Excel ブックのプロジェクト テンプレートと同様に動作します。 Word テンプレートと Excel テンプレートのプロジェクト テンプレートを活用すると、ソリューション内のカスタマイズされたテンプレートに基づいてローカルなドキュメントまたはブックを新しく作成するのが容易になります。 ユーザーがテンプレートに基づいて新しく作成するドキュメントでは、ソリューションの機能を利用できます。

> [!NOTE]
> マネージド コード拡張機能を参照する Word テンプレートは、グローバル VSTO アドインとして使用できません。Word のスタートアップ ディレクトリからテンプレートが読み込まれる場合、アセンブリは呼び出されません。 詳細については、「[グローバル テンプレートと Excel アドイン (.xla ファイル) に関する制限事項](#Limitations)」を参照してください。

 これらのプロジェクトの種類を使用して作業を開始する場合の詳細については、次のトピックを参照してください。

- [ドキュメント レベルのカスタマイズのプログラミング](../vsto/programming-document-level-customizations.md)

- [Word ソリューション](../vsto/word-solutions.md)

- [Excel ソリューション](../vsto/excel-solutions.md)

- [チュートリアル: Word のドキュメント レベルのカスタマイズを初めて作成する](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)

- [チュートリアル: Excel のドキュメント レベルのカスタマイズを初めて作成する](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)

## <a name="vsto-add-ins"></a><a name="AppLevel"></a> VSTO アドイン
 **[新しいプロジェクト]** ダイアログ ボックスの **[Office/SharePoint]** ノードには、VSTO アドインの作成に使用できる次のプロジェクト テンプレートが用意されています。

- **Excel 2013 および 2016 VSTO アドイン**

- **InfoPath 2013 VSTO アドイン**

- **Outlook 2013 および 2016 VSTO アドイン**

- **PowerPoint 2013 および 2016 アドイン**

- **Project 2013 および 2016 アドイン**

- **Visio 2013 および 2016 アドイン**

- **Word 2013 および 2016 アドイン**

- **Excel 2010 アドイン**

- **InfoPath 2010 アドイン**

- **Outlook 2010 アドイン**

- **PowerPoint 2010 アドイン**

- **Project 2010 アドイン**

- **Visio 2010 アドイン**

- **Word 2010 アドイン**

  これらのプロジェクト テンプレートのいずれかに基づくプロジェクトを作成する場合、ソリューションのコードは、関連付けられたアプリケーションが開いているときに実行されます。 ドキュメント レベルのプロジェクトとは異なり、コードは 1 つのドキュメントに関連付けられません。

  これらのプロジェクトの種類を使用して作業を開始する場合の詳細については、次のトピックを参照してください。

- [VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)

- [VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)

- [チュートリアル: 初めての Excel 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)

- [チュートリアル: 初めての Outlook 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)

- [チュートリアル: 初めての PowerPoint 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)

- [チュートリアル: 初めての Project 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)

- [チュートリアル: 初めての Word 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)

## <a name="document-vs-template-solutions"></a>ドキュメントとテンプレート ソリューション
 Word 文書または Excel ブックのソリューションをデザインする場合は、その文書をユーザーが使用できるようにするための最善の方法を決定する必要があります。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 文書のコピーを各ユーザーに配布する場合には、 Excel または Word のドキュメント プロジェクトを使用してソリューションを作成します。

 テンプレートをサーバーから利用できるようにすることで、各ユーザーがテンプレートを開いて、ローカル コピーを文書として保存できるようにする場合には、 Excel または Word のテンプレート プロジェクトを使用してソリューションを作成します。

## <a name="comparison"></a>比較
 文書とテンプレートの違いについて、次の表に示します。

|ドキュメント|テンプレート|
|---------------|---------------|
|読み取り専用に設定されていない場合、ユーザーは文書を開いて変更できます。 保存した変更はすべて、元の文書に保存されます。|ユーザーは、テンプレートを開いて、新しい文書としてローカル コピーを作成できます。 特別なアクセス許可が与えられていない限り、元のテンプレートを変更することはできません。|
|文書を開くと、 <xref:Microsoft.Office.Tools.Word.Document.Open> イベントが呼び出されます。|テンプレートを開くと、 <xref:Microsoft.Office.Tools.Word.Document.New> イベントが呼び出されます。|

## <a name="limitations-of-global-templates-and-excel-add-ins-xla-files"></a><a name="Limitations"></a> グローバル テンプレートと Excel アドイン (.xla ファイル) に関する制限事項
 ドキュメント、ブック、およびテンプレートは、グローバル テンプレートや Excel VSTO アドイン (.xla ファイル) として正常に機能しないことがあります。

## <a name="word-templates"></a>Word テンプレート
 Microsoft Office Word テンプレートにマネージド コード拡張機能が組み込まれていると、テンプレートがグローバル テンプレートに割り当てられている場合、または Word のスタートアップ ディレクトリから読み込まれた場合でも、プロジェクト アセンブリは呼び出されません。 また、ドキュメントは Office ソリューションの一部であるテンプレートの形式を認識しません。

## <a name="excel-add-ins-xla-files"></a>Excel アドイン (.xla ファイル)
 Excel VSTO アドイン ( *.xla* ファイル) を作成するための Office プロジェクトは存在しません。 ブックを .xla ファイルとして保存できますが、サポートされていない操作であり、推奨できません。 マネージド コード拡張機能が組み込まれているブックを **[Microsoft Office Excel アドイン (\*.xla)]** ファイルとして保存すると、 **[アドイン]** ダイアログ ボックスで選択して別のブックに適用できます。 VSTO アドインの適用後に対象のブックでコードが実行されることもありますが、このような Office ソリューションの使用方法はサポートされていません。

## <a name="see-also"></a>関連項目
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
- [Office ソリューションを開発する](../vsto/developing-office-solutions.md)
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Excel のドキュメント レベルのカスタマイズのプログラミングの概要](../vsto/getting-started-programming-document-level-customizations-for-excel.md)
- [Word のドキュメント レベルのカスタマイズのプログラミングの概要](../vsto/getting-started-programming-document-level-customizations-for-word.md)
- [VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)
