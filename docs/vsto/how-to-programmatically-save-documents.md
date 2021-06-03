---
title: '方法: プログラムによって文書を保存する'
description: Visual Studio を使用して、文書の名前を変更せずに、または新しい名前を付けて、プログラムによって文書を保存する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], saving
- Word [Office development in Visual Studio], saving documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 97f56ce0bd44eac71430a099b4fda9a7eddc7958
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107829009"
---
# <a name="how-to-programmatically-save-documents"></a>方法: プログラムによって文書を保存する

Microsoft Office Word 文書を保存するには、いくつかの方法があります。 文書の名前を変更せずに文書を保存することも、新しい名前を付けて文書を保存することもできます。

[!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="save-a-document-without-changing-the-name"></a>名前を変更せずに文書を保存する

### <a name="to-save-the-document-associated-with-a-document-level-customization"></a>文書レベルのカスタマイズに関連付けられている文書を保存するには

1. <xref:Microsoft.Office.Tools.Word.Document.Save%2A> クラスの <xref:Microsoft.Office.Tools.Word.Document> メソッドを呼び出します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet7":::

### <a name="to-save-the-active-document"></a>アクティブ文書を保存するには

1. 作業中の文書で <xref:Microsoft.Office.Interop.Word._Document.Save%2A> メソッドを呼び出します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet8":::
    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet8":::

   保存する文書が作業中の文書であるかどうかわからない場合は、これを名前で参照できます。

### <a name="to-save-a-document-specified-by-name"></a>名前で指定した文書を保存するには

1. <xref:Microsoft.Office.Interop.Word.Documents> コレクションの引数として文書名を使用します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet9":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet9":::

## <a name="save-a-document-with-a-new-name"></a>新しい名前を付けて文書を保存する

新しい名前を付けて文書を保存するには、`SaveAs` メソッドを使用します。 このメソッドは、文書レベルの Word プロジェクトで <xref:Microsoft.Office.Tools.Word.Document> ホスト項目のものを使用することも、任意の Word 文書でネイティブ <xref:Microsoft.Office.Interop.Word.Document> オブジェクトのものを使用することもできます。 このメソッドでは、新しいファイル名を指定する必要がありますが、他の引数は省略可能です。

> [!NOTE]
> `ThisDocument` の <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeSave> イベント ハンドラー内に **[名前を付けて保存]** ダイアログ ボックスを表示して、*Cancel* パラメーターを **false** に設定すると、アプリケーションが予期せず終了する可能性があります。 *Cancel* パラメーターを **true** に設定すると、自動保存が無効になっていることを示すエラー メッセージが表示されます。

### <a name="to-save-the-document-associated-with-a-document-level-customization-with-a-new-name"></a>新しい名前を付けて文書レベルのカスタマイズに関連付けられている文書を保存するには

1. 完全修飾パスとファイル名を使用して、プロジェクトの `ThisDocument` クラスの `SaveAs` メソッドを呼び出します。 指定した名前のファイルが既に対象のフォルダー内に存在する場合、そのファイルは警告なしで上書きされます。 このコード例を使用するには、 `ThisDocument` クラスからコードを実行します。

    > [!NOTE]
    > ターゲット ディレクトリが存在しない場合、またはファイルの保存に関する他の問題がある場合、`SaveAs` メソッドによって例外がスローされます。 `SaveAs` メソッドの周囲または呼び出し元メソッド内の `try...catch` ブロックを使用することをお勧めします。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet10":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet10":::

### <a name="to-save-a-native-document-with-a-new-name"></a>新しい名前を付けて文書を保存するには

1. 完全修飾パスとファイル名を使用して、保存する <xref:Microsoft.Office.Interop.Word.Document> の <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> メソッドを呼び出します。 指定した名前のファイルが既に対象のフォルダー内に存在する場合、そのファイルは警告なしで上書きされます。

     次のコード例では、新しい名前を付けて作業中の文書を保存します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

    > [!NOTE]
    > ターゲット ディレクトリが存在しない場合、またはファイルの保存に関する他の問題がある場合、<xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> メソッドによって例外がスローされます。 <xref:Microsoft.Office.Interop.Word._Document.SaveAs%2A> メソッドの周囲または呼び出し元メソッド内の **try...catch** ブロックを使用することをお勧めします。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet10":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet10":::

## <a name="compile-the-code"></a>コードのコンパイル

このコード例で必要な要素は次のとおりです。

- 文書を名前で保存するには、*NewDocument.doc* という名前の文書が、C ドライブの *Test* という名前のディレクトリに存在している必要があります。

- 新しい名前を付けて文書を保存するには、*Test* という名前のディレクトリが C ドライブに存在している必要があります。

## <a name="see-also"></a>関連項目

- [方法: プログラムによって文書を閉じる](../vsto/how-to-programmatically-close-documents.md)
- [方法: プログラムによって既存文書を開く](../vsto/how-to-programmatically-open-existing-documents.md)
- [Document ホスト項目](../vsto/document-host-item.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
