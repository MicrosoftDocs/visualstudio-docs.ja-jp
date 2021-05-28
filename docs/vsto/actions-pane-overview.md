---
title: 操作ウィンドウの概要
description: 操作ウィンドウは、特定の Microsoft Office Word 文書や Microsoft Office Excel ブックにアタッチされる、カスタマイズ可能なドキュメント アクション作業ウィンドウです。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- actions panes [Office development in Visual Studio], about actions panes
- actions panes [Office development in Visual Studio]
- smart documents [Office development in Visual Studio]
- user controls [Office development in Visual Studio], actions panes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 61e7ab9f00db6036d3bc8e41b9a2f19cf51f5511
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828151"
---
# <a name="actions-pane-overview"></a>操作ウィンドウの概要
  操作ウィンドウは、特定の Microsoft Office Word 文書や Microsoft Office Excel ブックにアタッチされる、カスタマイズ可能な **ドキュメント アクション** 作業ウィンドウです。 操作ウィンドウは、他の組み込み作業ウィンドウ (Excel の **[XML ソース]** 作業ウィンドウや、Word の **[スタイルと書式]** 作業ウィンドウなど) と同様に、Office の作業ウィンドウ内でホストされます。 操作ウィンドウのユーザー インターフェイスは、Windows フォーム コントロールまたは WPF コントロールを使用してデザインできます。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 操作ウィンドウは、Word または Excel のドキュメント レベルのカスタマイズ内でのみ作成できます。 VSTO アドイン内に操作ウィンドウを作成することはできません。 詳しくは、「[Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。

> [!NOTE]
> カスタム作業ウィンドウは、操作ウィンドウとは異なります。 カスタム作業ウィンドウは、特定のドキュメントではなく、アプリケーションに関連付けられます。 カスタム作業ウィンドウは、一部の Microsoft Office アプリケーション向けの VSTO アドインで作成できます。 詳細については、「[カスタム作業ウィンドウ](../vsto/custom-task-panes.md)」を参照してください。

## <a name="display-the-actions-pane"></a>操作ウィンドウを表示する
 操作ウィンドウは、<xref:Microsoft.Office.Tools.ActionsPane> クラスによって表されます。 ドキュメント レベルのプロジェクトを作成するとき、`ThisWorkbook` クラス (Excel の場合) または `ThisDocument` クラス (Word の場合) の `ActionsPane` フィールドをプロジェクトで使用することで、このクラスのインスタンスをコードで使用できます。 操作ウィンドウを表示するには、`ActionsPane` フィールドの <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> プロパティに Windows フォーム コントロールを追加します。 `actions` という名前のコントロールを操作ウィンドウに追加するコード例を次に示します。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet7":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet7":::

 操作ウィンドウは、実行時にコントロールを明示的に追加するとすぐに表示されます。 操作ウィンドウが表示された後は、ユーザーの操作に応じてコントロールを動的に追加または削除できます。 通常は、ユーザーが初めてドキュメントを開くときに操作ウィンドウが表示されるように、操作ウィンドウを表示するコードを `ThisDocument` または `ThisWorkbook` の `Startup` イベント ハンドラーに追加します。 しかし、ドキュメント内でのユーザーの操作に応じてのみ操作ウィンドウを表示することもできます。 たとえば、ドキュメント上のコントロールの `Click` イベントにコードを追加できます。

### <a name="add-multiple-controls-to-the-actions-pane"></a>操作ウィンドウに複数のコントロールを追加する
 操作ウィンドウに複数のコントロールを追加する場合は、対象のコントロールを 1 つのユーザー コントロールにグループ化し、このユーザー コントロールを <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> プロパティに追加します。 このプロセスには、次の手順が含まれます。

1. **[操作ウィンドウ コントロール]** 項目または **[ユーザー コントロール]** 項目をプロジェクトに追加して、操作ウィンドウのユーザー インターフェイス (UI) を作成します。 これらのアイテムのどちらにも、カスタム Windows フォーム <xref:System.Windows.Forms.UserControl> クラスが含まれています。 **[操作ウィンドウ コントロール]** 項目と **[ユーザー コントロール]** 項目は、名前が違うのみで、機能は同じです。

2. デザイナーを使用するか、またはコードを記述して、Windows フォーム コントロールを <xref:System.Windows.Forms.UserControl> に追加します。

   > [!NOTE]
   > また、WPF の <xref:System.Windows.Controls.UserControl> を Windows フォーム <xref:System.Windows.Forms.UserControl> に追加することにより、WPF コントロールを操作ウィンドウに追加することもできます。 詳しくは、「[Office ソリューションで WPF コントロールを使用する](../vsto/using-wpf-controls-in-office-solutions.md)」をご覧ください。

3. カスタム ユーザー コントロールのインスタンスを、プロジェクトの `ThisWorkbook` クラス (Excel の場合) または `ThisDocument` クラス (Word の場合) の `ActionsPane` フィールドに含まれるコントロールに追加します。

   このプロセスの詳細を示す例については、「[方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)」を参照してください。

## <a name="hide-the-actions-pane"></a>操作ウィンドウを非表示にする
 <xref:Microsoft.Office.Tools.ActionsPane> クラスには <xref:Microsoft.Office.Tools.ActionsPane.Hide%2A> メソッドと <xref:Microsoft.Office.Tools.ActionsPane.Visible%2A> プロパティがありますが、<xref:Microsoft.Office.Tools.ActionsPane> クラス自体のメンバーを使用して、ユーザー インターフェイスから操作ウィンドウを削除することはできません。 <xref:Microsoft.Office.Tools.ActionsPane.Hide%2A> メソッドを呼び出すか、<xref:Microsoft.Office.Tools.ActionsPane.Visible%2A> プロパティを **false** に設定すると、操作ウィンドウ上にあるコントロールだけが非表示になり、作業ウィンドウは非表示になりません。

 ソリューションの作業ウィンドウを非表示にするには、いくつかの方法があります。

- Word の場合、[ドキュメント アクション] 作業ウィンドウを表す <xref:Microsoft.Office.Interop.Word.TaskPane> オブジェクトの <xref:Microsoft.Office.Interop.Word.TaskPane.Visible%2A> プロパティを **false** に設定します。 次のコード例は、プロジェクトの `ThisDocument` クラスから実行することを前提としています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet34":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet34":::

- Excel の場合、<xref:Microsoft.Office.Tools.Excel.Workbook.Application%2A> オブジェクトの <xref:Microsoft.Office.Interop.Excel._Application.DisplayDocumentActionTaskPane%2A> プロパティを **false** に設定します。 次のコード例は、プロジェクトの `ThisWorkbook` クラスから実行することを前提としています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet11":::

- Word と Excel の両方において、作業ウィンドウを表すコマンド バーの <xref:Microsoft.Office.Core.CommandBar.Visible%2A> プロパティを **false** に設定する方法も使用できます。 次のコード例は、プロジェクトの `ThisDocument` クラスまたは `ThisWorkbook` から実行することを前提としています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet9":::

### <a name="clear-the-actions-pane-when-the-document-is-opened"></a>ドキュメントが開かれた時点では操作ウィンドウを消去する
 操作ウィンドウが表示されているときにユーザーがドキュメントを保存した場合、操作ウィンドウにコントロールが含まれているかどうかに関係なく、そのドキュメントを開くたびに操作ウィンドウが表示されます。 それをいつ表示するかを制御するには、`ThisDocument` または `ThisWorkbook` の `Startup` イベント ハンドラーで `ActionsPane` フィールドの <xref:Microsoft.Office.Tools.ActionsPane.Clear%2A> メソッドを呼び出し、ドキュメントを開いた時点で操作ウィンドウが表示されないようにします。

### <a name="determine-when-the-actions-pane-is-closed"></a>いつ操作ウィンドウが閉じられたかを判定する
 操作ウィンドウが閉じられたときに発生するイベントはありません。 <xref:Microsoft.Office.Tools.ActionsPane> クラスには <xref:Microsoft.Office.Tools.ActionsPane.VisibleChanged> イベントがありますが、このイベントは、エンド ユーザーによって操作ウィンドウが閉じられたときには発生しません。 このイベントは、<xref:Microsoft.Office.Tools.ActionsPane.Hide%2A> メソッドを呼び出すか、または <xref:Microsoft.Office.Tools.ActionsPane.Visible%2A> プロパティを **false** に設定することで操作ウィンドウ上のコントロールが非表示になったときに発生します。

 ユーザーが操作ウィンドウを閉じた場合、エンド ユーザーは、アプリケーションのユーザー インターフェイス (UI) で次のいずれかの手順を実行することにより、操作ウィンドウを再び表示できます。

##### <a name="to-display-the-actions-pane-by-using-the-ui-of-word-or-excel"></a>Word または Excel の UI を使用して操作ウィンドウを表示するには

1. リボンの **[表示]** タブをクリックします。

2. **[表示/非表示]** グループで、 **[ドキュメント アクション]** トグル ボタンをクリックします。

## <a name="program-actions-pane-events"></a>操作ウィンドウのイベントをプログラムする
 操作ウィンドウに複数のユーザー コントロールを追加し、ドキュメント上のイベントに応答するコードを作成して、ユーザー コントロールを表示したり非表示にしたりすることができます。 XML スキーマ要素をドキュメントにマップした場合は、XML 要素の 1 つにカーソルが置かれた時点で、操作ウィンドウに特定のユーザー コントロールを表示するようにできます。 詳しくは、「[方法: Visual Studio 内で Word 文書にスキーマを割り当てる](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)」および「[方法: Visual Studio 内でワークシートにスキーマを割り当てる](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)」をご覧ください。

 また、ホスト コントロール、アプリケーション、またはドキュメント イベントなど、任意のオブジェクトのイベントに応答するコードを作成することもできます。 詳しくは、「[チュートリアル: NamedRange コントロールのイベントに対するプログラミング](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)」をご覧ください。

## <a name="bind-data-to-controls-on-the-actions-pane"></a>操作ウィンドウ上のコントロールにデータをバインドする
 操作ウィンドウのコントロールは、Windows フォームのコントロールと同じデータ バインディング機能を備えています。 データセット、型指定されたデータセット、XML などのデータ ソースに、コントロールをバインドできます。 詳しくは、「[データ連結と Windows フォーム](/dotnet/framework/winforms/data-binding-and-windows-forms)」をご覧ください。

 操作ウィンドウのコントロールとドキュメントのコントロールは、同じデータセットにバインドできます。 たとえば、操作ウィンドウのコントロールとワークシートのコントロール間でマスター/詳細関係を作成できます。 詳しくは、「[チュートリアル: Excel の操作ウィンドウ上のコントロールにデータをバインドする](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)」をご覧ください。

## <a name="validate-data-in-actions-pane-controls"></a>操作ウィンドウ コントロール内のデータを検証する
 操作ウィンドウ上のコントロールの <xref:System.Windows.Forms.Control.Validating> イベント ハンドラーでメッセージ ボックスを表示する場合、フォーカスがコントロールからメッセージ ボックスに移った時点で 2 度目のイベントが発生することがあります。 この問題を回避するには、<xref:System.Windows.Forms.ErrorProvider> コントロールを使用して検証エラー メッセージを表示するようにします。

## <a name="user-control-stacking-order"></a>ユーザー コントロールの積み重ね順
 複数のユーザー コントロールを使用している場合は、垂直方向または水平方向のどちらにドッキングされるかにかかわらず、操作ウィンドウにユーザー コントロールを正しく積み重ねるコードを作成できます。 操作ウィンドウにユーザー コントロールを積み重ねる順序は、<xref:Microsoft.Office.Tools.ActionsPane.StackOrder%2A> プロパティの <xref:Microsoft.Office.Tools.StackStyle> 列挙体を使用して設定できます。 詳しくは、「[方法: 操作ウィンドウ上のコントロールのレイアウトを管理する](../vsto/how-to-manage-control-layout-on-actions-panes.md)」をご覧ください。

 <xref:Microsoft.Office.Tools.ActionsPane.StackOrder%2A> プロパティでは、次の <xref:Microsoft.Office.Tools.StackStyle> 列挙値を使用できます。

|積み重ねのスタイル|定義|
|--------------------|----------------|
|FromBottom|操作ウィンドウの下から積み重ねます。|
|FromLeft|操作ウィンドウの左から積み重ねます。|
|FromRight|操作ウィンドウの右から積み重ねます。|
|FromTop|操作ウィンドウの上から積み重ねます。|
|なし|積み重ね順を定義しません。順序は開発者が制御します。|

 次のコードでは、操作ウィンドウの上からユーザー コントロールをスタックするように <xref:Microsoft.Office.Tools.ActionsPane.StackOrder%2A> プロパティを設定します。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet10":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet10":::

## <a name="anchor-controls"></a>コントロールを固定する
 ユーザーが実行時に操作ウィンドウのサイズを変更した場合に、操作ウィンドウと一緒にコントロールのサイズも変更されるように設定できます。 Windows フォーム コントロールの <xref:System.Windows.Forms.Control.Anchor%2A> プロパティを使用すると、コントロールを操作ウィンドウに固定できます。 同じように、Windows フォーム コントロールをユーザー コントロールに固定することもできます。 詳しくは、「[方法: Windows フォームにコントロールを固定する](/dotnet/framework/winforms/controls/how-to-anchor-controls-on-windows-forms)」をご覧ください。

## <a name="resize-the-actions-pane"></a>操作ウィンドウのサイズを変更する
 <xref:Microsoft.Office.Tools.ActionsPane> は作業ウィンドウに埋め込まれているため、<xref:Microsoft.Office.Tools.ActionsPane> のサイズを直接変更することはできません。 ただし、作業ウィンドウを表す <xref:Microsoft.Office.Core.CommandBar> の <xref:Microsoft.Office.Core.CommandBar.Width%2A> プロパティを設定すると、プログラムによって作業ウィンドウの幅を変更できます。 作業ウィンドウの高さは、作業ウィンドウが水平にドッキングされている場合、または浮動している場合に変更できます。

 作業ウィンドウのサイズをプログラムによって変更することはお勧めしません。ユーザーが必要に応じて作業ウィンドウのサイズを選択できるようにする必要があるためです。 ただし、作業ウィンドウの幅を変更する必要がある場合には、次のコードを使用してこのタスクを実現できます。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet102":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet102":::

## <a name="reposition-the-actions-pane"></a>操作ウィンドウの位置を変更する
 <xref:Microsoft.Office.Tools.ActionsPane> は作業ウィンドウに埋め込まれているため、その位置を直接変更することはできません。 ただし、作業ウィンドウを表す <xref:Microsoft.Office.Core.CommandBar> の <xref:Microsoft.Office.Core.CommandBar.Position%2A> プロパティを設定すると、プログラムによって作業ウィンドウを移動できます。

 作業ウィンドウの位置をプログラムによって移動することはお勧めしません。ユーザーが必要に応じて、画面上での作業ウィンドウの位置を選択できるようにする必要があるためです。 ただし、作業ウィンドウを特定の位置に移動する必要がある場合は、次のコードを使用してこのタスクを実現できます。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet100":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet100":::

> [!NOTE]
> エンド ユーザーは、作業ウィンドウの位置を手動でいつでも変更できます。 プログラムで指定した位置に作業ウィンドウを常にドッキングしておくことはできません。 ただし、向きの変更を確認し、操作ウィンドウ上のコントロールが正しい方向で積み重ねられるようにすることは可能です。 詳しくは、「[方法: 操作ウィンドウ上のコントロールのレイアウトを管理する](../vsto/how-to-manage-control-layout-on-actions-panes.md)」をご覧ください。

 <xref:Microsoft.Office.Tools.ActionsPane> の <xref:Microsoft.Office.Tools.ActionsPane.Top%2A> プロパティと <xref:Microsoft.Office.Tools.ActionsPane.Left%2A> プロパティを設定しても、その位置は変更されません。これは、<xref:Microsoft.Office.Tools.ActionsPane> オブジェクトが作業ウィンドウに埋め込まれているためです。

 作業ウィンドウがドッキングされていない場合、作業ウィンドウを表す <xref:Microsoft.Office.Core.CommandBar> の <xref:Microsoft.Office.Core.CommandBar.Top%2A> プロパティと <xref:Microsoft.Office.Core.CommandBar.Left%2A> プロパティを設定できます。 次のコードでは、ドッキングが解除された作業ウィンドウをドキュメントの左上隅に移動します。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet101":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet101":::

## <a name="see-also"></a>関連項目
- [Office ソリューションで WPF コントロールを使用する](../vsto/using-wpf-controls-in-office-solutions.md)
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [Office プロジェクト内のオブジェクトへのグローバル アクセス](../vsto/global-access-to-objects-in-office-projects.md)
- [方法: Word 文書または Excel ブックに操作ウィンドウを追加する](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
- [チュートリアル: Word の操作ウィンドウでコントロールにデータをバインドする](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)
- [チュートリアル: Excel の操作ウィンドウ上のコントロールにデータをバインドする](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md)
- [方法: 操作ウィンドウ上のコントロールのレイアウトを管理する](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [チュートリアル: 操作ウィンドウからドキュメントにテキストを挿入する](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
