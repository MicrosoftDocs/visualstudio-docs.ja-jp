---
title: '方法: 操作ウィンドウ上のコントロールのレイアウトを管理する'
description: ユーザー コントロールを適切に積み重ねるコードを書いて、操作ウィンドウのコントロールのレイアウトを管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- actions panes [Office development in Visual Studio], control layout
- controls [Office development in Visual Studio], layout on actions panes
- smart documents [Office development in Visual Studio], control layout
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 182dee248f161f3dde721c50ee996d6f621dd9af
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827449"
---
# <a name="how-to-manage-control-layout-on-actions-panes"></a>方法: 操作ウィンドウ上のコントロールのレイアウトを管理する
  既定では、操作ウィンドウは、文書またはワークシートの右側にドッキングされますが、左、上、または下にドッキングできます。 複数のユーザー コントロールを使用している場合は、操作ウィンドウにユーザー コントロールを正しく積み重ねるコードを書くことができます。 詳細については、「[操作ペインの概要](../vsto/actions-pane-overview.md)」を参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 コントロールの積み重ね順は、操作ウィンドウが垂直方向または水平方向のどちらにドッキングされているかによって異なります。

> [!NOTE]
> ユーザーが実行時に操作ウィンドウのサイズを変更した場合に、操作ウィンドウと一緒にサイズ変更するようにコントロールを設定できます。 Windows フォーム コントロールの <xref:System.Windows.Forms.Control.Anchor%2A> プロパティを使用すると、コントロールを操作ウィンドウに固定できます。 詳細については、「[方法 : Windows フォームにコントロールを固定する](/dotnet/framework/winforms/controls/how-to-anchor-controls-on-windows-forms)」を参照してください。

> [!NOTE]
> 次の手順で参照している Visual Studio ユーザー インターフェイス要素の一部は、お使いのコンピューターでは名前や場所が異なる場合があります。 これらの要素は、使用している Visual Studio のエディションや独自の設定によって決まります。 詳細については、「[Visual Studio IDE のカスタマイズ](../ide/personalizing-the-visual-studio-ide.md)」を参照してください。

## <a name="to-set-the-stack-order-of-the-actions-pane-controls"></a>操作ウィンドウのコントロールの積み重ね順を設定するには

1. 複数のユーザー コントロールまたは入れ子になった操作ウィンドウのコントロールを持つ操作ウィンドウを含む、Microsoft Office Word の文書レベルのプロジェクトを開きます。 詳細については、「[方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)」を参照してください。

2. **ソリューション エクスプローラー** で **ThisDocument.cs** または **ThisDocument.vb** を右クリックしてから、 **[コードの表示]** をクリックします。

3. 操作ウィンドウの <xref:Microsoft.Office.Tools.ActionsPane.OrientationChanged> イベント ハンドラーで、操作ウィンドウの向きが水平になっているかどうかを確認します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet30":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet30":::

4. 向きが水平の場合は、操作ウィンドウのコントロールを左から積み重ねます。それ以外の場合は、上から積み重ねます。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet31":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet31":::

5. C# では、`ActionsPane` のイベント ハンドラーを <xref:Microsoft.Office.Tools.Word.Document.Startup> イベント ハンドラーに追加する必要があります。 イベント ハンドラーの作成方法について詳しくは、「[方法: Office プロジェクトでイベント ハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)」をご覧ください。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet32":::

6. プロジェクトを実行し、操作ウィンドウが文書の上部にドッキングされているときは操作ウィンドウのコントロールが左から右に積み重ねられていること、また操作ウィンドウが文書の右側にドッキングされているときはコントロールが上から下に積み重ねられていることを確認します。

## <a name="example"></a>例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet29":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet29":::

## <a name="compile-the-code"></a>コードのコンパイル
 この例で必要な要素は次のとおりです。

- 複数のユーザー コントロールまたは入れ子になった操作ウィンドウのコントロールを含む操作ウィンドウを持つ Word 文書レベルのプロジェクト。

## <a name="see-also"></a>関連項目
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
- [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [チュートリアル : 操作ウィンドウからドキュメントにテキストを挿入する](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
- [チュートリアル : 操作ウィンドウからドキュメントにテキストを挿入する](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
