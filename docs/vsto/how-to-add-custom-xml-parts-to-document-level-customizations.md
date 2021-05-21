---
title: '方法: ドキュメント レベルのカスタマイズにカスタム XML 部分を追加する'
description: ドキュメント レベルのカスタマイズにカスタム XML 部分を作成して、Microsoft Office Excel ブックまたは Microsoft Office Word 文書に XML データを格納する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- document-level customizations [Office development in Visual Studio], custom XML parts
- Office documents [Office development in Visual Studio, custom XML parts
- Word [Office development in Visual Studio], custom XML parts
- Excel [Office development in Visual Studio], custom XML parts
- custom XML parts [Office development in Visual Studio], adding
- documents [Office development in Visual Studio], custom XML parts
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 99374a2daded3c4b49b60053a69cd1ff7c4dffe8
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827689"
---
# <a name="how-to-add-custom-xml-parts-to-document-level-customizations"></a>方法: ドキュメント レベルのカスタマイズにカスタム XML 部分を追加する
  ドキュメント レベルのカスタマイズにカスタム XML 部分を作成すると、Microsoft Office Excel ブックまたは Microsoft Office Word 文書に XML データを格納できます。 詳細については、「[カスタム XML 部分の概要](../vsto/custom-xml-parts-overview.md)」を参照してください。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

> [!NOTE]
> Visual Studio では、Microsoft Office PowerPoint のドキュメント レベルのプロジェクトは提供していません。 VSTO アドインを使用してカスタム XML 部分を PowerPoint プレゼンテーションに追加する方法については、「[方法: VSTO アドインを使用してドキュメントにカスタム XML 部分を追加する](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)」を参照してください。

### <a name="to-add-a-custom-xml-part-to-an-excel-workbook"></a>カスタム XML 部分を Excel ブックに追加するには

1. ブックの <xref:Microsoft.Office.Core.CustomXMLPart> コレクションに、新しい <xref:Microsoft.Office.Core.CustomXMLParts> オブジェクトを追加します。 <xref:Microsoft.Office.Core.CustomXMLPart> にはブックに格納する XML 文字列が含まれています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartExcelDocLevel/ThisWorkbook.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartExcelDocLevel/ThisWorkbook.vb" id="Snippet1":::

2. Excel のドキュメント レベルのプロジェクト内の `AddCustomXmlPartToWorkbook` クラスに `ThisWorkbook` メソッドを追加します。

3. プロジェクトの他のコードからメソッドを呼び出します。 たとえば、ユーザーがブックを開いたときにカスタム XML 部分を作成するには、このメソッドを `ThisWorkbook_Startup` イベント ハンドラーから呼び出します。

### <a name="to-add-a-custom-xml-part-to-a-word-document"></a>カスタム XML 部分を Word ドキュメントに追加するには

1. ドキュメントの <xref:Microsoft.Office.Core.CustomXMLPart> コレクションに、新しい <xref:Microsoft.Office.Core.CustomXMLParts> オブジェクトを追加します。 <xref:Microsoft.Office.Core.CustomXMLPart> にはドキュメントに格納する XML 文字列が含まれています。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartWordDocLevel/ThisDocument.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartWordDocLevel/ThisDocument.cs" id="Snippet1":::

2. Word のドキュメント レベルのプロジェクト内の `AddCustomXmlPartToDocument` クラスに `ThisDocument` メソッドを追加します。

3. プロジェクトの他のコードからメソッドを呼び出します。 たとえば、ユーザーが文書を開いたときにカスタム XML 部分を作成するには、このメソッドを `ThisDocument_Startup` イベント ハンドラーから呼び出します。

## <a name="robust-programming"></a>信頼性の高いプログラミング
 わかりやすくするために、この例では、メソッドでローカル変数として定義されている XML 文字列を使用しています。 通常は、ファイルやデータベースなどの外部ソースから XML を取得する必要があります。

## <a name="see-also"></a>関連項目
- [カスタム XML 部分の概要](../vsto/custom-xml-parts-overview.md)
- [方法: VSTO アドインを使用してドキュメントにカスタム XML 部分を追加する](../vsto/how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins.md)
