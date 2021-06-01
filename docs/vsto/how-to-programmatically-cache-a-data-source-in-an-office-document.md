---
title: データ ソースをプログラムによって Office ドキュメント内にキャッシュする
description: ホスト項目の StartCaching メソッドを呼び出すことで、データ オブジェクトをプログラムによってドキュメント内のデータ キャッシュに追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], data
- datasets [Office development in Visual Studio], caching
- StartCaching method
- data caching [Office development in Visual Studio], programmatically
- data [Office development in Visual Studio], caching
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 070253fb7ec57bedad628e116ce193fa2d9cf50b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827592"
---
# <a name="how-to-programmatically-cache-a-data-source-in-an-office-document"></a>方法: データ ソースをプログラムによって Office ドキュメント内にキャッシュする
  ホスト項目 (<xref:Microsoft.Office.Tools.Word.Document>、<xref:Microsoft.Office.Tools.Excel.Workbook>、<xref:Microsoft.Office.Tools.Excel.Worksheet> など) の `StartCaching` メソッドを呼び出すことで、データ オブジェクトをプログラムによってドキュメント内のデータ キャッシュに追加することができます。 データ キャッシュからデータ オブジェクトを削除するには、ホスト項目の `StopCaching` メソッドを呼び出します。

 `StartCaching` メソッドと `StopCaching` メソッドはどちらもプライベートですが、IntelliSense には表示されます。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 `StartCaching` メソッドを使ってデータ オブジェクトをデータ キャッシュに追加する場合、<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性を使ってデータ オブジェクトを宣言する必要はありません。 ただし、データ オブジェクトをデータ キャッシュに追加するには、特定の要件を満たしている必要があります。 詳細については、「[キャッシュ データ](../vsto/caching-data.md)」を参照してください。

## <a name="to-programmatically-cache-a-data-object"></a>データ オブジェクトをプログラムによってキャッシュするには

1. データ オブジェクトは、メソッドの内部ではなく、クラス レベルで宣言します。 この例では、プログラムによってキャッシュする、`dataSet1` という名前の <xref:System.Data.DataSet> を宣言する場合を想定しています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet12":::

2. データ オブジェクトをインスタンス化し、ドキュメントまたはワークシート インスタンスの `StartCaching` メソッドを呼び出して、データ オブジェクトの名前を渡します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet13":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet13":::

## <a name="to-stop-caching-a-data-object"></a>データ オブジェクトのキャッシュを停止するには

1. ドキュメントまたはワークシート インスタンスの `StopCaching` メソッドを呼び出し、データ オブジェクトの名前を渡します。 この例では、キャッシュを停止する、`dataSet1` という名前の <xref:System.Data.DataSet> がある場合を想定しています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet14":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet14":::

    > [!NOTE]
    > ドキュメントまたはワークシートの `Shutdown` イベントのイベント ハンドラーから `StopCaching` を呼び出すことはしないでください。 `Shutdown` イベントが発生した時点で、データ キャッシュを変更できる状態ではなくなっています。 `Shutdown` イベントについて詳しくは、「[Office プロジェクトのイベント](../vsto/events-in-office-projects.md)」をご覧ください。

## <a name="see-also"></a>関連項目

- [キャッシュ データ](../vsto/caching-data.md)
- [方法: オフラインで使用するデータまたはサーバー上で使用するデータをキャッシュする](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [方法: パスワードで保護されたドキュメント内のデータをキャッシュする](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [サーバー上のドキュメント内のデータにアクセスする](../vsto/accessing-data-in-documents-on-the-server.md)
- [データを保存する](../data-tools/save-data-back-to-the-database.md)
