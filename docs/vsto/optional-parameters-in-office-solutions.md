---
title: Office ソリューションの省略可能なパラメーター
description: 省略したパラメーターに対しては自動的に既定値が使用されるため、省略可能なパラメーターには値を渡す必要がないことについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], optional parameters
- Visual C# [Office development in Visual Studio], optional parameters
- Visual Basic [Office development in Visual Studio], optional parameters
- application development [Office development in Visual Studio], optional parameters
- missing field [Office development in Visual Studio]
- optional parameters [Office development in Visual Studio]
- parameters [Office development in Visual Studio], optional
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9c95842ac2c6d77a2312ac5c4c197ba22ed2020e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825421"
---
# <a name="optional-parameters-in-office-solutions"></a>Office ソリューションの省略可能なパラメーター
  Microsoft Office アプリケーションのオブジェクト モデルに含まれるメソッドの多くは、省略可能なパラメーターを受け取ります。 Visual Studio で Visual Basic を使用して Office ソリューションを開発する場合は、省略可能なパラメーターに値を渡す必要はありません。省略したパラメーターに対しては自動的に既定値が使用されます。 ほとんどの場合は、Visual C# プロジェクトでも省略可能なパラメーターを省略できます。 ただし、ドキュメント レベルの Word プロジェクトでは、`ThisDocument` クラスの省略可能な **ref** パラメーターを省略できません。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Visual C# および Visual Basic プロジェクトで省略可能なパラメーターを使用する詳細については、「[名前付き引数と省略可能な引数 &#40;C&#35; プログラミング ガイド&#41;](/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments)」および「[省略可能なパラメーター &#40;Visual Basic&#41;](/dotnet/visual-basic/programming-guide/language-features/procedures/optional-parameters)」を参照してください。

> [!NOTE]
> 旧バージョンの Visual Studio では、Visual C# プロジェクトのすべての省略可能なパラメーターに値を渡す必要があります。 便宜上、これらのプロジェクトには `missing` というグローバル変数が含まれています。パラメーターの既定値を使用する場合に、このグローバル変数を省略可能なパラメーターに渡すことができます。 Visual Studio の Office の Visual C# プロジェクトにも `missing` 変数が含まれていますが、通常、[!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] で Office ソリューションを開発する場合は、この変数を使用する必要はありません。ただし、ドキュメント レベルの Word プロジェクトで、省略可能な **ref** パラメーターを持つ `ThisDocument` クラスのメソッドを呼び出す場合は例外です。

## <a name="example-in-excel"></a>Excel の例
 <xref:Microsoft.Office.Tools.Excel.Worksheet.CheckSpelling%2A> メソッドには、多くの省略可能なパラメーターがあります。 次のコード例に示すように、一部のパラメーターの値を指定し、他のパラメーターには既定値を使用することができます。 この例では、`Sheet1` というワークシート クラスを持つドキュメント レベルのプロジェクトが必要です。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/excelworkbook1/Sheet1.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/excelworkbook1/Sheet1.vb" id="Snippet1":::

## <a name="example-in-word"></a>Word の例
 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> メソッドには、多くの省略可能なパラメーターがあります。 次のコード例に示すように、一部のパラメーターの値を指定し、他のパラメーターには既定値を使用することができます。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/worddocument1/ThisDocument.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs" id="Snippet1":::

## <a name="use-optional-parameters-of-methods-in-the-thisdocument-class-in-visual-c-document-level-projects-for-word"></a>Word 用の Visual C# ドキュメント レベル プロジェクトで ThisDocument クラスのメソッドの省略可能なパラメーターを使用する
 Word オブジェクト モデルには、<xref:System.Object> 値を受け入れる省略可能な **ref** パラメーターを持つメソッドが多数あります。 しかし、Word 用の Visual C# ドキュメント レベル プロジェクトでは、生成された `ThisDocument` クラスのメソッドの省略可能な **ref** パラメーターを省略できません。 Visual C# では、クラスではなくインターフェイスのメソッドについてのみ、省略可能な **ref** パラメーターを省略できます。 たとえば、次のコード例はコンパイルされません。これは、`ThisDocument` クラスの <xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A> メソッドの省略可能な **ref** パラメーターを省略できないためです。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs" id="Snippet3":::

 `ThisDocument` クラスのメソッドを呼び出す場合は、次のガイドラインに従います。

- 省略可能な **ref** パラメーターの既定値を使用するには、パラメーターに `missing` 変数を渡します。 `missing` 変数は Visual C# Office プロジェクトで自動的に定義され、生成されたプロジェクト コード内で <xref:System.Type.Missing> 値に割り当てられます。

- 省略可能な **ref** パラメーターに独自の値を指定するには、指定する値に割り当てられるオブジェクトを宣言し、オブジェクトをパラメーターに渡します。

  次のコード例は、*ignoreUppercase* パラメーターの値を指定し、他のパラメーターの既定値を受け入れることで <xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A> メソッドを呼び出す方法を示しています。

  :::code language="csharp" source="../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs" id="Snippet4":::

  `ThisDocument` クラスのメソッドの省略可能な **ref** パラメーターを省略するコードを記述するには、別の方法として、<xref:Microsoft.Office.Tools.Word.Document.InnerObject%2A> プロパティから返される <xref:Microsoft.Office.Interop.Word.Document> オブジェクトの同じメソッドを呼び出し、そのメソッドのパラメーターを省略することができます。 これは、<xref:Microsoft.Office.Interop.Word.Document> がクラスではなくインターフェイスであるためです。

  :::code language="csharp" source="../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs" id="Snippet5":::

  値型と参照型のパラメーターの詳細については、「[引数の値渡しと参照渡し &#40;Visual Basic&#41;](/dotnet/visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference)」 (Visual Basic の場合) および「[パラメーターの引き渡し &#40;C&#35; プログラミング ガイド&#41;](/dotnet/csharp/programming-guide/classes-and-structs/passing-parameters)」を参照してください。

## <a name="see-also"></a>関連項目
- [Office ソリューションを開発する](../vsto/developing-office-solutions.md)
- [Office ソリューションでコードを書く](../vsto/writing-code-in-office-solutions.md)
