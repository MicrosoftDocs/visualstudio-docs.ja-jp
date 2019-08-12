---
title: カスタム作業ウィンドウ
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, task panes
- user interface panels [Office development in Visual Studio]
- task panes [Office development in Visual Studio]
- user interfaces [Office development in Visual Studio], custom task panes
- custom task panes [Office development in Visual Studio], creating
- task panes [Office development in Visual Studio]. multiple application windows
- custom task panes [Office development in Visual Studio], multiple application windows
- task panes [Office development in Visual Studio], creating
- application-level add-ins [Office development in Visual Studio], custom task panes
- multiple applications windows with custom task panes [Office development in Visual Studio]
- add-ins [Office development in Visual Studio], custom task panes
- custom task panes [Office development in Visual Studio]
- task panes [Office development in Visual Studio], about custom task panes
- custom task panes [Office development in Visual Studio], about custom task panes
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 766c93bb45380098af984db256d36d1e0948e56f
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926717"
---
# <a name="custom-task-panes"></a>カスタム作業ウィンドウ
  作業ウィンドウは、通常、Microsoft Office アプリケーションのウィンドウの一辺にドッキングされているユーザー インターフェイス ウィンドウです。 カスタム作業ウィンドウは、独自の作業ウィンドウを作成し、ユーザーがソリューションの各機能にアクセスする際に使い慣れたインターフェイスを利用できるようにするものです。 たとえば、インターフェイスにはドキュメントを変更するコードや、データ ソースのデータを表示するコードを実行するコントロールが含まれます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

> [!NOTE]
> カスタム作業ウィンドウは、操作ウィンドウとは異なります。 操作ウィンドウは、Microsoft Office Word および Microsoft Office Excel のドキュメント レベルのカスタマイズの一部です。 詳細については、「[操作ウィンドウの概要](../vsto/actions-pane-overview.md)」を参照してください。

## <a name="benefits-of-custom-task-panes"></a>カスタム作業ウィンドウの利点
 カスタム作業ウィンドウでは、使用する機能を使い慣れたユーザー インターフェイスに取り込むことができます。 Visual Studio のツールを使用して、カスタム作業ウィンドウをすばやく作成できます。

### <a name="familiar-user-interface"></a>使い慣れたユーザーインターフェイス
 Microsoft Office システムのアプリケーションのユーザーは、Word の **[スタイルと書式設定]** 作業ウィンドウなどの作業ウィンドウの使用に既に慣れています。 カスタム作業ウィンドウは Microsoft Office システムの他の作業ウィンドウと似た動作をします。 ユーザーは、アプリケーション ウィンドウのいずれかの辺にカスタム作業ウィンドウをドッキングすることができます。また、ウィンドウの任意の場所にカスタム作業ウィンドウをドラッグすることができます。 複数のカスタム作業ウィンドウを同時に表示できる VSTO アドインを作成することもできます。各作業ウィンドウは、ユーザーが個別に操作できます。

### <a name="windows-forms-support"></a>Windows フォームのサポート
 Visual Studio で Office 開発ツールを使用して作成したカスタム作業ウィンドウのユーザー インターフェイスは、Windows フォーム コントロールに基づいています。 使い慣れた Windows フォーム デザイナーを使用して、カスタム作業ウィンドウのユーザー インターフェイスを設計できます。 また、Windows フォームのデータ バインディング サポートを使用して、作業ウィンドウ上のコントロールにデータ ソースをバインドすることもできます。

## <a name="create-a-custom-task-pane"></a>カスタム作業ウィンドウの作成
 2 つの手順で、基本的なカスタム作業ウィンドウを作成できます。

1. Windows フォーム コントロールを <xref:System.Windows.Forms.UserControl> オブジェクトに追加することにより、カスタム作業ウィンドウのユーザー インターフェイスを作成します。

2. そのユーザー コントロールを VSTO アドインの <xref:Microsoft.Office.Tools.CustomTaskPaneCollection> オブジェクトに渡すことにより、カスタム作業ウィンドウをインスタンス化します。 このコレクションは、作業ウィンドウの外観を変更し、ユーザー イベントに応答するために使用できる新しい <xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトを返します。

   詳細については、「[方法 :カスタム作業ウィンドウをアプリケーション](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)に追加します。

