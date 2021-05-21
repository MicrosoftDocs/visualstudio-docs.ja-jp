---
title: '方法: プログラムによって文書でスペル チェックを行う'
description: CheckSpelling メソッドを使用して、プログラムによって文書内のスペル チェックを行う方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], checking spelling
- spelling checker, documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 8d7e04c542f91b9d7675eb81e7a3178e3427c52a
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828853"
---
# <a name="how-to-programmatically-check-spelling-in-documents"></a>方法: プログラムによって文書でスペル チェックを行う
  文書内のスペル チェックを行うには、<xref:Microsoft.Office.Interop.Word._Application.CheckSpelling%2A> メソッドを使用します。 このメソッドは、指定したパラメーターのスペルが正しいかどうかを示すブール値を返します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-check-spelling-and-display-results-in-a-message-box"></a>スペル チェックを実行し、メッセージ ボックスに結果を表示するには

1. <xref:Microsoft.Office.Interop.Word._Application.CheckSpelling%2A> メソッドを呼び出し、テキストの範囲を渡してスペルミスがないかどうかを確認します。 このコード例を使用するには、プロジェクトの `ThisDocument` クラスまたは `ThisAddIn` クラスからコードを実行します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet113":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet113":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書に複数の範囲を定義して選択する](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
