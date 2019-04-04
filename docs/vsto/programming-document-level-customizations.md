---
title: プログラムのドキュメント レベルのカスタマイズ
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- Sheet3
- thisWorkbook
- thisDocument
- Sheet1
- Sheet2
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ThisDocument class
- Sheet3 class
- ThisWorkbook class
- writing code for Office solutions
- programming [Office development in Visual Studio], document-level customizations
- Sheet1 class
- Office applications [Office development in Visual Studio], document-level customizations
- Sheet2 class
- document-level customizations [Office development in Visual Studio], programming
- application development [Office development in Visual Studio], document-level customizations
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0815ccf781782a0d638fcf941a6e48edcf8ccd1f
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56624686"
---
# <a name="program-document-level-customizations"></a>プログラムのドキュメント レベルのカスタマイズ
  ドキュメント レベルのカスタマイズを使用して、Microsoft Office Word または Microsoft Office Excel を拡張する場合に、次のタスクを実行できます。

- オブジェクト モデルを使用してアプリケーションを自動化します。

- ドキュメントの画面にコントロールを追加します。

- カスタマイズ アセンブリから、ドキュメント内に Visual Basic for Applications (VBA) コードを呼び出します。

- VBA からカスタマイズ アセンブリ内のコードを呼び出します。

- Microsoft Office がインストールされていないサーバー上にドキュメントがあるときに、そのドキュメントの特定の要素を管理します。

- アプリケーションのユーザー インターフェイス (UI) をカスタマイズします。

  [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

  ドキュメント レベルのプロジェクトのコードの記述には、Visual Studio の他のプロジェクトの種類とは異なる点があります。 相違点の多くは、Office オブジェクト モデルがマネージド コードに公開される方法に起因しています。 詳細については、[Office ソリューションでコードを記述](../vsto/writing-code-in-office-solutions.md)を参照してください。

  Visual Studio の Office 開発ツールを使用して作成できますドキュメント レベルのカスタマイズとその他の種類のソリューションに関する一般的な情報は、[Office ソリューション開発の概要&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)を参照してください。

## <a name="use-the-generated-classes-in-document-level-projects"></a>ドキュメント レベルのプロジェクトで生成されたクラスを使用します。
 ドキュメント レベルのプロジェクトを作成するときに、Visual Studio は、コードの記述を開始できるプロジェクト クラスを自動的に生成します。 Visual Studio は、Word と Excel 用のさまざまなクラスを生成します。

- Word 用のドキュメント レベルのプロジェクトでは、クラスは既定で `ThisDocument` と呼ばれます。

- Excel 用のドキュメント レベルのプロジェクトには、生成されたクラスが複数あり、ワークブック自体のために 1 つ、各ワークシート用に 1 つずつです。 既定では、それらのクラスの名前は次のようになります。

  -   `ThisWorkbook`

  -   `Sheet1`

  -   `Sheet2`

  -   `Sheet3`

  生成されたクラスには、ドキュメントを開いたり閉じたりしたときに呼び出されるイベント ハンドラーが含まれています。 ドキュメントを開いたときにコードを実行するには、 `Startup` イベント ハンドラーにコードを追加します。 ドキュメントを閉じたときにコードを実行するには、 `Shutdown` イベント ハンドラーにコードを追加します。 詳細については、[Office プロジェクト内のイベント](../vsto/events-in-office-projects.md)を参照してください。

### <a name="understand-the-design-of-the-generated-classes"></a>生成されたクラスの設計を理解します。
 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] または [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]を対象とするプロジェクトでは、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] のホスト項目の種類はインターフェイスなので、生成されたクラスがそこから実装を派生させることはできません。 代わりに、生成されたクラスでは、次の基本クラスからそのほとんどのメンバーが派生します。

- `ThisDocument`: <xref:Microsoft.Office.Tools.Word.DocumentBase>から派生します。

- `ThisWorkbook`: <xref:Microsoft.Office.Tools.Excel.WorkbookBase>から派生します。

- `Sheet` *n*: から派生した<xref:Microsoft.Office.Tools.Excel.WorksheetBase>します。

  これらの基本クラスは、そのメンバーのすべての呼び出しを [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]の対応するホスト項目インターフェイスの内部実装にリダイレクトします。 たとえば、 <xref:Microsoft.Office.Tools.Word.DocumentBase.Protect%2A> クラスの `ThisDocument` メソッドを呼び出す場合、 <xref:Microsoft.Office.Tools.Word.DocumentBase> クラスはこの呼び出しを <xref:Microsoft.Office.Tools.Word.Document> の [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]インターフェイスの内部実装にリダイレクトします。

## <a name="access-the-object-model-of-the-host-application"></a>ホスト アプリケーションのオブジェクト モデルへのアクセスします。
 ホスト アプリケーションのオブジェクト モデルにアクセスするには、プロジェクト内で生成されたクラスのメンバーを使用します。 これらの各クラスは Excel または Word のオブジェクト モデル内のオブジェクトに対応しており、同じプロパティ、メソッド、およびイベントのほとんどが含まれています。 たとえば、Word のドキュメント レベルのプロジェクトの `ThisDocument` クラスは、Word オブジェクト モデルの <xref:Microsoft.Office.Interop.Word.Document> オブジェクトとほとんど同じメンバーを提供します。

 次のコード例では、Word オブジェクト モデルを使用して、Word のドキュメント レベルのカスタマイズの一部であるドキュメントを保存する方法を示します。 この例は `ThisDocument` クラスから実行することを意図しています。

