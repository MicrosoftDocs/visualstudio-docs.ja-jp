---
title: '方法: プログラムによって Word の組み込みダイアログ ボックスを使用する'
description: Visual Studio を使って、Microsoft Word の組み込みダイアログ ボックスをプログラムによって使用する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], dialog boxes
- dialog boxes, Word
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 6038000dec20f9183f974ad8d187230e634d5eed
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826214"
---
# <a name="how-to-programmatically-use-built-in-dialog-boxes-in-word"></a>方法: プログラムによって Word の組み込みダイアログ ボックスを使用する
  Microsoft Office Word の作業中に、ユーザー入力用のダイアログ ボックスを表示しなければならない場合があります。 独自のものを作成することもできますが、Word の組み込みダイアログ ボックスを使用する方法もあります。これらは、<xref:Microsoft.Office.Interop.Word.Application> オブジェクトの <xref:Microsoft.Office.Interop.Word.Dialogs> コレクションで公開されます。 これにより、200 を超える組み込みダイアログ ボックスにアクセスできます。これらは列挙として表されます。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="display-dialog-boxes"></a>ダイアログ ボックスを表示する
 ダイアログ ボックスを表示するには、<xref:Microsoft.Office.Interop.Word.WdWordDialog> 列挙のいずれかの値を使用して、表示するダイアログ ボックスを表す <xref:Microsoft.Office.Interop.Word.Dialog> オブジェクトを作成します。 その後、<xref:Microsoft.Office.Interop.Word.Dialog> オブジェクトの <xref:Microsoft.Office.Interop.Word.Dialog.Show%2A> メソッドを呼び出します。

 次のコード例では、 **[ファイルを開く]** ダイアログ ボックスを表示する方法を示します。 このコード例を使用するには、プロジェクトの `ThisDocument` または `ThisAddIn` クラスからコードを実行します。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet100":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet100":::

### <a name="access-dialog-box-members-that-are-available-through-late-binding"></a>遅延バインディングによって使用できるダイアログ ボックスのメンバーにアクセスする
 Word のダイアログ ボックスのプロパティとメソッドの一部は、遅延バインディングを通じてのみ使用できます。 **Option Strict** がオンになっている Visual Basic プロジェクトでは、これらのメンバーにアクセスするために、リフレクションを使用する必要があります。 詳細については、「[Office ソリューションの遅延バインディング](../vsto/late-binding-in-office-solutions.md)」を参照してください。

 次のコード例では、**Option Strict** がオフになっている Visual Basic プロジェクトで、あるいは [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] または [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] を対象とする Visual C# プロジェクトで、 **[ファイルを開く]** ダイアログ ボックスの **Name** プロパティを使用する方法を示します。 このコード例を使用するには、プロジェクトの `ThisDocument` または `ThisAddIn` クラスからコードを実行します。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet122":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet122":::

 次のコード例では、**Option Strict** がオンになっている Visual Basic プロジェクトで、 **[ファイルを開く]** ダイアログ ボックスの **Name** プロパティに、リフレクションを使用してアクセスする方法を示しています。 このコード例を使用するには、プロジェクトの `ThisDocument` または `ThisAddIn` クラスからコードを実行します。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet102":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって Word のダイアログ ボックスを非表示モードで使用する](../vsto/how-to-programmatically-use-word-dialog-boxes-in-hidden-mode.md)
- [Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
- [Option Strict ステートメント](/dotnet/visual-basic/language-reference/statements/option-strict-statement)
- [リフレクション (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [リフレクション (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
