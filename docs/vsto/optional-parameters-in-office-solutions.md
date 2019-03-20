---
title: Office ソリューションの省略可能なパラメーター
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d6baf0c32d087ea804bb8e221745337c73b64114
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56639269"
---
# <a name="optional-parameters-in-office-solutions"></a>Office ソリューションの省略可能なパラメーター
  Microsoft Office アプリケーションのオブジェクト モデルに含まれるメソッドの多くは、省略可能なパラメーターを受け取ります。 Visual Studio で Visual Basic を使用して Office ソリューションを開発する場合は、省略可能なパラメーターに値を渡す必要はありません。省略したパラメーターに対しては自動的に既定値が使用されます。 ほとんどの場合、Visual C# プロジェクトで省略可能なパラメーターを省略することもできます。 オプションを省略できませんただし、 **ref**のパラメーター、`ThisDocument`ドキュメント レベルの Word プロジェクトでクラス。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Visual c# および Visual Basic プロジェクトで省略可能なパラメーターの使用方法の詳細については、次を参照してください[名前付き引数と省略可能な引数&#40;C&#35;プログラミング ガイド&#41;](/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments)と[&#40;Visual Basic&#41;](/dotnet/visual-basic/programming-guide/language-features/procedures/optional-parameters)します。

> [!NOTE]
>  旧バージョンの Visual Studio では、Visual C# プロジェクトのすべての省略可能なパラメーターに値を渡す必要があります。 便宜上、これらのプロジェクトには `missing` というグローバル変数が含まれています。パラメーターの既定値を使用する場合に、このグローバル変数を省略可能なパラメーターに渡すことができます。 Visual Studio での Office の visual c# プロジェクトがまだが含まれて、`missing`変数が通常必要はありませんでの Office ソリューションを開発するときに使用する[!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)]、オプションのメソッドを呼び出す場合を除く**ref**内のパラメーター、 `ThisDocument` Word のドキュメント レベル プロジェクト内のクラス。

## <a name="example-in-excel"></a>Excel の例
 <xref:Microsoft.Office.Tools.Excel.Worksheet.CheckSpelling%2A> メソッドには、多くの省略可能なパラメーターがあります。 次のコード例に示すように、一部のパラメーターの値を指定し、他のパラメーターには既定値を使用することができます。 この例では、`Sheet1` というワークシート クラスを持つドキュメント レベルのプロジェクトが必要です。

 [!code-csharp[Trin_VstrefGeneralExcel#1](../vsto/codesnippet/CSharp/excelworkbook1/Sheet1.cs#1)]
 [!code-vb[Trin_VstrefGeneralExcel#1](../vsto/codesnippet/VisualBasic/excelworkbook1/Sheet1.vb#1)]

## <a name="example-in-word"></a>Word の例
 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> メソッドには、多くの省略可能なパラメーターがあります。 次のコード例に示すように、一部のパラメーターの値を指定し、他のパラメーターには既定値を使用することができます。

 [!code-vb[Trin_VstrefGeneralWord#1](../vsto/codesnippet/VisualBasic/worddocument1/ThisDocument.vb#1)]
 [!code-csharp[Trin_VstrefGeneralWord#1](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#1)]

## <a name="use-optional-parameters-of-methods-in-the-thisdocument-class-in-visual-c-document-level-projects-for-word"></a>Word 用の Visual C# ドキュメント レベルのプロジェクトの ThisDocument クラスでメソッドの省略可能なパラメーターを使用してください。
 Word オブジェクト モデルには、多くのメソッドでオプションが含まれています。 **ref**パラメーターを受け入れる<xref:System.Object>値。 オプションを省略できませんただし、 **ref** 、生成されたメソッドのパラメーターを`ThisDocument`Word 用の Visual C# ドキュメント レベル プロジェクト内のクラス。 Visual C# を使用する省略可能な省略**ref**のみインターフェイスのメソッドのパラメーターがないクラスします。 たとえば、次のコード例はコンパイルされず、コンパイル オプションを省略することはできませんので**ref**のパラメーター、<xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A>のメソッド、`ThisDocument`クラス。

 [!code-csharp[Trin_VstrefGeneralWord#3](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#3)]

 `ThisDocument` クラスのメソッドを呼び出す場合は、次のガイドラインに従います。

- オプションの既定値を受け入れるように**ref**パラメーターでは、パス、`missing`パラメーターに変数。 `missing` 変数は Visual C# Office プロジェクトで自動的に定義され、生成されたプロジェクト コード内で <xref:System.Type.Missing> 値に割り当てられます。

- 省略可能な独自の値を指定する**ref**パラメーターを指定する値に割り当てられているオブジェクトを宣言し、パラメーターに、オブジェクトを渡します。

  次のコード例を呼び出す方法を示します、<xref:Microsoft.Office.Tools.Word.DocumentBase.CheckSpelling%2A>メソッドの値を指定することによって、 *ignoreUppercase*パラメーターとその他のパラメーターの既定値を受け入れることです。

  [!code-csharp[Trin_VstrefGeneralWord#4](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#4)]

  省略可能な指定を省略するコードを記述する場合**ref**内のメソッドのパラメーター、`ThisDocument`クラス、または上で呼び出せる同じメソッド、<xref:Microsoft.Office.Interop.Word.Document>によって返されるオブジェクト、<xref:Microsoft.Office.Tools.Word.Document.InnerObject%2A>プロパティを省略して、そのメソッドからのパラメーター。 これは、<xref:Microsoft.Office.Interop.Word.Document> がクラスではなくインターフェイスであるためです。

  [!code-csharp[Trin_VstrefGeneralWord#5](../vsto/codesnippet/CSharp/worddocument1/ThisDocument.cs#5)]

  値と参照型パラメーターの詳細については、次を参照してください[値と参照渡しの引数を渡す&#40;Visual Basic&#41; ](/dotnet/visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference) (Visual Basic) 用と[パラメーターを渡す&#40;C&#35; 。プログラミング ガイド&#41;](/dotnet/csharp/programming-guide/classes-and-structs/passing-parameters)します。

## <a name="see-also"></a>関連項目
- [Office ソリューションの開発](../vsto/developing-office-solutions.md)
- [Office ソリューションにおけるコードの記述](../vsto/writing-code-in-office-solutions.md)