```vb
Me.Save()
```

```csharp
this.Save();
```

 同じ処理を `ThisDocument` クラスの外から行うには、 `Globals` オブジェクトを使用して `ThisDocument` クラスにアクセスします。 たとえば、[操作] ウィンドウ UI に **[保存]** ボタンUI を組み込む場合は、このコードを [操作] ウィンドウのコード ファイルに追加します。

```vb
Globals.ThisDocument.Save()
```

```csharp
Globals.ThisDocument.Save();
```

 `ThisDocument` クラスはそのほとんどのメンバーを <xref:Microsoft.Office.Tools.Word.Document> ホストの項目から取得するので、実際には、このコードで呼び出される `Save` メソッドは <xref:Microsoft.Office.Tools.Word.Document.Save%2A> ホスト項目の <xref:Microsoft.Office.Tools.Word.Document> メソッドです。 このメソッドは、Word オブジェクト モデルの <xref:Microsoft.Office.Interop.Word._Document.Save%2A> オブジェクトの <xref:Microsoft.Office.Interop.Word.Document> メソッドに対応しています。

 Word および Excel のオブジェクト モデルの使用に関する詳細については、[Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)と[Excel オブジェクト モデルの概要](../vsto/excel-object-model-overview.md)を参照してください。

 詳細については、`Globals`オブジェクトを参照してください[Office プロジェクト内のオブジェクトへのアクセスをグローバル](../vsto/global-access-to-objects-in-office-projects.md)します。

## <a name="add-controls-to-documents"></a>ドキュメントにコントロールを追加します。
 ドキュメントの UI をカスタマイズするには、Windows フォーム コントロールまたは *ホスト コントロール* をドキュメントの画面に追加します。 さまざまな種類のコントロールを組み合わせ、コードを記述することによって、コントロールのデータへのバインド、ユーザー情報の収集、およびユーザーの操作への応答を実行できます。

 ホスト コントロールは Word オブジェクト モデルと Excel オブジェクト モデルの一部のオブジェクトを拡張するクラスです。 たとえば、 <xref:Microsoft.Office.Tools.Excel.ListObject> ホスト コントロールには、Excel の <xref:Microsoft.Office.Interop.Excel.ListObject> のすべての機能が用意されています。 ただし、 <xref:Microsoft.Office.Tools.Excel.ListObject> ホスト コントロールには追加のイベントやデータ バインディング機能もあります。

 詳細については、[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)と[Windows フォームでコントロールの Office ドキュメントの概要](../vsto/windows-forms-controls-on-office-documents-overview.md)を参照してください。

## <a name="combine-vba-and-document-level-customizations"></a>VBA とドキュメント レベルのカスタマイズを結合します。
 ドキュメント レベルのカスタマイズの一部であるドキュメントに VBA コードを使用できます。 カスタマイズ アセンブリからドキュメント内の VBA コードを呼び出したり、ドキュメント内の VBA コードがカスタマイズ アセンブリのコードを呼び出せるようにプロジェクトを構成したりすることができます。

 詳細については、[結合 VBA とドキュメント レベルのカスタマイズ](../vsto/combining-vba-and-document-level-customizations.md)を参照してください。

## <a name="manage-documents-on-a-server"></a>管理サーバー上のドキュメント
 Microsoft Office Word または Microsoft Office Excel がインストールされていないサーバーで、ドキュメント レベルのカスタマイズのさまざまな要素を管理することができます。 たとえば、ドキュメントのデータ キャッシュにあるデータにアクセスし、変更することができます。 また、ドキュメントに関連付けられているカスタマイズ アセンブリも管理できます。 たとえば、プログラムを使用してドキュメントからアセンブリを削除して、ドキュメントがコードを実行しないようにしたり、プログラムを使用してアセンブリをドキュメントにアタッチすることができます。

 詳細については、[ServerDocument クラスを使用してサーバー上のドキュメントを管理](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)を参照してください。

## <a name="customize-the-user-interface-of-microsoft-office-applications"></a>Microsoft Office アプリケーションのユーザー インターフェイスをカスタマイズします。
 ドキュメント レベルのカスタマイズを使用して、次の方法で、Excel や Word の UI をカスタマイズできます。

- ホスト コントロールまたは Windows フォーム コントロールをドキュメントの画面に追加します。

   詳細については、次を参照してください[拡張オブジェクトを使用して Word の自動化](../vsto/automating-word-by-using-extended-objects.md)、[拡張オブジェクトを使用して Excel の自動化](../vsto/automating-excel-by-using-extended-objects.md)、および[Windows フォーム コントロールの Office ドキュメントの概要](../vsto/windows-forms-controls-on-office-documents-overview.md).

