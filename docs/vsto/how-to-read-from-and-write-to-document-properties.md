---
title: '方法: ドキュメント プロパティの読み込みと書き込みを行う'
description: Visual Studio を使用して、Microsoft Excel および Microsoft Word でドキュメント プロパティを取得または設定する方法について学習します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], document properties
- documents [Office development in Visual Studio], properties
- document properties [Office development in Visual Studio]
- Excel [Office development in Visual Studio], document properties
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 3474d86a7408e841d383c82e5ab38da90253dbbf
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826682"
---
# <a name="how-to-read-from-and-write-to-document-properties"></a>方法: ドキュメント プロパティの読み込みと書き込みを行う
  ドキュメント プロパティをドキュメントと共に保存できます。 Office アプリケーションには、作成者、タイトル、件名など、多数の組み込みプロパティが用意されています。 このトピックでは、Microsoft Office Excel および Microsoft Office Word でドキュメント プロパティを設定する方法について説明します。

 [!INCLUDE[appliesto_docprops](../vsto/includes/appliesto-docprops-md.md)]

## <a name="set-document-properties-in-excel"></a>Excel でドキュメント プロパティを設定する
 Excel の組み込みプロパティを操作するには、次のプロパティを使用します。

- ドキュメント レベルのプロジェクトでは、 <xref:Microsoft.Office.Tools.Excel.Workbook.BuiltinDocumentProperties%2A> クラスの `ThisWorkbook` プロパティを使用します。

- VSTO アドイン プロジェクトでは、 <xref:Microsoft.Office.Interop.Excel._Workbook.BuiltinDocumentProperties%2A> オブジェクトの <xref:Microsoft.Office.Interop.Excel.Workbook> プロパティを使用します。

  これらのプロパティは、 <xref:Microsoft.Office.Core.DocumentProperties> オブジェクトのコレクションである <xref:Microsoft.Office.Core.DocumentProperty> オブジェクトを返します。 このコレクションの `Item` プロパティを使用すると、名前またはコレクション内のインデックスに基づいて特定のプロパティを取得できます。

  次のコード例は、ドキュメント レベルのプロジェクトで組み込みの **Revision Number** プロパティを変更する方法を示しています。

### <a name="to-change-the-revision-number-property-in-excel"></a>Excel の Revision Number プロパティを変更するには

1. 組み込みのドキュメント プロパティを変数に代入します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs" id="Snippet7":::

2. `Revision Number` プロパティの値を 1 つインクリメントします。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb" id="Snippet8":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs" id="Snippet8":::

## <a name="set-document-properties-in-word"></a>Word でドキュメント プロパティを設定する
 Word の組み込みプロパティを操作するには、次のプロパティを使用します。

- ドキュメント レベルのプロジェクトでは、 <xref:Microsoft.Office.Tools.Word.Document.BuiltInDocumentProperties%2A> クラスの `ThisDocument` プロパティを使用します。

- VSTO アドイン プロジェクトでは、 <xref:Microsoft.Office.Interop.Word._Document.BuiltInDocumentProperties%2A> オブジェクトの <xref:Microsoft.Office.Interop.Word.Document> プロパティを使用します。

  これらのプロパティは、 <xref:Microsoft.Office.Core.DocumentProperties> オブジェクトのコレクションである <xref:Microsoft.Office.Core.DocumentProperty> オブジェクトを返します。 このコレクションの `Item` プロパティを使用すると、名前またはコレクション内のインデックスに基づいて特定のプロパティを取得できます。

  次のコード例は、ドキュメント レベルのプロジェクトで組み込みの **Subject** プロパティを変更する方法を示しています。

### <a name="to-change-the-subject-property"></a>Subject プロパティを変更するには

1. 組み込みのドキュメント プロパティを変数に代入します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingWordCS/ThisDocument.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingWordVB/ThisDocument.vb" id="Snippet1":::

2. `Subject` プロパティを「Whitepaper」に変更します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingWordCS/ThisDocument.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingWordVB/ThisDocument.vb" id="Snippet2":::

## <a name="robust-programming"></a>信頼性の高いプログラミング
 これらの例では、Excel の場合はドキュメント レベルのプロジェクトの `ThisWorkbook` クラス、Word の場合はドキュメント レベルのプロジェクトの `ThisDocument` クラスにそれぞれコードを記述していることを前提としています。

 Word、Excel、およびそれらのオブジェクトを操作する場合でも、Microsoft Office では使用可能な組み込みドキュメント プロパティの一覧が提供されます。 未定義のプロパティにアクセスしようとすると、例外が発生します。

## <a name="see-also"></a>関連項目
- [プログラム VSTO アドイン](../vsto/programming-vsto-add-ins.md)
- [プログラム ドキュメント レベルのカスタマイズ](../vsto/programming-document-level-customizations.md)
- [方法: カスタム ドキュメント プロパティを作成および変更する](../vsto/how-to-create-and-modify-custom-document-properties.md)
