---
title: '方法: プログラムによって Word のダイアログ ボックスを非表示モードで使用する'
description: Visual Studio を使って、Microsoft Word のダイアログ ボックスをプログラムによって非表示モードで使用する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- hidden dialog boxes
- Word [Office development in Visual Studio], dialog boxes
- dialog boxes, hidden mode in Word
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 39a81ccec284541d93d3a5901211d8a46ea6b61a
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826188"
---
# <a name="how-to-programmatically-use-word-dialog-boxes-in-hidden-mode"></a>方法: プログラムによって Word のダイアログ ボックスを非表示モードで使用する
  Microsoft Office Word の組み込みダイアログ ボックスをユーザーに表示せずに呼び出すことで、複雑な操作を 1 つのメソッド呼び出しで実行することができます。 これを行うには、<xref:Microsoft.Office.Interop.Word.Dialog.Display%2A> メソッドを呼び出さずに、<xref:Microsoft.Office.Interop.Word.Dialog> オブジェクトの <xref:Microsoft.Office.Interop.Word.Dialog.Execute%2A> メソッドを使用します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="examples"></a>例
 次のコード例では、 **[ページ設定]** ダイアログ ボックスを非表示モードで使用して、複数のページ設定プロパティをユーザー入力なしで設定する方法を示しています。 この例では、<xref:Microsoft.Office.Interop.Word.Dialog> オブジェクトを使ってカスタム ページ サイズを構成します。 ページ設定の特定の設定 (上余白、下余白など) は、<xref:Microsoft.Office.Interop.Word.Dialog> オブジェクトの遅延バインディング プロパティとして使用できます。 これらのプロパティは、実行時に Word によって動的に作成されます。

 次の例は、**Option Strict** がオフになっている Visual Basic プロジェクトと、[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] を対象とした Visual C# プロジェクトで、このタスクを実行する方法を示したものです。 これらのプロジェクトでは、Visual Basic および Visual C# のコンパイラで、遅延バインディング機能を使用できます。 このコード例を使用するには、プロジェクトの `ThisDocument` または `ThisAddIn` クラスからコードを実行します。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet123":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet123":::

 次の例は、**Option Strict** がオンになっている Visual Basic プロジェクトでこのタスクを実行する方法を示したものです。 これらのプロジェクトでは、遅延バインディング プロパティにアクセスするためにリフレクションを使用する必要があります。 このコード例を使用するには、プロジェクトの `ThisDocument` または `ThisAddIn` クラスからコードを実行します。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet104":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって Word の組み込みダイアログ ボックスを使用する](../vsto/how-to-programmatically-use-built-in-dialog-boxes-in-word.md)
- [Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)
- [Office ソリューションの遅延バインディング](../vsto/late-binding-in-office-solutions.md)
- [リフレクション (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [リフレクション (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
