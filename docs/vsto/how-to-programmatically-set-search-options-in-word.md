---
title: '方法: プログラムによって Word の検索オプションを設定する'
description: Visual Studio を使って、Microsoft Word で選択できる検索オプションをプログラムで設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- settings, Word search options
- documents [Office development in Visual Studio], search options
- Word, searching options
- searching, Word options
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 605f782bf6dc3bb56b52bdcd896d1c6419cf5f51
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825031"
---
# <a name="how-to-programmatically-set-search-options-in-word"></a>方法: プログラムによって Word の検索オプションを設定する
  Microsoft Office Word 文書で選択できる検索オプションを設定するには、次の 2 つの方法があります。

- <xref:Microsoft.Office.Interop.Word.Find> オブジェクトの個々のプロパティを設定する。

- <xref:Microsoft.Office.Interop.Word.Find> オブジェクトの <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> メソッドの引数を使用する。

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="use-properties-of-a-find-object"></a>Find オブジェクトのプロパティを使用する
 次のコードでは、現在の選択範囲内のテキストを検索するために、<xref:Microsoft.Office.Interop.Word.Find> オブジェクトのプロパティを設定しています。 前方検索、折り返し、検索テキストなどの検索条件は、<xref:Microsoft.Office.Interop.Word.Find> オブジェクトのプロパティであることに注意してください。

 C# コードを記述する場合、<xref:Microsoft.Office.Interop.Word.Find> オブジェクトの各プロパティを設定することは効率的ではありません。<xref:Microsoft.Office.Interop.Word.Find.Execute%2A> メソッドで、同じプロパティをパラメーターとして指定する必要があるためです。 そのため、この例には Visual Basic のコードのみを含めています。

### <a name="to-set-search-options-using-a-find-object"></a>Find オブジェクトを使用して検索オプションを設定するには

1. 選択範囲を前方に検索して **find me** というテキストを探すように、<xref:Microsoft.Office.Interop.Word.Find> オブジェクトのプロパティを設定します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet76":::

## <a name="use-execute-method-arguments"></a>Execute メソッドの引数を使用する
 次のコードでは、現在の選択範囲内のテキストを検索するために、<xref:Microsoft.Office.Interop.Word.Find> オブジェクトの <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> メソッドを使用しています。 前方検索、折り返し、検索テキストなどの検索条件は、<xref:Microsoft.Office.Interop.Word.Find.Execute%2A> メソッドのパラメーターとして渡されることに注意してください。

### <a name="to-set-search-options-using-execute-method-arguments"></a>Execute メソッドの引数を使用して検索オプションを設定するには

1. 検索条件を <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> メソッドのパラメーターとして渡して、**find me** というテキストが選択範囲で前方検索されるようにします。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet77":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet77":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書内のテキストを検索および置換する](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [方法: 文書で見つかった項目をプログラムによってループする](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [方法: プログラムによって検索後に選択範囲を復元する](../vsto/how-to-programmatically-restore-selections-after-searches.md)
