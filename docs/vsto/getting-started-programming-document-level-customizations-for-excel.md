---
title: 'Excel: ドキュメント レベルのカスタマイズのプログラミングの概要'
description: Visual Studio を使用して Microsoft Office Excel のドキュメント レベルのカスタマイズの作成を始めるために知っておく必要があることについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel solutions in Visual Studio
- Excel projects [Office development in Visual Studio], getting started
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: de5d7529e0bd8bc99eb4f375a31dab9ea9520234
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860725"
---
# <a name="get-started-programming-document-level-customizations-for-excel"></a>Excel のドキュメント レベルのカスタマイズのプログラミングの概要
  Visual Studio を使用して Microsoft Office Excel のドキュメント レベルのカスタマイズの作成を始める場合は、次のことを理解しておく必要があります。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="understand-how-document-level-customizations-for-excel-work"></a>Excel のドキュメント レベルのカスタマイズのしくみについて理解する
 Excel のドキュメント レベルのカスタマイズは、1 つのブックに基づいています。 エンド ユーザーがカスタマイズを使い始めるには、ブックを開くか、Excel テンプレートからブックを作成します。 ブックでのイベント (たとえば、セルへの入力や、ボタンやメニュー項目のクリックなど) で、アセンブリ内のイベント処理メソッドを呼び出すことができます。 ブックを閉じると、カスタマイズによって提供される機能は Excel で使用できなくなります。これらの機能は、それが含まれるドキュメント内でのみ使用できます。

 詳細については、「[ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)」を参照してください。

## <a name="create-document-level-projects-for-excel"></a>Excel 用のドキュメント レベルのプロジェクトを作成する
 Excel のドキュメント レベルのカスタマイズを作成するには、 **[新しいプロジェクト]** ダイアログ ボックスで Excel ブックまたは Word テンプレートのプロジェクト テンプレートを使用します。 これらのテンプレートには必要なアセンブリ参照とプロジェクト ファイルが含まれています。

 Excel 用のドキュメント レベル プロジェクトを作成する方法の詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。 これらのプロジェクト テンプレートの詳細については、「[Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。

## <a name="program-excel-workbooks-by-using-host-items-and-host-controls"></a>ホスト項目とホスト コントロールを使用して Excel ブックをプログラミングする
 "*ホスト項目*" と "*ホスト コントロール*" は、Visual Studio を使用して作成されたドキュメント レベルのカスタマイズ用のプログラミング モデルを提供するクラスです。

 ホスト項目は、コードのエントリ ポイントを提供し、ホスト コントロールと Windows フォーム コントロール用のコンテナーとしても機能します。 Excel 用のドキュメント レベルのプロジェクトでは、これらのホスト項目は、`ThisWorkbook`、`Sheet1`、`Sheet2`、`Sheet3` の各クラスによって表されます。

 ホスト コントロールは、リスト オブジェクトや範囲など、Excel のネイティブ オブジェクトに基づいています。 ホスト コントロールは、Excel のネイティブ オブジェクトと同様の機能を提供しますが、新しいイベント、デザイナー サポート、データ バインディング機能も備えています。 それらは、プロジェクト コードと IntelliSense でファーストクラス オブジェクトとして表示されるので、Excel オブジェクト モデル内を移動する必要はなく、コード内で特定のオブジェクトを簡単に直接参照できます。

 詳細については、次のトピックを参照してください。

- [プログラムのドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)

- [拡張オブジェクトを使用して Excel を自動化する](../vsto/automating-excel-by-using-extended-objects.md)

- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)

## <a name="customize-the-user-interface-of-excel"></a>Excel のユーザー インターフェイスをカスタマイズする
 ユーザーがソリューションと対話する何らかの手段を提供するため、ほとんどの Microsoft Office ソリューションにおいて、Office アプリケーションのユーザー インターフェイス (UI) が変更されます。 ドキュメント レベルのカスタマイズを使用して Excel の UI を変更するには、さまざまな方法があります。 たとえば、リボンにコントロールを追加したり、操作ウィンドウを表示したりすることができます。 詳細については、「[Office UI のカスタマイズ](../vsto/office-ui-customization.md)」を参照してください。

 また、プロジェクトに関連付けられているブックを Visual Studio で直接開くこともできます。 ブックを Visual Studio で開くと、Excel のユーザー インターフェイスを使用してブックを変更できます。 ブックをデザイン サーフェイスとして使用することもでき、コントロールをワークシートにドラッグできます。 詳細については、「[Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)」を参照してください。

## <a name="use-data-binding"></a>データ バインディングを使用する
 ホスト コントロールは、 **[データ ソース]** ウィンドウからドラッグできるコントロールの一覧にも含まれます。 この方法でホスト コントロールを追加すると、ウィンドウを使用して設定したデータ ソースに自動的にバインドされます。 コードを記述しなくても、データベース、Web サービス、ビジネス オブジェクトのデータを表示できます。 詳細については、「[Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

## <a name="next-steps"></a>次のステップ
 Excel のドキュメント レベルのカスタマイズを作成する方法については、「[チュートリアル: Excel のドキュメント レベルのカスタマイズを初めて作成する](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)」を参照してください。 このチュートリアルでは、Visual Studio の Office 開発ツールと、Excel のドキュメント レベルのカスタマイズのプログラミング モデルについて説明されています。

 Excel プロジェクトの一般的なタスクが解説されているトピックの一覧については、「[Office プログラミングの共通タスク](../vsto/common-tasks-in-office-programming.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [プログラムのドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)
- [Excel ソリューション](../vsto/excel-solutions.md)
- [チュートリアル: Excel のドキュメント レベルのカスタマイズを初めて作成する](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)
- [Excel を使用したチュートリアル](../vsto/walkthroughs-using-excel.md)
- [Excel オブジェクト モデルの概要](../vsto/excel-object-model-overview.md)
- [Office ソリューションでコードを書く](../vsto/writing-code-in-office-solutions.md)
