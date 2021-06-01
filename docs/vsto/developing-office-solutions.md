---
title: Office ソリューションを開発する
description: Visual Studio で Office Developer Tools を使用してプロジェクトを設計する方法について説明します。 また、コードとカスタム ユーザー インターフェイス (UI) の実装を始める方法についても説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 012f08b4a4a8364d278322b7fe057231183fa233
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99897583"
---
# <a name="develop-office-solutions"></a>Office ソリューションを開発する
  Visual Studio の Office Developer Tools を使用してプロジェクトを設計し、プロジェクト ファイルを設定すると、コードとカスタム ユーザー インターフェイス (UI) の実装に集中できるようになります。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="office-solutions-programming-model"></a>Office ソリューションのプログラミング モデル
 Office オブジェクト モデルは、プログラミングできるさまざまなオブジェクトを公開します。 ユーザーはマネージド コードを使用して Office ソリューションをプログラミングするたびに、Office プライマリ相互運用機能アセンブリの型を使用するコードを記述します。 また、Visual Studio の Office プロジェクト テンプレートを使用して作成したソリューションでは、プロジェクトに生成されたクラスに直接コードを記述します。 詳細については、「[Office ソリューションでコードを書く](../vsto/writing-code-in-office-solutions.md)」を参照してください。

## <a name="program-different-types-of-office-solutions"></a>さまざまな種類の Office ソリューションをプログラミングする
 作成しているソリューションの種類は、プロジェクトで使用できる機能を決定します。 たとえば、デザイン時に Visual Studio の *[ツールボックス]* から項目をドラッグして、Windows フォーム コントロールおよび拡張された Office コントロール ( **ホスト コントロール** という名前) をドキュメント レベルのカスタマイズに追加することができます。 ただし、VSTO アドインを開発している場合は、コードを記述することで、これらのコントロールのみを実行時にドキュメントに追加できます。

 さまざまな種類のソリューションに固有の機能の詳細については、次のトピックを参照してください。

- [VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)。

- [ドキュメント レベルのカスタマイズのプログラミング](../vsto/programming-document-level-customizations.md)。

- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)。

  Office ソリューションの計画に役立つ背景情報およびプロジェクトの作成に役立つ手順については、「[Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[Office ソリューションでコードを書く](../vsto/writing-code-in-office-solutions.md)|Office ソリューションのコードの記述に関するさまざまな側面について説明します。|
|[VSTO アドインのプログラミング](../vsto/programming-vsto-add-ins.md)|VSTO アドインおよび関連するプログラミング タスクのプログラミング モデルの概要を示します。|
|[プログラムのドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)|ドキュメント レベルのカスタマイズのプログラミング モデルおよび関連するプログラミング タスクの概要を示します。|
|[Office UI のカスタマイズ](../vsto/office-ui-customization.md)|VSTO アドインおよびドキュメント レベルのカスタマイズを使用して、Office アプリケーションの UI をカスタマイズできるさまざまな方法について説明します。|
|[Office ソリューションにおけるデータ](../vsto/data-in-office-solutions.md)|コントロールへのデータ バインドおよびドキュメント レベルのカスタマイズのデータ キャッシュなど、Office ソリューションのデータを処理できるさまざまな方法について説明します。|
|[自動保存による Office ソリューションへの影響](./how-autosave-impacts-office-solutions.md)|自動保存を有効にしたときに、Office ソリューションに対して必要になる場合がある調整について説明します。|
|[Office ソリューションのトラブルシューティング](../vsto/troubleshooting-office-solutions.md)|Office ソリューションの作成時に発生する可能性がある一般的な問題を解決するためのヒントを提供します。|
|[Office でのスレッドのサポート](../vsto/threading-support-in-office.md)|Office ソリューションで複数のスレッドを操作する概要を示します。|
|[Office プロジェクトでのアクセシビリティ](../vsto/accessibility-in-office-projects.md)|Office ソリューションで使用できるユーザー補助機能について説明します。|

## <a name="see-also"></a>関連項目
- [方法: カスタム ドキュメント プロパティを作成および変更する](../vsto/how-to-create-and-modify-custom-document-properties.md)
- [方法: ドキュメント プロパティの読み込みと書き込みを行う](../vsto/how-to-read-from-and-write-to-document-properties.md)
- [方法: Office Multilingual User Interface を使用する](../vsto/how-to-target-the-office-multilingual-user-interface.md)
- [チュートリアル: 初めての Excel 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)
- [チュートリアル: Excel のドキュメント レベルのカスタマイズを初めて作成する](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)
- [チュートリアル: 初めての Outlook 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)
- [チュートリアル: 初めての PowerPoint 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)
- [チュートリアル: 初めての Project 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)
- [チュートリアル: 初めての Word 用 VSTO アドインを作成する](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)
- [チュートリアル: Word のドキュメント レベルのカスタマイズを初めて作成する](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)
