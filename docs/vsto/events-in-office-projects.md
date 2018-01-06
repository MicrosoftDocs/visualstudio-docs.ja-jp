---
title: "Office プロジェクトのイベント |Microsoft ドキュメント"
ms.custom: 
ms.date: 02/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: office-development
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Sheet1_Startup
- ThisDocument_Shutdown
- ThisDocument_Startup
- application-level add-ins [Office development in Visual Studio], events
- event handlers [Office development in Visual Studio]
- ThisWorkbook_Startup
- Sheet2_Startup
- ThisWorkbook_Shutdown
- document-level customizations [Office development in Visual Studio], events
- Sheet2_Shutdown
- Startup event
- Sheet3_Shutdown
- add-ins [Office development in Visual Studio], events
- Shutdown event
- ThisAddIn_Startup
- Sheet3_Startup
- Startup method [Office development in Visual Studio]
- Shutdown method [Office development in Visual Studio]
- Sheet1_Shutdown
- events [Office development in Visual Studio]
- ThisAddIn_Shutdown
ms.assetid: 666d7f23-ef85-4f2e-9cd3-258df5bdc6fd
caps.latest.revision: "51"
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload: office
ms.openlocfilehash: 87d1fe708d4090fc6d2dd9509a04d13e7a21e079
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="events-in-office-projects"></a>Office プロジェクトのイベント
  各 Office プロジェクト テンプレートは、自動的に複数のイベント ハンドラーを生成します。 ドキュメント レベルのカスタマイズに使用するイベント ハンドラーは、VSTO アドイン用のイベント ハンドラーとは若干異なります。  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
## <a name="document-level-projects"></a>ドキュメント レベルのプロジェクト  
 Visual Studio では、ドキュメント レベルのカスタマイズ内の新規または既存のドキュメントまたはワークシートの背後に生成されたコードを提供します。 このコードは 2 つの異なるイベントを発生させます。 **Startup** と **Shutdown**です。  
  
### <a name="startup-event"></a>Startup イベント  
 **Startup** イベントは、ドキュメントが実行中になり、アセンブリ内の初期化コードがすべて実行された後で、ホスト項目 (ドキュメント、ブックまたはワークシート) ごとに発生します。 これは、コードが実行されているクラスのコンストラクターで最後に実行されるイベントです。 ホスト項目の詳細については、「 [Host Items and Host Controls Overview](../vsto/host-items-and-host-controls-overview.md)」を参照してください。  
  
 ドキュメント レベルのプロジェクトを作成する場合、Visual Studio は生成されたコード ファイル内の **Startup** イベント用に次のイベント ハンドラーを作成します。  
  
-   Microsoft Office Word プロジェクトの場合、イベント ハンドラーの名前は `ThisDocument_Startup`です。  
  
-   Microsoft Office Excel プロジェクトの場合、イベント ハンドラーの名前は次のようになります。  
  
    -   `Sheet1_Startup`  
  
    -   `Sheet2_Startup`  
  
    -   `Sheet3_Startup`  
  
    -   `ThisWorkbook_Startup`  
  
### <a name="shutdown-event"></a>Shutdown イベント  
 **Shutdown** イベントは、コードが読み込まれるアプリケーション ドメインがアンロードされるときに、ホスト項目 (ドキュメントまたはワークシート) ごとに発生します。 これは、アンロード時にクラス内で呼び出される最後のイベントです。  
  
 ドキュメント レベルのプロジェクトを作成する場合、Visual Studio は生成されたコード ファイル内の **Shutdown** イベント用に次のイベント ハンドラーを作成します。  
  
-   Microsoft Office Word プロジェクトの場合、イベント ハンドラーの名前は `ThisDocument_Shutdown`です。  
  
-   Microsoft Office Excel プロジェクトの場合、イベント ハンドラーの名前は次のようになります。  
  
    -   `Sheet1_Shutdown`  
  
    -   `Sheet2_Shutdown`  
  
    -   `Sheet3_Shutdown`  
  
    -   `ThisWorkbook_Shutdown`  
  
> [!NOTE]  
>  ドキュメントの **Shutdown** イベント ハンドラー中にプログラムによってコントロールを削除しないでください。 **Shutdown** イベントが発生すると、ドキュメントの UI 要素は利用できなくなります。 アプリケーションが終了する前にコントロールを削除する場合は、 **BeforeClose** や **BeforeSave**などの別のイベント ハンドラーにコードを追加します。  
  