- 文書に操作ウィンドウを追加する。

   詳細については、[操作ウィンドウの概要](../vsto/actions-pane-overview.md)を参照してください。

- リボンにカスタム タブを追加します。

   詳細については、[リボンの概要](../vsto/ribbon-overview.md)を参照してください。

- リボン上の組み込みタブにカスタム グループを追加します。

   詳細については、「[方法 :組み込みタブをカスタマイズする](../vsto/how-to-customize-a-built-in-tab.md)します。

  UI の Microsoft Office アプリケーションのカスタマイズに関する詳細については、[Office UI のカスタマイズ](../vsto/office-ui-customization.md)を参照してください。

## <a name="get-extended-objects-from-native-office-objects-in-document-level-customizations"></a>ドキュメント レベルのカスタマイズでネイティブな Office オブジェクトから拡張オブジェクトを取得します。
 Office イベントの多くのイベント ハンドラーでは、イベントが発生するワークブック、ワークシート、またはドキュメントを表すネイティブの Office オブジェクトを受け取ります。 場合によっては、いくつかのコードはドキュメント レベルのカスタマイズでワークブックやドキュメントによってイベントが発生した場合のみ実行します。 たとえば、Excel のドキュメント レベルのカスタマイズでは、カスタマイズされたワークブック内でワークシートを 1 つアクティブ化したときに一部のコードを実行し、同時に開いている他のワークブックでワークシートをアクティブ化したときには実行しないようにします。

 ネイティブの Office オブジェクトがある場合は、そのオブジェクトがドキュメント レベルのカスタマイズで *ホスト項目* または *ホスト コントロール* に拡張されているかどうかをテストできます。 ホスト項目とホスト コントロールは、Word または Excel オブジェクト モデルにネイティブで存在するオブジェクト ( [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ネイティブの Office オブジェクト *) に機能を追加する*が提供する種類のインスタンスです。 総称して、ホスト項目とホスト コントロールは *拡張オブジェクト*とも呼ばれます。 ホスト項目とホスト コントロールの詳細については、[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)を参照してください。

## <a name="understand-the-getvstoobject-and-hasvstoobject-methods"></a>Getvstoobject メソッドと HasVstoObject メソッドを理解します。
 ネイティブの Office オブジェクトをテストするには、プロジェクト内で `HasVstoObject` メソッドと `GetVstoObject` メソッドを使用します。

- カスタマイズでネイティブの Office オブジェクトに拡張オブジェクトがあるかどうかを判断するには、`HasVstoObject` メソッドを使用します。 このメソッドは、ネイティブの Office オブジェクトに拡張オブジェクトがある場合は **true** を返し、ない場合は **false** を返します。

- ネイティブの Office オブジェクトに対する拡張オブジェクトを取得する場合は、`GetVstoObject` メソッドを使用します。 このメソッドは、指定したネイティブの Office オブジェクトに拡張オブジェクトがあれば、 <xref:Microsoft.Office.Tools.Excel.ListObject>、 <xref:Microsoft.Office.Tools.Excel.Workbook>、 <xref:Microsoft.Office.Tools.Excel.Worksheet>、または <xref:Microsoft.Office.Tools.Word.Document> オブジェクトを返します。 それ以外の場合、`GetVstoObject`返します**null**します。 たとえば、`GetVstoObject` メソッドは、指定した <xref:Microsoft.Office.Interop.Word.Document> が Word ドキュメント プロジェクトのドキュメントで基礎となるオブジェクトの場合、<xref:Microsoft.Office.Tools.Word.Document> を返します。

  ドキュメント レベルのプロジェクトで使用することはできません、`GetVstoObject`新たに作成するメソッド<xref:Microsoft.Office.Tools.Excel.Workbook>、 <xref:Microsoft.Office.Tools.Excel.Worksheet>、または<xref:Microsoft.Office.Tools.Word.Document>実行時にホスト項目。 このメソッドは、デザイン時にプロジェクトで生成される既存のホスト項目へのアクセスにのみ使用できます。 実行時に新しいホスト項目を作成する場合は、VSTO アドイン プロジェクトを開発する必要があります。 詳細については、[ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)と[拡張 Word 文書や Excel ブックを実行時に VSTO アドインで](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)を参照してください。

## <a name="use-the-getvstoobject-and-hasvstoobject-methods"></a>Getvstoobject メソッドと HasVstoObject メソッドを使用します。
 呼び出す、`HasVstoObject`と`GetVstoObject`メソッドを使用して、`Globals.Factory.GetVstoObject`または`Globals.Factory.HasVstoObject`メソッド、およびネイティブの Word または Excel オブジェクトを渡します (など、<xref:Microsoft.Office.Interop.Word.Document>または<xref:Microsoft.Office.Interop.Excel.Worksheet>) をテストします。

## <a name="see-also"></a>関連項目
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [VBA とドキュメント レベルのカスタマイズを結合します。](../vsto/combining-vba-and-document-level-customizations.md)
- [ServerDocument クラスを使用してサーバー上のドキュメントを管理します。](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [Office ソリューションにおけるコードの記述](../vsto/writing-code-in-office-solutions.md)
