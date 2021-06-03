---
title: '方法: Word 文書に XMLNode コントロールを追加する'
description: 非繰り返し XML スキーマ要素を Microsoft Office Word 文書にマップすると、Visual Studio で XMLNodes コントロールが文書に自動的に追加されることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNode control, adding to documents
- controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7a55d2e92ae84cb8d5388fe90655b1c95f6f8e09
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99954125"
---
# <a name="how-to-add-xmlnode-controls-to-word-documents"></a>方法: Word 文書に XMLNode コントロールを追加する
  **重要** このトピックに記載されている Microsoft Word に関する情報は、Microsoft が カスタム XML に関連する特定の機能を Microsoft Word から削除した 2010 年 1 月より前に Microsoft によってライセンス供与された Microsoft Word 製品を使用している米国領土外を本拠地とする個人と組織、またはそのような Microsoft Word 製品上で実行されるプログラムを開発している個人または開発者のみを対象にしています。 Microsoft Word に関するこの情報は、2010 年 1 月 10 日以降に Microsoft によってライセンス供与された Microsoft Word 製品を使用している、またはその上で実行されるプログラムを開発している米国内の個人または組織は対象外であり、使用することはできません。それらの製品は、その日付より前にライセンス供与された製品または米国外で使用するために購入およびライセンス供与された製品と同様に動作することはありません。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 非繰り返し XML スキーマ要素を Microsoft Office Word 文書にマップすると、Visual Studio では <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールが文書に自動的に追加されます。 繰り返し XML スキーマ要素のマッピングについては、「[方法: Word 文書に XMLNode コントロールを追加する](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md)」を参照してください。

> [!NOTE]
> <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールを **[ツールボックス]** や **[データ ソース]** ウィンドウから使用することはできず、プログラムによって作成することはできません。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-an-xmlnode-control-to-a-document"></a>XMLNodes コントロールを文書に追加するには

1. Visual Studio デザイナーの文書のリボンで、 **[開発者]** タブをクリックします。

    > [!NOTE]
    > **[開発]** タブが表示されていない場合は、最初にこれを表示する必要があります。 詳細については、「[方法: [開発者] タブをリボンに表示する](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)」を参照してください。

2. **[XML]** グループの **[スキーマ]** をクリックします。

     **[テンプレートとアドイン]** ダイアログ ボックスが表示されます。

3. **[XML スキーマ]** タブをクリックします。

4. **[スキーマの追加]** をクリックします。

     **[スキーマの追加]** ダイアログ ボックスが開きます。

5. **[スキーマの追加]** ダイアログ ボックスで、非繰り返しスキーマ要素が含まれている XML スキーマを選択し、 **[開く]** をクリックします。

     **[スキーマの設定]** ダイアログ ボックスが表示されます。

6. 別名を割り当てるか、 **[OK]** をクリックして別名を指定せずにスキーマを追加します。

     **[スキーマの追加]** ダイアログ ボックスにスキーマが追加されます。

7. **[スキーマの追加]** ダイアログ ボックスで、 **[OK]** をクリックします。

8. **[XML データ構造]** 作業ウィンドウが開きます。

9. **[XML データ構造]** 作業ウィンドウで非繰り返しスキーマ要素をクリックして、文書に追加します。

     <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールが作成され、プロジェクトに追加されます。

## <a name="see-also"></a>関連項目
- [XMLNode コントロール](../vsto/xmlnode-control.md)
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
