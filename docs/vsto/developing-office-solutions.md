---
title: Office ソリューションの開発
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, about developing solutions
- solutions [Office development in Visual Studio], developing
- Office solutions [Office development in Visual Studio], developing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8ede09f18808eda22c747ac28e3c279fc43266bc
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551578"
---
# <a name="develop-office-solutions"></a>Office ソリューションの開発
  Visual Studio の Office Developer Tools を使用してプロジェクトを設計し、プロジェクト ファイルを設定すると、コードとカスタム ユーザー インターフェイス (UI) の実装に集中できるようになります。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="office-solutions-programming-model"></a>Office ソリューションのプログラミングモデル
 Office オブジェクト モデルは、プログラミングできるさまざまなオブジェクトを公開します。 ユーザーはマネージド コードを使用して Office ソリューションをプログラミングするたびに、Office プライマリ相互運用機能アセンブリの型を使用するコードを記述します。 また、Visual Studio の Office プロジェクト テンプレートを使用して作成したソリューションでは、プロジェクトに生成されたクラスに直接コードを記述します。 詳細については、「 [Office ソリューションのコードの記述](../vsto/writing-code-in-office-solutions.md)」を参照してください。

## <a name="program-different-types-of-office-solutions"></a>さまざまな種類の Office ソリューションをプログラミングする
 作成しているソリューションの種類は、プロジェクトで使用できる機能を決定します。 たとえば、デザイン時に Visual Studio の *[ツールボックス]* から項目をドラッグして、Windows フォーム コントロールおよび拡張された Office コントロール ( **ホスト コントロール** という名前) をドキュメント レベルのカスタマイズに追加することができます。 ただし、VSTO アドインを開発している場合は、コードを記述することで、これらのコントロールのみを実行時にドキュメントに追加できます。

 さまざまな種類のソリューションに固有の機能の詳細については、次のトピックを参照してください。

- [プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)。

- [ドキュメントレベルのカスタマイズをプログラム](../vsto/programming-document-level-customizations.md)します。

- [OFFICE UI のカスタマイズ](../vsto/office-ui-customization.md)。

  Office ソリューションの計画に役立つ背景情報と、プロジェクトの作成に役立つ手順については、「 [office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|タイトル|説明|
|-----------|-----------------|
|[Office ソリューションにおけるコードの記述](../vsto/writing-code-in-office-solutions.md)|Office ソリューションのコードの記述に関するさまざまな側面について説明します。|
|[プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)|VSTO アドインおよび関連するプログラミング タスクのプログラミング モデルの概要を示します。|
|[ドキュメント レベルのカスタマイズのプログラミング](../vsto/programming-document-level-customizations.md)|ドキュメント レベルのカスタマイズのプログラミング モデルおよび関連するプログラミング タスクの概要を示します。|
|[Office UI のカスタマイズ](../vsto/office-ui-customization.md)|VSTO アドインおよびドキュメント レベルのカスタマイズを使用して、Office アプリケーションの UI をカスタマイズできるさまざまな方法について説明します。|
|[Office ソリューションのデータ](../vsto/data-in-office-solutions.md)|コントロールへのデータ バインドおよびドキュメント レベルのカスタマイズのデータ キャッシュなど、Office ソリューションのデータを処理できるさまざまな方法について説明します。|
|[自動保存が Office ソリューションに与える影響](./how-autosave-impacts-office-solutions.md)|自動保存が有効になっている場合に Office ソリューションに対して行う必要がある調整について説明します。|
|[Office ソリューションのトラブルシューティング](../vsto/troubleshooting-office-solutions.md)|Office ソリューションの作成時に発生する可能性がある一般的な問題を解決するためのヒントを提供します。|
|[Office でのスレッドのサポート](../vsto/threading-support-in-office.md)|Office ソリューションで複数のスレッドを操作する概要を示します。|
|[Office プロジェクトのユーザー補助機能](../vsto/accessibility-in-office-projects.md)|Office ソリューションで使用できるユーザー補助機能について説明します。|

## <a name="see-also"></a>関連項目
- [方法: カスタムドキュメントプロパティの作成および変更](../vsto/how-to-create-and-modify-custom-document-properties.md)
- [方法: ドキュメントのプロパティの読み取りと書き込み](../vsto/how-to-read-from-and-write-to-document-properties.md)
- [方法: Office 多言語ユーザーインターフェイスを対象にする](../vsto/how-to-target-the-office-multilingual-user-interface.md)
- [チュートリアル: 初めての Excel 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)
- [チュートリアル: Excel 用のドキュメントレベルのカスタマイズを初めて作成する](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)
- [チュートリアル: Outlook 用の初めての VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)
- [チュートリアル: 初めての PowerPoint 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)
- [チュートリアル: Project 用の最初の VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)
- [チュートリアル: Word 用の最初の VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)
- [チュートリアル: 最初の Word 用ドキュメント レベルのカスタマイズの作成](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)
