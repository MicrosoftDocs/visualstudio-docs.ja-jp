---
title: Word のドキュメント レベルのカスタマイズのプログラミングの概要
description: Visual Studio を使用して Microsoft Office Word のドキュメント レベルのカスタマイズの作成を始めるために知っておく必要があることについて説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word solutions in Visual Studio
- Word projects [Office development in Visual Studio], getting started
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ff19fd84b66b9d31ed806589044775e006ef7096
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860660"
---
# <a name="get-started-programming-document-level-customizations-for-word"></a>Word のドキュメント レベルのカスタマイズのプログラミングの概要
  Visual Studio を使用して Microsoft Office Word のドキュメント レベルのカスタマイズの作成を始める場合は、次のことを理解しておく必要があります。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

## <a name="understand-how-document-level-customizations-for-word-work"></a>Word のドキュメント レベルのカスタマイズのしくみについて理解する
 作成する Word の各カスタマイズは、1 つのドキュメントに基づいています。 エンド ユーザーがカスタマイズを使い始めるときは、ドキュメントを開くか、Word テンプレートからドキュメントを作成します。 ドキュメントでのイベント (たとえば、特定の領域へのカーソルの移動や、ボタンやメニュー項目のクリックなど) で、アセンブリ内のイベント処理メソッドを呼び出すことができます。 ドキュメントが閉じられると、カスタマイズによって提供される機能は Word で使用できなくなります。

 詳細については、「[ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)」を参照してください。

## <a name="create-document-level-projects-for-word"></a>Word 用のドキュメント レベルのプロジェクトを作成する
 Word のドキュメント レベルのカスタマイズを作成するには、 **[新しいプロジェクト]** ダイアログ ボックスで Word 文書または Word テンプレートのプロジェクト テンプレートを使用します。 これらのテンプレートには必要なアセンブリ参照とプロジェクト ファイルが含まれています。

 Word 用のドキュメント レベル プロジェクトを作成する方法の詳細については、「[方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)」を参照してください。 これらのプロジェクト テンプレートの詳細については、「[Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。

## <a name="program-word-documents-by-using-host-items-host-controls"></a>ホスト項目とホスト コントロールを使用して Word 文書をプログラミングする
 "*ホスト項目*" と "*ホスト コントロール*" は、ドキュメント レベルのカスタマイズ用のプログラミング モデルを提供するクラスです。

 ホスト項目は、コードのエントリ ポイントを提供し、ホスト コントロールと Windows フォーム コントロール用のコンテナーとしても機能します。 Word のドキュメント レベルのプロジェクトでは、ホスト項目は `ThisDocument` クラスによって表されます。

 ホスト コントロールは、コンテンツ コントロール、ブックマーク、XML ノードなどのネイティブな Word オブジェクトに基づいています。 ホスト コントロールは、Word のネイティブ オブジェクトと同様の機能を提供しますが、新しいイベント、デザイナー サポート、データ バインディング機能も備えています。 それらは、プロジェクト コードと IntelliSense でファーストクラス オブジェクトとして表示されるので、Word オブジェクト モデル内を移動する必要はなく、コード内で特定のオブジェクトを簡単に直接参照できます。

 詳細については、次のトピックを参照してください。

- [プログラムのドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)

- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)

- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)

## <a name="customize-the-user-interface-of-word"></a>Word のユーザー インターフェイスをカスタマイズする
 ユーザーがソリューションと対話する何らかの手段を提供するため、ほとんどの Microsoft Office ソリューションにおいて、Office アプリケーションのユーザー インターフェイス (UI) が変更されます。 ドキュメント レベルのカスタマイズを使用して Word の UI を変更するには、さまざまな方法があります。 たとえば、リボンにコントロールを追加したり、操作ウィンドウを表示したりすることができます。 詳細については、「[Office UI のカスタマイズ](../vsto/office-ui-customization.md)」を参照してください。

 また、プロジェクトに関連付けられているドキュメントを Visual Studio で直接開くこともできます。 ドキュメントを Visual Studio で開くと、Word のユーザー インターフェイスを使用してドキュメントを変更できます。 ドキュメントをデザイン サーフェイスとして使用することもでき、コントロールをその上にドラッグできます。 詳細については、「[Visual Studio 環境における Office プロジェクト](../vsto/office-projects-in-the-visual-studio-environment.md)」を参照してください。

## <a name="bind-controls-to-data"></a>データにコントロールをバインドする
 コンテンツ コントロールと <xref:Microsoft.Office.Tools.Word.Bookmark> コントロールは、 **[データ ソース]** ウィンドウからドラッグできるコントロールのリストに含まれています。 この方法でコンテンツ コントロールとブックマークを追加すると、ウィンドウを使用して設定したデータ ソースに自動的にバインドされます。 コードを記述しなくても、データベース、サービス、ビジネス オブジェクトのデータを表示できます。 詳細については、「[Office ソリューションのコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)」を参照してください。

## <a name="next-steps"></a>次のステップ
 Word のドキュメント レベルのカスタマイズを作成する方法については、「[チュートリアル: Word のドキュメント レベルのカスタマイズを初めて作成する](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)」を参照してください。 このチュートリアルでは、Visual Studio の Office 開発ツールと、Word のドキュメント レベルのカスタマイズのプログラミング モデルについて説明されています。

 Word プロジェクトの一般的なタスクが解説されているトピックの一覧については、「[Office プログラミングの共通タスク](../vsto/common-tasks-in-office-programming.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio で Office プロジェクトを作成する](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [プログラムのドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)
- [Word ソリューション](../vsto/word-solutions.md)
- [チュートリアル: Word のドキュメント レベルのカスタマイズを初めて作成する](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)
- [Word を使用したチュートリアル](../vsto/walkthroughs-using-word.md)
- [Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)
- [Office ソリューションでコードを書く](../vsto/writing-code-in-office-solutions.md)
