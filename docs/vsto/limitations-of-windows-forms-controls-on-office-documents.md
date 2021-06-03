---
title: Office ドキュメント上の Windows フォーム コントロールの制限事項
description: Microsoft Office ドキュメントでの Windows フォーム コントロールのメソッドとプロパティの制限事項について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], ActiveX legacy
- ActiveX controls [Office development in Visual Studio]
- Windows Forms controls [Office development in Visual Studio], limitations
- controls [Office development in Visual Studio], Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], unsupported properties and methods
- Toolbox [Office development in Visual Studio], unsupported controls
- user controls [Office development in Visual Studio], grouping controls
- Windows Forms controls [Office development in Visual Studio], Toolbox
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cc507d31f791a3f3d7addbcffc0b9b87963d443f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888720"
---
# <a name="limitations-of-windows-forms-controls-on-office-documents"></a>Office ドキュメント上の Windows フォーム コントロールの制限事項

Microsoft Office Word 文書または Microsoft Office Excel ワークシートに追加される Windows フォーム コントロールと Windows フォームに追加される Windows フォーム コントロールには、いくつかの違いがあります。 たとえば、ドキュメントに <xref:Microsoft.Office.Tools.Word.Controls.Button> コントロールを追加した場合、<xref:System.Windows.Forms.Control.Dock>、<xref:System.Windows.Forms.Control.Anchor>、<xref:System.Windows.Forms.Control.TabIndex> などのプロパティは予期したとおりに動作しません。

これらの違いの多くは、ドキュメントで Windows フォーム コントロールをホストする方法に起因します。 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] では、ドキュメントに Windows フォーム コントロールを追加すると、Windows フォーム コントロールをホストする ActiveX コントロールがドキュメントに埋め込まれます。 Windows フォーム コントロールはドキュメントに直接埋め込まれません。

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="limitations-of-methods-and-properties-of-windows-forms-controls"></a>Windows フォーム コントロールのメソッドとプロパティの制限事項

Windows フォーム コントロールのメソッドとプロパティには、ドキュメント上では Windows フォーム上と同じように動作しないものがあります。そのため、これらを使用しないことをお勧めします。 たとえば、<xref:System.Windows.Forms.Control.Dock> や <xref:System.Windows.Forms.Control.Anchor> などのプロパティの設定は、ドキュメントではなく、コンテナー ActiveX コントロールに対するコントロールの位置にのみ影響します。 Word と Excel でサポートされない Windows フォーム コントロールのメソッドとプロパティの一覧を次に示します。

- Excel コントロールでサポートされないプロパティ:

  - <xref:System.Windows.Forms.Control.Anchor>
  - <xref:System.Windows.Forms.Control.Dock>
  - <xref:System.Windows.Forms.Control.Location>
  - <xref:System.Windows.Forms.Control.TabIndex>
  - <xref:System.Windows.Forms.Control.TabStop>
  - <xref:System.Windows.Forms.Control.TopLevelControl>

- Word コントロールでサポートされないメソッドとプロパティ:

  - <xref:System.Windows.Forms.Control.Hide%2A>
  - <xref:System.Windows.Forms.Control.Show%2A>
  - <xref:System.Windows.Forms.Control.Anchor>
  - <xref:System.Windows.Forms.Control.Dock>
  - <xref:System.Windows.Forms.Control.Location>
  - <xref:System.Windows.Forms.Control.TabIndex>
  - <xref:System.Windows.Forms.Control.TabStop>
  - <xref:System.Windows.Forms.Control.TopLevelControl>
  - <xref:System.Windows.Forms.Control.Visible>

また、Word 文書の行内にある Windows フォーム コントロールの <xref:System.Windows.Forms.Control.Left> または <xref:System.Windows.Forms.Control.Top> プロパティを設定することもできません。 Windows フォーム コントロールは、次の場合に行内に追加されます。

- プログラムで、Word 文書にコントロールを追加し、場所の範囲を指定するメソッドを使用します。

- デザイン時に、Word 文書に Windows フォーム コントロールを追加します。 これを変更するには、デザイナーでコントロールを変更します。

## <a name="differences-in-windows-forms-controls-on-office-documents"></a>Office ドキュメント上の Windows フォーム コントロールの相違点

Windows フォーム コントロールは、通常、Office ドキュメント上でも Windows フォーム上と同じように動作しますが、いくつかの違いがあります。 次の表では、Office ドキュメント上の Windows フォーム コントロールに存在する違いについて説明します。