### <a name="create-the-user-interface"></a>ユーザー インターフェイスを作成する
 Visual Studio の Office 開発ツールを使用して作成されるすべてのカスタム作業ウィンドウには、<xref:System.Windows.Forms.UserControl> オブジェクトが含まれます。 このユーザー コントロールは、カスタム作業ウィンドウのユーザー インターフェイスを提供します。 ユーザーコントロールは、デザイン時または実行時に作成できます。 デザイン時にユーザー コントロールを作成する場合は、Windows フォーム デザイナーを使用して、作業ウィンドウのユーザー インターフェイスを作成できます。

### <a name="instantiate-the-custom-task-pane"></a>カスタム作業ウィンドウのインスタンス化
 カスタム作業ウィンドウのユーザー インターフェイスが含まれるユーザー コントロールを作成した後に、<xref:Microsoft.Office.Tools.CustomTaskPane> をインスタンス化する必要があります。 これを実行するには、いずれかの <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A> メソッドを呼び出すことにより、ユーザー コントロールを VSTO アドインの <xref:Microsoft.Office.Tools.CustomTaskPaneCollection> に渡します。 このコレクションは、`ThisAddIn` クラスの `CustomTaskPanes` フィールドとして公開されます。 次のコード例は `ThisAddIn` クラスから実行することを意図しています。

 [!code-vb[Trin_TaskPaneBasic#2](../vsto/codesnippet/VisualBasic/Trin_TaskPaneBasic/ThisAddIn.vb#2)]
 [!code-csharp[Trin_TaskPaneBasic#2](../vsto/codesnippet/CSharp/Trin_TaskPaneBasic/ThisAddIn.cs#2)]

 <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A> メソッドは、新しい <xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトを返します。 このオブジェクトを使用して、作業ウィンドウの外観を変更したり、ユーザー イベントに応答したりできます。

### <a name="control-the-task-pane-in-multiple-windows"></a>複数のウィンドウで作業ウィンドウを制御する
 カスタム作業ウィンドウは、ドキュメント フレーム ウィンドウに関連付けられます。ドキュメント フレーム ウィンドウは、ドキュメントや項目をユーザーに表示するものです。 作業ウィンドウは、関連付けられたウィンドウが表示されている場合にのみ表示されます。

 どのウィンドウが作業ウィンドウを表示するのかを決定するには、作業ウィンドウを作成するときに適切な <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A> メソッド オーバーロードを使用します。

- 作業ウィンドウをアクティブなウィンドウに関連付けるには、<xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A> メソッドを使用します。

- 指定したウィンドウでホストされているドキュメントに作業ウィンドウを関連付けるには、<xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A> メソッドを使用します。

  一部の Office アプリケーションでは、複数のウィンドウが開いているときに作業ウィンドウを作成する、または表示するタイミングについて、明示的な命令が必要です。 その場合、作業ウィンドウがアプリケーションで確実に適切なドキュメントや項目に表示されるようにするために、カスタム作業ウィンドウをコードのどこでインスタンス化するかを検討することが重要になります。 詳細については、「[アプリケーションウィンドウでのカスタム作業ウィンドウの管理](#Managing)」を参照してください。

## <a name="access-the-application-from-the-task-pane"></a>作業ウィンドウからアプリケーションにアクセスする
 ユーザー コントロールからアプリケーションを自動化する場合、コード内の `Globals.ThisAddIn.Application` を使用して、オブジェクト モデルに直接アクセスできます。 静的な `Globals` クラスは、`ThisAddIn` オブジェクトへのアクセスを提供します。 このオブジェクトの `Application` フィールドは、アプリケーションのオブジェクト モデルへのエントリ ポイントです。

 オブジェクトのフィールド`Application`の詳細については、「[プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)」を参照してください。 `ThisAddIn`カスタム作業ウィンドウからアプリケーションを自動化する方法を示すチュートリアルについては、 [「チュートリアル:カスタム作業ウィンドウ](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)からのアプリケーションの自動適用。 クラスの`Globals`詳細については、「 [Office プロジェクト内のオブジェクトへのグローバルアクセス](../vsto/global-access-to-objects-in-office-projects.md)」を参照してください。

## <a name="manage-the-user-interface-of-the-task-pane"></a>作業ウィンドウのユーザーインターフェイスの管理
 作業ウィンドウを作成した後に、<xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトのプロパティとイベントを使用して、作業ウィンドウのユーザー インターフェイスを制御したり、ユーザーが作業ウィンドウを変更したときに対応したりすることができます。

### <a name="make-the-custom-task-pane-visible"></a>カスタム作業ウィンドウを表示する
 既定では、作業ウィンドウは表示されません。 作業ウィンドウが表示されるようにするには<xref:Microsoft.Office.Tools.CustomTaskPane.Visible%2A> 、プロパティを**true**に設定する必要があります。

 ユーザーは、作業ウィンドウの隅にある **[閉じる]** ボタン (X) をクリックすることで、いつでも作業ウィンドウを閉じることができます。 ただし、ユーザーがもう一度、カスタム作業ウィンドウを開くための既定の方法はありません。 ユーザーがカスタム作業ウィンドウを閉じた場合、それを表示する方法を提供しない限り、そのユーザーはカスタム作業ウィンドウを再度表示することはできません。

 VSTO アドインでカスタム作業ウィンドウを作成する場合は、ユーザーがクリックしてカスタム作業ウィンドウを表示したり非表示にできる UI 要素 (ボタンなど) も作成する必要があります。 リボンのカスタマイズをサポートする Microsoft Office アプリケーションでカスタム作業ウィンドウを作成する場合は、カスタム作業ウィンドウを表示したり非表示にしたりするボタンを持つコントロール グループをリボンに追加できます。 これを行う方法を示すチュートリアルについては[、「チュートリアル:カスタム作業ウィンドウをリボンボタン](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)と同期します。

 リボンのカスタマイズをサポートしない Microsoft Office アプリケーションでカスタム作業ウィンドウを作成する場合は、カスタム作業ウィンドウを表示または非表示にする <xref:Microsoft.Office.Core.CommandBarButton> を追加できます。

### <a name="modify-the-appearance-of-the-task-pane"></a>作業ウィンドウの外観を変更する
 <xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトのプロパティを使用して、カスタム作業ウィンドウの位置とサイズを制御できます。 カスタム作業ウィンドウに含まれている <xref:System.Windows.Forms.UserControl> オブジェクトのプロパティを使用して、カスタム作業ウィンドウの外観に、他の多くの変更を行うことができます。 たとえば、ユーザー コントロールの <xref:System.Windows.Forms.Control.BackgroundImage%2A> プロパティを使用して、カスタム作業ウィンドウの背景画像を指定できます。

 次の表に、<xref:Microsoft.Office.Tools.CustomTaskPane> プロパティを使用してカスタム作業ウィンドウに加えることができる変更をリストします。

|タスク|プロパティ|
|----------|--------------|
|作業ウィンドウのサイズを変更する|<xref:Microsoft.Office.Tools.CustomTaskPane.Height%2A><br /><br /> <xref:Microsoft.Office.Tools.CustomTaskPane.Width%2A>|
|作業ウィンドウの場所を変更するには|<xref:Microsoft.Office.Tools.CustomTaskPane.DockPosition%2A>|
|作業ウィンドウを非表示にする、または表示されるようにするには|<xref:Microsoft.Office.Tools.CustomTaskPane.Visible%2A>|
|ユーザーが作業ウィンドウの場所を変更できないようにするには|<xref:Microsoft.Office.Tools.CustomTaskPane.DockPositionRestrict%2A>|

### <a name="program-custom-task-pane-events"></a>プログラムのカスタム作業ウィンドウイベント
 ユーザーがカスタム作業ウィンドウを変更するときに、VSTO アドインが応答するようにしたい場合があります。 たとえば、ユーザーがウィンドウの向きを縦方向から横方向に変更した場合にコントロールの位置を変更するという局面が考えられます。

 次の表に、ユーザーがカスタム作業ウィンドウに加える変更に応答するために利用できるイベントを示します。

|タスク|event|
|----------|-----------|
|ユーザーが作業ウィンドウの場所を変更したときに応答するには|<xref:Microsoft.Office.Tools.CustomTaskPane.DockPositionChanged>|
|ユーザーが作業ウィンドウを非表示にしたり、表示させた場合に応答するには|<xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged>|

## <a name="clean-up-resources-used-by-the-task-pane"></a>作業ウィンドウで使用されるリソースをクリーンアップする
 カスタム作業ウィンドウを作成した後、<xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトは VSTO アドインが実行されている限りメモリに残ります。 ユーザーが作業ウィンドウの隅にある **[閉じる]** ボタン (X) をクリックしても、オブジェクトはメモリに残ります。

 VSTO アドインがまだ実行している間に、作業ウィンドウで使用されたリソースをクリーンアップするには、<xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Remove%2A> または <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.RemoveAt%2A> メソッドを使用します。 これらのメソッドは、指定された <xref:Microsoft.Office.Tools.CustomTaskPane> オブジェクトを `CustomTaskPanes` コレクションから削除し、オブジェクトの <xref:Microsoft.Office.Tools.CustomTaskPane.Dispose%2A> メソッドを呼び出します。

 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] は VSTO アドインがアンロードされるときに、カスタム作業ウィンドウで使用されたリソースを自動的にクリーンアップします。 プロジェクトの`ThisAddIn_Shutdown`イベントハンドラー <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Remove%2A>で<xref:Microsoft.Office.Tools.CustomTaskPaneCollection.RemoveAt%2A>メソッドまたはメソッドを呼び出さないでください。 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] は、`ThisAddIn_Shutdown` が呼び出される前に、<xref:Microsoft.Office.Tools.CustomTaskPane> で使用されているリソースをクリーンアップするため、これらのメソッドにより <xref:System.ObjectDisposedException> がスローされます。 の詳細`ThisAddIn_Shutdown`については、「 [Office プロジェクトのイベント](../vsto/events-in-office-projects.md)」を参照してください。

## <a name="Managing"></a>複数のアプリケーションウィンドウでカスタム作業ウィンドウを管理する
 複数のウィンドウを使用してドキュメントやその他の項目を表示するアプリケーションでカスタム作業ウィンドウを作成する場合、その作業ウィンドウをユーザーが必要とするときに確実に表示させるには、追加の手順を実行する必要があります。

 すべてのアプリケーションのカスタム作業ウィンドウは、ドキュメント フレーム ウィンドウと関連付けられます。このウィンドウは、ドキュメントや項目のビューをユーザーに表示します。 作業ウィンドウは、関連付けられたウィンドウが表示されている場合にのみ表示されます。 ただし、すべてのアプリケーションでドキュメント フレーム ウィンドウが同じ方法で使用されるわけではありません。

 次のアプリケーション グループには別の開発要件があります。

- [Outlook](#Outlook)

- [Word、InfoPath、PowerPoint](#WordAndInfoPath)

## <a name="Outlook"></a>Outlook
 Outlook 用のカスタム作業ウィンドウを作成するときには、カスタム作業ウィンドウが特定のエクスプローラーまたはインスペクター ウィンドウに関連付けられます。 エクスプローラーはフォルダーの内容を表示するウィンドウで、インスペクターとは、電子メールメッセージやタスクなどの項目を表示するウィンドウです。

 複数のエクスプ ローラーやインスペクターのウィンドウでカスタム作業ウィンドウを表示する場合は、エクスプ ローラーまたはインスペクター ウィンドウが開いたときに、カスタム作業ウィンドウの新しいインスタンスを作成する必要があります。 そのためには、エクスプ ローラーまたはインスペクター ウィンドウが作成されるときに発生するイベントを処理し、次に、イベント ハンドラーで作業ウィンドウを作成します。 どのウィンドウを表示させるかに応じて、作業ウィンドウを非表示にしたり表示させたりするように、エクスプ ローラーおよびインスペクターのイベントを処理することもできます。

 作業ウィンドウを特定のエクスプローラーまたはインスペクターに関連付けるには、 <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A>メソッドを使用して作業ウィンドウを作成し<xref:Microsoft.Office.Interop.Outlook.Explorer> 、 <xref:Microsoft.Office.Interop.Outlook.Inspector>オブジェクトまたはオブジェクトを*ウィンドウ*パラメーターに渡します。 カスタム作業ウィンドウの作成の詳細については、「[カスタム作業ウィンドウの概要](../vsto/custom-task-panes.md)」を参照してください。

- <xref:Microsoft.Office.Interop.Outlook.ExplorersEvents_Event.NewExplorer>

- <xref:Microsoft.Office.Interop.Outlook.ExplorerEvents_10_Event.Activate>

- <xref:Microsoft.Office.Interop.Outlook.ExplorerEvents_10_Event.Close>

- <xref:Microsoft.Office.Interop.Outlook.ExplorerEvents_10_Event.Deactivate>

  インスペクター ウィンドウの状態を監視するために、次のようなインスペクターに関連するイベントを処理できます。

- <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector>

- <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_10_Event.Activate>

- <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_10_Event.Close>

- <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_10_Event.Deactivate>

### <a name="prevent-multiple-instances-of-a-custom-task-pane-in-outlook"></a>Outlook でカスタム作業ウィンドウの複数のインスタンスを禁止する
 Outlook のウィンドウでカスタム作業ウィンドウの複数のインスタンスが表示されないようにするには、各ウィンドウが閉じられるときに `ThisAddIn` クラスの `CustomTaskPanes` コレクションからカスタム作業ウィンドウを明示的に削除します。 ウィンドウが閉じられるときに発生するイベント (<xref:Microsoft.Office.Interop.Outlook.ExplorerEvents_10_Event.Close> や <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_10_Event.Close> など) で <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Remove%2A> メソッドを呼び出します。

 カスタム作業ウィンドウを明示的に削除しない場合は、Outlook のウィンドウで、カスタム作業ウィンドウの複数のインスタンスが表示される可能性があります。 Outlook ではウィンドウが再利用されることがありますが、再利用されるウィンドウにアタッチされたカスタム作業ウィンドウがあった場合、その作業ウィンドウへの参照は再利用されるウィンドウに残ります。

## <a name="WordAndInfoPath"></a>Word、InfoPath、PowerPoint
 Word、InfoPath、および PowerPoint ではそれぞれのドキュメントが別々のドキュメント フレーム ウィンドウに表示されます。 これらのアプリケーションのカスタム作業ウィンドウを作成する場合、そのカスタム作業ウィンドウは特定のドキュメントにのみ関連付けられます。 ユーザーが別のドキュメントを開いた場合、前のドキュメントが再度表示されるまで、カスタム作業ウィンドウは非表示です。

 複数のドキュメントでカスタム作業ウィンドウを表示する場合は、ユーザーが新しいドキュメントを作成するか、既存のドキュメントを開くときに、カスタム作業ウィンドウの新しいインスタンスを作成します。 そのためには、ドキュメントが作成または開かれるときに発生するイベントを処理し、次にイベント ハンドラーで作業ウィンドウを作成します。 どのドキュメントを表示させるかに応じて作業ウィンドウを非表示にしたり表示させたりするように、ドキュメント イベントを処理することもできます。

 作業ウィンドウを特定のドキュメントウィンドウに関連付けるには、 <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A>メソッドを使用して作業ウィンドウを作成し、(Word <xref:Microsoft.Office.Interop.InfoPath.WindowObject>の場合)、(InfoPath の場合)、または[documentwindow](/previous-versions/office/developer/office-2010/ff762047(v=office.14)) (PowerPoint の場合) を*ウィンドウ*パラメーターに<xref:Microsoft.Office.Interop.Word.Window>渡します.

### <a name="word-events"></a>Word イベント
 Word のドキュメント ウィンドウの状態を監視するために、次のイベントを処理できます。

- <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeClose>

- <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen>

- <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.NewDocument>

- <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.WindowActivate>

- <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.WindowDeactivate>

### <a name="infopath-events"></a>InfoPath イベント
 InfoPath のドキュメント ウィンドウの状態を監視するために、次のイベントを処理できます。

- <xref:Microsoft.Office.Interop.InfoPath._ApplicationEvents_Event.NewXDocument>

- <xref:Microsoft.Office.Interop.InfoPath._ApplicationEvents_Event.WindowActivate>

- <xref:Microsoft.Office.Interop.InfoPath._ApplicationEvents_Event.WindowDeactivate>

- <xref:Microsoft.Office.Interop.InfoPath._ApplicationEvents_Event.XDocumentBeforeClose>

- <xref:Microsoft.Office.Interop.InfoPath._ApplicationEvents_Event.XDocumentOpen>

### <a name="powerpoint-events"></a>PowerPoint イベント
 PowerPoint のドキュメント ウィンドウの状態を監視するために、次のイベントを処理できます。

- [EApplication_Event (Microsoft......)](/previous-versions/office/developer/office-2010/ff761105(v%3doffice.14))

- [EApplication_Event が開かれています。](/previous-versions/office/developer/office-2010/ff762843(v%3doffice.14))

- [EApplication_Event. NewPresentation (Microsoft...](/previous-versions/office/developer/office-2010/ff761498(v%3doffice.14))

- [EApplication_Event が開かれています。](/previous-versions/office/developer/office-2010/ff760423(v=office.14))

- [EApplication_Event を有効にしてください。](/previous-versions/office/developer/office-2010/ff761153(v=office.14))

- [EApplication_Event............ WindowDeactivate](/previous-versions/office/developer/office-2010/ff763093(v=office.14))

## <a name="see-also"></a>関連項目
- [方法: カスタム作業ウィンドウをアプリケーションに追加する](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [チュートリアル: カスタム作業ウィンドウからのアプリケーションの自動化](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
- [チュートリアル: カスタム作業ウィンドウとリボンボタンの同期](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)
- [チュートリアル: Outlook で電子メールメッセージと共にカスタム作業ウィンドウを表示する](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)
