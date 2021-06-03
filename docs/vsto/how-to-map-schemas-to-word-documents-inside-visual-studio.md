---
title: '方法: Visual Studio 内で Word 文書にスキーマを割り当てる'
description: Visual Studio でドキュメントを開いているときに、XML スキーマを Microsoft Office Word 文書にマップする方法について説明します。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio], mapping
- mappings [Office development in Visual Studio], XML schemas to Word documents
- Word [Office development in Visual Studio], mapping XML schemas
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 082d5fe4fbcc7f66709770c16d3c9a1a2811e60d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900925"
---
# <a name="how-to-map-schemas-to-word-documents-inside-visual-studio"></a>方法: Visual Studio 内で Word 文書にスキーマを割り当てる
  **重要** このトピックに記載されている Microsoft Word に関する情報は、Microsoft が カスタム XML に関連する特定の機能を Microsoft Word から削除した 2010 年 1 月より前に Microsoft によってライセンス供与された Microsoft Word 製品を使用している米国領土外を本拠地とする個人と組織、またはそのような Microsoft Word 製品上で実行されるプログラムを開発している個人または開発者のみを対象にしています。 Microsoft Word に関するこの情報は、2010 年 1 月 10 日以降に Microsoft によってライセンス供与された Microsoft Word 製品を使用している、またはその上で実行されるプログラムを開発している米国内の個人または組織は対象外であり、使用することはできません。それらの製品は、その日付より前にライセンス供与された製品または米国外で使用するために購入およびライセンス供与された製品と同様に動作することはありません。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Visual Studio でドキュメントを開いているときに、XML スキーマをドキュメントにマップすることができます。 Visual Studio の外部でドキュメントを開くときに使用するのと同じ Microsoft Office Word ツールを使用します。 Word ソリューションを作成する前または後からドキュメントにスキーマをマップするかどうかにかかわらず、Office プロジェクトによって同じオブジェクトが作成されます。

## <a name="to-map-an-xml-schema-to-a-word-document-in-visual-studio"></a>Visual Studio で XML スキーマを Word 文書にマップする方法

1. Visual Studio 内で Word 文書またはテンプレート プロジェクトを開きます。

2. ドキュメント内をクリックして、デザイナーにフォーカスを移動します。

3. リボンの **[開発]** タブをクリックします。

    > [!NOTE]
    > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳細については、「[方法: [開発者] タブをリボンに表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

4. **[XML]** グループの **[スキーマ]** をクリックします。

     **[テンプレートとアドイン]** ダイアログ ボックスが表示されます。

5. **[XML スキーマ]** タブをクリックします。

6. **[スキーマの追加]** をクリックします。

     **[スキーマの追加]** ダイアログ ボックスが開きます。

7. スキーマ ファイルを参照して選択し、 **[開く]** をクリックします。

     **[スキーマの設定]** ダイアログ ボックスが開きます。

8. 別名を割り当てるか、 **[OK]** をクリックして別名を指定せずにスキーマを追加します。

9. **[OK]** をクリックします。

     **[XML 構造]** ウィンドウが開きます。

10. **[XML 構造]** ウィンドウから、対応するコントロールを作成するドキュメント内の場所に要素をドラッグします。

## <a name="see-also"></a>関連項目
- [方法: Visual Studio 内でワークシートにスキーマを割り当てる](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
- [ドキュメント レベルのカスタマイズにおける XML スキーマとデータ](../vsto/xml-schemas-and-data-in-document-level-customizations.md)
