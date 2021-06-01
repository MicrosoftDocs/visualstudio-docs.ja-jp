---
title: '方法: プログラムによって Visio 図面を開く'
description: Visual Studio を使用してプログラムによって Open または OpenEx メソッドを使用して Visio 図面を開く方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], opening Visio documents
- Visio [Office development in Visual Studio], opening Visio documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5f96efd41eb91551fe3cf7c03b55a44b7a9e1bf1
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824745"
---
# <a name="how-to-programmatically-open-visio-documents"></a>方法: プログラムによって Visio 図面を開く
  既存の Microsoft Office Visio 図面を開くには、Open と OpenEx の 2 つのメソッドがあります。 OpenEx メソッドは、呼び出し元が図面を開く方法を指定できる引数を提供する点を除いて、Open メソッドと同じです。

 オブジェクト モデルの詳細については、 [Microsoft.Office.Interop.Visio.Documents.Open](/office/vba/api/Visio.Documents.Open) メソッドと [Microsoft.Office.Interop.Visio.Documents.OpenEx](/office/vba/api/Visio.Documents.OpenEx) メソッドの VBA リファレンス ドキュメントを参照してください。

## <a name="open-a-visio-document"></a>Visio 図面を開く

### <a name="to-open-a-visio-document"></a>Visio 図面を開くには

- `Microsoft.Office.Interop.Visio.Documents.Open` メソッドを呼び出し、Visio 図面の完全修飾パスを指定します。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet5":::

## <a name="open-a-visio-document-with-specified-arguments"></a>引数を指定して Visio 図面を開く

### <a name="to-open-a-visio-document-as-read-only-and-docked"></a>読み取り専用およびドッキングとして Visio 図面を開くには

- `Microsoft.Office.Interop.Visio.Documents.OpenEx` メソッドを呼び出して、Visio 図面の完全修飾パスを指定し、必要な引数を指定します。この例では、ドッキングと読み取り専用の引数を指定しています。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb" id="Snippet6":::

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例で必要な要素は次のとおりです。

- `myDrawing.vsd` という名前の Visio 図面が、"*マイ ドキュメント*" フォルダー (Windows XP 以前の場合) または "*ドキュメント*" フォルダー (Windows Vista の場合) の `Test` という名前のディレクトリに配置されている必要があります。

## <a name="see-also"></a>関連項目
- [Visio ソリューション](../vsto/visio-solutions.md)
- [Visio オブジェクト モデルの概要](../vsto/visio-object-model-overview.md)
- [方法: プログラムによって新しい Visio 図面を作成する](../vsto/how-to-programmatically-create-new-visio-documents.md)
- [方法: プログラムによって Visio 図面を閉じる](../vsto/how-to-programmatically-close-visio-documents.md)
- [方法: プログラムによって Visio 図面を保存する](../vsto/how-to-programmatically-save-visio-documents.md)
- [方法: プログラムによって Visio 図面を印刷する](../vsto/how-to-programmatically-print-visio-documents.md)
