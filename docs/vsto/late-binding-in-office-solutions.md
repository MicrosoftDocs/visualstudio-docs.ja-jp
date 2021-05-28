---
title: Office ソリューションの遅延バインディング
description: Microsoft Office アプリケーション内のオブジェクト モデルの一部の型で、遅延バインディング機能を通じて使用できる機能が、どのように提供されるかについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- objects [Office development in Visual Studio], casting
- types [Office development in Visual Studio], casting
- automation [Office development in Visual Studio], casting objects
- casting, object to specific type
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e618dcd0cc699b4626f825890cf0fc8bd7ddd853
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107823887"
---
# <a name="late-binding-in-office-solutions"></a>Office ソリューションの遅延バインディング
  Microsoft Office アプリケーションのオブジェクト モデルの一部の型では、遅延バインディング機能を通じて使用できる機能が提供されます。 たとえば、一部のメソッドとプロパティでは、Office アプリケーションのコンテキストに応じて異なる型のオブジェクトが返されることがあり、型によっては、コンテキストによって異なるメソッドやプロパティを公開できます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 **Option Strict** がオフになっている Visual Basic プロジェクトと、[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] または [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] を対象とした Visual C# プロジェクトでは、これらの遅延バインディング機能を使用する型を直接操作することができます。

## <a name="implicit-and-explicit-casting-of-object-return-values"></a>オブジェクトの戻り値の暗黙的および明示的なキャスト
 Microsoft Office プライマリ相互運用機能アセンブリ (PIA) の多くのメソッドとプロパティでは、複数の異なる型のオブジェクトを返すことができるため、<xref:System.Object> 値が返されます。 たとえば、<xref:Microsoft.Office.Tools.Excel.Workbook.ActiveSheet%2A> プロパティは <xref:System.Object> を返します。これは、どのシートがアクティブかによって、戻り値が <xref:Microsoft.Office.Interop.Excel.Worksheet> または <xref:Microsoft.Office.Interop.Excel.Chart> オブジェクトになる可能性があるためです。

 メソッドまたはプロパティが <xref:System.Object> を返す場合は、(Visual Basic で) オブジェクトを明示的に変換して、**Option Strict** がオンになっている Visual Basic プロジェクトでの適切な型にする必要があります。 **Option Strict** がオフになっている Visual Basic プロジェクトでは、<xref:System.Object> 戻り値を明示的にキャストする必要はありません。

 ほとんどの場合、<xref:System.Object> を返すメンバーの戻り値の型は、参照ドキュメントに一覧表示されています。 オブジェクトを変換またはキャストすると、コード エディターでオブジェクトの IntelliSense が有効になります。

 Visual Basic での変換について詳しくは、「[暗黙の型変換と明示的な型変換 &#40;Visual Basic&#41;](/dotnet/visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions)」および「[CType 関数 &#40;Visual Basic&#41;](/dotnet/visual-basic/language-reference/functions/ctype-function)」をご覧ください。

### <a name="examples"></a>例
 次のコード例は、**Option Strict** がオンになっている Visual Basic プロジェクトで、オブジェクトを特定の型にキャストする方法を示したものです。 このタイプのプロジェクトでは、<xref:Microsoft.Office.Tools.Excel.WorksheetBase.Cells%2A> プロパティを明示的に <xref:Microsoft.Office.Interop.Excel.Range> にキャストする必要があります。 この例では、`Sheet1` というワークシート クラスを含んだ、ドキュメント レベルのプロジェクトが必要です。

  :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb" id="Snippet9":::

 次のコード例は、**Option Strict** がオフになっている Visual Basic か、[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] を対象とした Visual C# プロジェクトで、オブジェクトを特定の型に暗黙的にキャストする方法を示したものです。 これらのタイプのプロジェクトでは、<xref:Microsoft.Office.Tools.Excel.WorksheetBase.Cells%2A> プロパティは暗黙的に <xref:Microsoft.Office.Interop.Excel.Range> にキャストされます。 この例では、`Sheet1` というワークシート クラスを含んだ、ドキュメント レベルのプロジェクトが必要です。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb" id="Snippet10":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/Sheet1.cs" id="Snippet10":::

## <a name="access-members-that-are-available-only-through-late-binding"></a>遅延バインディングを通じてのみ使用できるメンバーにアクセスする
 Office PIA の一部のプロパティとメソッドは、遅延バインディングを通じてのみ使用できます。 **Option Strict** がオフになっているか Visual Basic プロジェクトや、[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] または [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] を対象とした Visual C# プロジェクトでは、それらの言語の遅延バインディング機能を使って、遅延バインドされたメンバーにアクセスできます。 **Option Strict** がオンになっている Visual Basic プロジェクトでは、これらのメンバーにアクセスするために、リフレクションを使用する必要があります。

### <a name="examples"></a>例
 次のコード例は、**Option Strict** がオフになっている Visual Basic か、[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] を対象とした Visual C# プロジェクトで、遅延バインドされたメンバーにアクセスする方法を示したものです。 この例では、Word の **[ファイルを開く]** ダイアログ ボックスの、遅延バインドされた **Name** プロパティにアクセスします。 この例を使用するには、Word プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet122":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet122":::

 次のコード例は、**Option Strict** がオンになっている Visual Basic プロジェクトで、リフレクションを使って同じタスクを実行する方法を示したものです。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet102":::

## <a name="see-also"></a>こちらもご覧ください
- [Office ソリューションでコードを書く](../vsto/writing-code-in-office-solutions.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
- [dynamic 型の使用 &#40;C&#35; プログラミング ガイド&#41;](/dotnet/csharp/programming-guide/types/using-type-dynamic)
- [Option Strict ステートメント](/dotnet/visual-basic/language-reference/statements/option-strict-statement)
- [リフレクション (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [リフレクション (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
