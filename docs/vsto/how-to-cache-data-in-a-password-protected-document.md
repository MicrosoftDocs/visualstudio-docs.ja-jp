---
title: '方法: パスワードで保護されたドキュメントにデータをキャッシュする'
description: パスワードで保護されたドキュメントやブック内のデータ キャッシュにデータを追加する場合は、プロジェクトで 2 つのメソッドをオーバーライドすることで、キャッシュされたデータへの変更を保存できます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], protected documents
- datasets [Office development in Visual Studio], caching
- data [Office development in Visual Studio], caching
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ccdb906022d4dcfc321af294eec59afa36832773
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824186"
---
# <a name="how-to-cache-data-in-a-password-protected-document"></a>方法: パスワードで保護されたドキュメントにデータをキャッシュする
  パスワードで保護されたドキュメントやブック内のデータ キャッシュにデータを追加した場合、キャッシュされたデータへの変更は自動的には保存されません。 キャッシュされたデータへの変更を保存するには、プロジェクトで 2 つのメソッドをオーバーライドします。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="caching-in-word-documents"></a>Word 文書でのキャッシュ

### <a name="to-cache-data-in-a-word-document-that-is-protected-with-a-password"></a>パスワードで保護された Word 文書にデータをキャッシュするには

1. `ThisDocument` クラスで、パブリックのフィールドまたはプロパティをキャッシュ対象としてマークします。 詳細については、「[データのキャッシュ](../vsto/caching-data.md)」を参照してください。

2. `ThisDocument` クラスの <xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A> メソッドをオーバーライドし、ドキュメントから保護を削除します。

     ドキュメントが保存されると、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によってこのメソッドが呼び出され、ドキュメントの保護を解除できるようになります。 これにより、キャッシュされたデータへの変更を保存できるようになります。

3. `ThisDocument` クラスの <xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A> メソッドをオーバーライドし、ドキュメントに保護を再適用します。

     ドキュメントが保存されると、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によってこのメソッドが呼び出され、ドキュメントに保護を再適用できるようになります。

### <a name="example"></a>例
 次のコード例は、パスワードで保護された Word 文書にデータをキャッシュする方法を示したものです。 このコードでは、<xref:Microsoft.Office.Tools.Word.DocumentBase.UnprotectDocument%2A> メソッドで保護を削除する前に、現在の <xref:Microsoft.Office.Tools.Word.Document.ProtectionType%2A> の値を保存します。これにより、<xref:Microsoft.Office.Tools.Word.DocumentBase.ProtectDocument%2A> メソッドで同じ種類の保護を再適用できるようになります。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_CachedDataProtectedDocument/ThisDocument.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedDocument/ThisDocument.vb" id="Snippet1":::

### <a name="compile-the-code"></a>コードのコンパイル
 このコードを、プロジェクトの `ThisDocument` クラスに追加します。 このコードでは、パスワードが `securelyStoredPassword` という名前のフィールドに格納されていることを前提としています。

## <a name="cache-in-excel-workbooks"></a>Excel ブックでのキャッシュ
 Excel プロジェクトでは、<xref:Microsoft.Office.Tools.Excel.Workbook.Protect%2A> メソッドを使ってブック全体をパスワードで保護する場合にのみ、この手順が必要になります。 <xref:Microsoft.Office.Tools.Excel.Worksheet.Protect%2A> メソッドを使って特定のワークシートだけをパスワードで保護する場合、この手順は必要ありません。

### <a name="to-cache-data-in-an-excel-workbook-that-is-protected-with-a-password"></a>パスワードで保護された Excel ブックにデータをキャッシュするには

1. `ThisWorkbook` クラス、またはいずれかの `Sheet`*n* クラスで、パブリックのフィールドまたはプロパティをキャッシュ対象としてマークします。 詳細については、「[データのキャッシュ](../vsto/caching-data.md)」を参照してください。

2. `ThisWorkbook` クラスの <xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A> メソッドをオーバーライドし、ブックから保護を削除します。

     ブックが保存されると、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によってこのメソッドが呼び出され、ブックの保護を解除できるようになります。 これにより、キャッシュされたデータへの変更を保存できるようになります。

3. `ThisWorkbook` クラスの <xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A> メソッドをオーバーライドし、ドキュメントに保護を再適用します。

     ブックが保存されると、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] によってこのメソッドが呼び出され、ブックに保護を再適用できるようになります。

### <a name="example"></a>例
 次のコード例は、パスワードで保護された Excel ブックにデータをキャッシュする方法を示したものです。 このコードでは、<xref:Microsoft.Office.Tools.Excel.WorkbookBase.UnprotectDocument%2A> メソッドで保護を削除する前に、現在の <xref:Microsoft.Office.Tools.Excel.Workbook.ProtectStructure%2A> および <xref:Microsoft.Office.Tools.Excel.Workbook.ProtectWindows%2A> の値を保存します。これにより、<xref:Microsoft.Office.Tools.Excel.WorkbookBase.ProtectDocument%2A> メソッドで同じ種類の保護を再適用できるようになります。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_CachedDataProtectedWorkbook/ThisWorkbook.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_CachedDataProtectedWorkbook/ThisWorkbook.cs" id="Snippet1":::

### <a name="compile-the-code"></a>コードのコンパイル
 このコードを、プロジェクトの `ThisWorkbook` クラスに追加します。 このコードでは、パスワードが `securelyStoredPassword` という名前のフィールドに格納されていることを前提としています。

## <a name="see-also"></a>こちらもご覧ください
- [キャッシュ データ](../vsto/caching-data.md)
- [方法: オフラインで使用するデータまたはサーバー上で使用するデータをキャッシュする](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [方法: Office ドキュメント内のデータ ソースをプログラムでキャッシュする](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