### <a name="event-handler-method-declarations"></a>イベント ハンドラー メソッドの宣言  
 イベント ハンドラー メソッドの宣言にはすべて次の同じ引数が渡されます。 *sender* と *e*です。 Excel では、 *sender* 引数は `Sheet1` や `Sheet2`などのシートを参照します。Word では、 *sender* 引数はドキュメントを参照します。 *e* 引数は、ここでは使用されませんが、イベントの標準の引数を参照します。  
  
 次のコード例は、Word のドキュメント レベルのプロジェクト内にある既定のイベント ハンドラーを示します。  
  
 [!code-vb[Trin_VstcoreWordAutomation#121](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#121)]
 [!code-csharp[Trin_VstcoreWordAutomation#121](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#121)]  
  
 次のコード例は、Excel のドキュメント レベルのプロジェクト内にある既定のイベント ハンドラーを示します。  
  
> [!NOTE]  
>  次のコード例は、 `Sheet1` クラスのイベント ハンドラーを示します。 その他のホスト項目クラス内のイベント ハンドラーの名前は、クラス名に対応しています。 たとえば、 `Sheet2` クラスでは、 **Startup** イベント ハンドラーの名前は `Sheet2_Startup`です。 `ThisWorkbook`クラス、**スタートアップ**イベント ハンドラーの名前は`ThisWorkbook_Startup`します。  
  
 [!code-csharp[Trin_VstcoreExcelAutomation#83](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#83)]
 [!code-vb[Trin_VstcoreExcelAutomation#83](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#83)]  
  
### <a name="order-of-events-in-document-level-excel-projects"></a>ドキュメント レベルの Excel プロジェクト内のイベントの順序  
 Excel プロジェクト内の **Startup** イベント ハンドラーは、次の順序で呼び出されます。  
  
1.  `ThisWorkbook_Startup`。  
  
2.  `Sheet1_Startup`。  
  
3.  `Sheet2_Startup`。  
  
4.  `Sheet3_Startup`。  
  
5.  順にその他のシート。  
  
 ブック ソリューション内の **Shutdown** イベント ハンドラーは、次の順序で呼び出されます。  
  
1.  `ThisWorkbook_Shutdown`。  
  
2.  `Sheet1_Shutdown`。  
  
3.  `Sheet2_Shutdown`。  
  
4.  `Sheet3_Shutdown`。  
  
5.  順にその他のシート。  
  
 順序は、プロジェクトがコンパイルされるときに決定されます。 ユーザーが実行時にシートを再配置した場合、次にブックが開くまたは閉じるときにイベントが発生する順序は変更されません。  
  
## <a name="vsto-add-in-projects"></a>VSTO アドイン プロジェクト  
 Visual Studio は、VSTO アドインで生成されたコードを提供します。このコードは 2 つの異なるイベントを発生させます。 <xref:Microsoft.Office.Tools.AddInBase.Startup> と <xref:Microsoft.Office.Tools.AddInBase.Shutdown>です。  
  
### <a name="startup-event"></a>Startup イベント  
 <xref:Microsoft.Office.Tools.AddIn.Startup> イベントは、VSTO アドインが読み込まれ、アセンブリ内のすべての初期化コードが実行された後に発生します。 このイベントは、生成されたコード ファイル内の `ThisAddIn_Startup` メソッドによって処理されます。  
  
 `ThisAddIn_Startup` イベント ハンドラー内のコードは、VSTO アドインが <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> メソッドをオーバーライドしない限り、最初に実行されるユーザー コードです。 この場合、 `ThisAddIn_Startup` イベント ハンドラーが、 <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A>の後に呼び出されます。  
  
 コードを追加しないで、`ThisAdd-In_Startup`コードでは、ドキュメントを開く場合、イベント ハンドラー。 代わりに、ユーザーがドキュメントを作成するとき、または開くときに Office アプリケーションが発生させるイベントにそのコードを追加します。 詳細については、「 [Accessing a Document When the Office Application Starts](../vsto/programming-vsto-add-ins.md#AccessingDocuments)」を参照してください。  
  
 VSTO アドインの起動処理の詳細については、次を参照してください。[アーキテクチャの VSTO アドイン](../vsto/architecture-of-vsto-add-ins.md)です。  
  
### <a name="shutdown-event"></a>Shutdown イベント  
 <xref:Microsoft.Office.Tools.AddInBase.Shutdown> イベントは、コードが読み込まれるアプリケーション ドメインがアンロードされるときに発生します。 このイベントは、生成されたコード ファイル内の `ThisAddIn_Shutdown` メソッドによって処理されます。 このイベント ハンドラーは、VSTO アドインがアンロードされるときに最後に実行されるユーザー コードです。  
  
#### <a name="shutdown-event-in-outlook-vsto-add-ins"></a>Outlook VSTO アドインのシャットダウン イベント  
 <xref:Microsoft.Office.Tools.AddInBase.Shutdown> イベントは、ユーザーが Outlook の COM アドイン ダイアログ ボックスを使用して、VSTO アドインを無効にした場合にのみ発生します。 Outlook の終了時には発生しません。 Outlook の終了時に実行する必要のあるコードがある場合は、次のいずれかのイベントを処理します。  
  
-   <xref:Microsoft.Office.Interop.Outlook.ApplicationEvents_11_Event.Quit> オブジェクトの <xref:Microsoft.Office.Interop.Outlook.Application> イベント。  
  
-   <xref:Microsoft.Office.Interop.Outlook.ExplorerEvents_10_Event.Close> オブジェクトの <xref:Microsoft.Office.Interop.Outlook.Explorer> イベント。  
  
> [!NOTE]  
>  レジストリを変更して終了する場合、Outlook が <xref:Microsoft.Office.Tools.AddInBase.Shutdown> イベントを発生させるように強制することができます。 ただし、管理者がこの設定を元に戻す場合、 `ThisAddIn_Shutdown` メソッドに追加したコードは Outlook の終了時に実行されなくなります。 詳細については、 [[Outlook 2010 でのシャットダウンの変更]](http://go.microsoft.com/fwlink/?LinkID=184614)を参照してください。  
  
## <a name="see-also"></a>参照  
 [Office ソリューションの開発](../vsto/developing-office-solutions.md)   
 [方法: Visual Studio での Office プロジェクトの作成](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [ドキュメント レベルのカスタマイズのプログラミング](../vsto/programming-document-level-customizations.md)   
 [Programming VSTO Add-Ins](../vsto/programming-vsto-add-ins.md)   
 [Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)  
  
  