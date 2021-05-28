---
title: Word 文書または Excel ブックに操作ウィンドウを追加する
description: Microsoft Office Word 文書や Microsoft Excel ブックに操作ウィンドウを追加するには、まず Windows フォーム ユーザー コントロールを作成する必要があるということについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- smart documents [Office development in Visual Studio], creating in Word
- smart documents [Office development in Visual Studio], adding controls
- actions panes [Office development in Visual Studio], creating in Word
- actions panes [Office development in Visual Studio], adding controls
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9cf079727581b9cec4b6cb77a0a0c3f0b503b3a0
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825525"
---
# <a name="how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks"></a>方法: Word 文書または Excel ブックに操作ウィンドウを追加する
  Microsoft Office Word 文書や Microsoft Excel ブックに操作ウィンドウを追加するには、まず Windows フォーム ユーザー コントロールを作成します。 次に、プロジェクト内の `ThisDocument.ActionsPane` フィールド (Word) または `ThisWorkbook.ActionsPane` フィールド (Excel) の <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> プロパティに、ユーザー コントロールを追加します。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="creating-the-user-control"></a>ユーザー コントロールの作成
 次の手順は、Word または Excel プロジェクトでユーザー コントロールを作成する方法を示したものです。 また、ユーザー コントロールにボタンを追加して、それがクリックされたときに、文書やブックにテキストが書き込まれるようにします。

#### <a name="to-create-the-user-control"></a>ユーザー コントロールを作成するには

1. Visual Studio で Word または Excel のドキュメント レベルのプロジェクトを開きます。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。

3. **[新しい項目の追加]** ダイアログ ボックスで、 **[操作ウィンドウ コントロール**] を選択し、名前を **HelloControl** と指定して、 **[追加]** をクリックします。

    > [!NOTE]
    > 別の方法として、 **[ユーザー コントロール]** の項目をプロジェクトに追加することもできます。 **[操作ウィンドウ コントロール]** の項目と **[ユーザー コントロール]** の項目によって生成されるクラスは、機能的には同等です。

4. **ツールボックス** の **[Windows フォーム]** タブから、**Button** コントロールをコントロール上にドラッグします。

    > [!NOTE]
    > デザイナーにコントロールが表示されていない場合は、**ソリューション エクスプローラー** で **[HelloControl]** をダブルクリックします。

5. ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーにコードを追加します。 次の例は、Microsoft Office Word 文書の場合のコードです。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/HelloControl.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/HelloControl.vb" id="Snippet12":::

6. C# では、ボタン クリックのイベント ハンドラーを追加する必要があります。 このコードは、`HelloControl` コンストラクター内の、`InitializeComponent` の呼び出しの後に配置できます。

     イベント ハンドラーの作成方法について詳しくは、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」をご覧ください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/HelloControl.cs" id="Snippet13":::

## <a name="add-the-user-control-to-the-actions-pane"></a>操作ウィンドウにユーザー コントロールを追加する
 操作ウィンドウを表示するには、`ThisDocument.ActionsPane` フィールド (Word) または `ThisWorkbook.ActionsPane` フィールド (Excel) の <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> プロパティに、ユーザー コントロールを追加します。

### <a name="to-add-the-user-control-to-the-actions-pane"></a>操作ウィンドウにユーザー コントロールを追加するには

1. `ThisDocument` クラスまたは `ThisWorkbook` クラスに、クラス レベルの宣言として次のコードを追加します (このコードをメソッドに追加することはしないでください)。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet14":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet14":::

2. `ThisDocument` クラスの `ThisDocument_Startup` イベント ハンドラー、または `ThisWorkbook` クラスの `ThisWorkbook_Startup` イベント ハンドラーに、次のコードを追加します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet15":::

## <a name="see-also"></a>こちらもご覧ください
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
- [方法: 操作ウィンドウ上のコントロールのレイアウトを管理する](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