|機能|差|
|-------------------|----------------|
|コントロール タブの順序|Excel ワークシートまたは Word 文書に配置されているコントロール間を Tab キーで移動することはできません。|
|コントロールのグループ化|Office ドキュメントでは、<xref:System.Windows.Forms.GroupBox> コントロールを使用して他のコントロールを含めることはできません。 ドキュメントに複数のオプション ボタンを直接追加した場合、これらのオプション ボタンは相互に排他的ではありません。 オプション ボタンが相互に排他的になるようにコードを記述することもできますが、ユーザー コントロールにオプション ボタンを追加してから、ドキュメントにユーザー コントロールを追加することをお勧めします。 詳細については、「[Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」の Word コントロールのサンプルまたは Excel コントロールのサンプルをご覧ください。|
|コントロール型|ドキュメントで使用される Windows フォーム コントロールは、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によって提供されるクラスでラップされます。これにより、Excel ワークシートまたは Word 文書に固有の追加機能を制御できます。 たとえば、Excel ワークシート上に **ボタン** コントロールがある場合は、そのオブジェクトを参照またはキャストするときに、型を <xref:System.Windows.Forms.Button> ではなく <xref:Microsoft.Office.Tools.Excel.Controls.Button> として指定する必要があります。|
|コントロールの位置とサイズ|コントロールのサイズと位置は、コンテナー ActiveX コントロールの一部であるプロパティによって決定されます。 ActiveX コントロールのプロパティでは、Windows フォーム コントロールの同等のプロパティとは異なる値を受け取ります。 コントロールの `Top`、`Left`、`Height`、または `Width` プロパティを設定するときは、ピクセルではなくポイント単位で指定します。|
|Word 文書でのコントロールの位置|フローベースのレイアウトにコントロールを追加する場合は、コンテンツが変更されたときにコントロールがコンテンツと共にフローすることにご注意ください。 コントロールは Word 文書の行内に追加されるため、**ツールボックス** からコントロールをドラッグしたときに段落に固定できません。 コントロールをダブルクリックするなど、別の方法でコントロールを追加すると、画像を挿入するために用意された Word のオプションに従ってコントロールが挿入されます。<br /><br /> 行内にあるコントロールの `Left` または `Top` プロパティを設定することはできません。<br /><br /> ヘッダー、フッター、またはサブドキュメント内にコントロールを配置することはできません。|
|コントロール イベント|コントロールが選択されると、次の順序でイベントが発生します。<br /><br /> 1.  `Enter`<br />2.  `GotFocus`<br /><br /> コントロールが選択解除されると、次の順序でイベントが発生します。<br /><br /> 1.  `Leave`<br />2.  `Validating`<br />3.  `Validated`<br />4.  `LostFocus`|
|コントロールの拡大縮小|ドキュメントのズーム設定を 100% 以外の値に変更すると、コントロールは無効になりますが、ドキュメントでは拡大縮小しているように見えます。 たとえば、ドキュメントのズームが 130% のときにボタンをクリックすると、ズームが 100% に設定されるまでコントロールが無効になっていることを示すメッセージが表示されます。 ズームを 100% に変更すると、コントロールが正しく機能します。|
|コントロールのプロパティ値|Windows フォーム上のコントロールのプロパティは、整数値に設定されますが、Word 文書上のコントロールでは単精度に設定されます。 Excel では、コントロールのプロパティ値は倍精度に設定されます。 ワークシート上のコントロールの `Height` および `Width` プロパティがワークシートまたは画面のサイズを超える場合、その値は切り捨てられます。|
|コントロールのサイズ変更|8 個のサイズ変更ハンドルのいずれかを使用してドキュメント上のコントロールのサイズを変更した場合、コントロールがもう一度選択されるまで、新しいコントロールの寸法は **[プロパティ]** ウィンドウに反映されません。|
|コントロールの動作|ワークシート ウィンドウが分割されると、Excel ワークシート上のコントロールが予期しない動作をする場合があります。 たとえば、ワークシート上の <xref:Microsoft.Office.Tools.Excel.Controls.TextBox> へのアクセスは、いずれかのウィンドウでしかできない場合があります。|
|コントロールの名前付け|コントロールの名前に予約語は使用できません。 たとえば、<xref:Microsoft.Office.Tools.Excel.Controls.Button> をワークシートに追加し、名前を **System** に変更すると、プロジェクトをビルドするときにエラーが発生します。|
|プログラムによるコントロールの追加|実行時にコントロールのコンストラクターを使用してドキュメントにコントロールを追加しないでください。 代わりに、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によって提供されるヘルパー メソッドを使用します。 たとえば、ワークシートにボタンを追加するには、<xref:Microsoft.Office.Tools.Excel.ControlExtensions.AddButton%2A> メソッドを使用します。 これらのヘルパー メソッドでサポートされていないコントロールを追加する場合は、`AddControl` メソッドを使用できます。 詳細については、「[実行時に Office 文書にコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)」を参照してください。|
|コントロールのコピー|実行時に Windows フォーム コントロールをコピーしてドキュメントに貼り付けると、空のコンテナー ActiveX コントロールがドキュメントに貼り付けられます。 Windows フォーム コントロールは新しい位置に表示されず、元のコントロールの背後にあるコードはコンテナー ActiveX コントロールにコピーされません。|

## <a name="limitations-in-document-level-projects"></a>ドキュメントレベルのプロジェクトでの制限事項

Windows フォーム コントロールの使用に関する制限事項には、ドキュメントレベルのプロジェクトに固有のものがあります。

### <a name="control-support-at-design-time"></a>デザイン時のコントロールのサポート

Visual Studio デザイナーで Excel ワークシートまたは Word 文書を開いたときに、特定の Windows フォーム コントロールが **ツールボックス** から削除されます。 これは、技術的な制限のため、または Word または Excel 内でその機能が既に使用可能になっているためです。 Excel および Word プロジェクトでは、ドキュメントにフォーカスがあるときに **ツールボックス** に表示されるすべての Windows フォーム コントロールとその他のコンポーネントがサポートされます。また、ワークシートまたはドキュメントにサードパーティ製のコントロールを追加することもできます。

> [!NOTE]
> ドキュメントが保護されている場合は、すべてのコントロールが **ツールボックス** から削除されます。 ドキュメントの保護の詳細については、「[ドキュメントレベルのソリューションにおけるドキュメントの保護](../vsto/document-protection-in-document-level-solutions.md)」を参照してください。

> [!NOTE]
> サードパーティ製のコントロールを Office ソリューションで使用するには、その <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性が **true** に設定されている必要があります。

**ツールボックス** では、次のコントロールとコンポーネントは使用できません。

- <xref:System.Windows.Forms.BindingNavigator>

- <xref:System.Windows.Forms.ContextMenuStrip>

- <xref:System.Windows.Forms.DataGrid>

- <xref:System.DirectoryServices.DirectoryEntry>

- <xref:System.DirectoryServices.DirectorySearcher>

- <xref:System.Windows.Forms.ErrorProvider>

- <xref:System.Diagnostics.EventLog>

- <xref:System.IO.FileSystemWatcher>

- <xref:System.Windows.Forms.FlowLayoutPanel>

- <xref:System.Windows.Forms.GroupBox>

- <xref:System.Windows.Forms.MainMenu>

- <xref:System.Windows.Forms.MenuStrip>

- <xref:System.Messaging.MessageQueue>

- <xref:System.Windows.Forms.NotifyIcon>

- <xref:System.Windows.Forms.PageSetupDialog>

- <xref:System.Windows.Forms.Panel>

- <xref:System.Diagnostics.PerformanceCounter>

- <xref:System.Windows.Forms.PrintDialog>

- <xref:System.Drawing.Printing.PrintDocument>

- <xref:System.Windows.Forms.PrintPreviewControl>

- <xref:System.Diagnostics.Process>

- <xref:System.Windows.Forms.RichTextBox>

- <xref:System.IO.Ports.SerialPort>

- <xref:System.ServiceProcess.ServiceController>

- <xref:System.Windows.Forms.SplitContainer>

- <xref:System.Windows.Forms.Splitter>

- <xref:System.Windows.Forms.StatusBar>

- <xref:System.Windows.Forms.StatusStrip>

- <xref:System.Windows.Forms.TabControl>

- <xref:System.Windows.Forms.TableLayoutPanel>

- <xref:System.Timers.Timer>

- <xref:System.Windows.Forms.Timer>

- <xref:System.Windows.Forms.ToolBar>

- <xref:System.Windows.Forms.ToolStrip>

- <xref:System.Windows.Forms.ToolStripContainer>

- <xref:System.Windows.Forms.ToolStripDropDown>

- <xref:System.Windows.Forms.ToolStripDropDownMenu>

- <xref:System.Windows.Forms.ToolStripPanel>

### <a name="support-for-legacy-activex-controls"></a>従来の ActiveX コントロールのサポート

ActiveX コントロールを含む既存の Word 文書または Excel ブックを使用するドキュメントレベルの Office プロジェクトを作成する場合、ActiveX コントロールの機能は失われません。ただし、Visual Studio 内からドキュメントに新しい ActiveX コントロールを追加することはサポートされていません。 たとえば、Word 文書に Visual Basic for Applications (VBA) マクロを実行する **コントロール** ツールボックスのボタンがある場合、Office プロジェクトでドキュメントが使用された後も、マクロは引き続き実行されます。 ただし、ActiveX コントロールと VBA マクロを削除して、Windows フォーム コントロールとマネージド コードに置き換えることをお勧めします。

## <a name="see-also"></a>関連項目

- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [Office ドキュメントでの Windows フォーム コントロールの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [実行時に Office ドキュメントにコントロールを追加する](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [方法: Office ドキュメントに Windows フォーム コントロールを追加する](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
