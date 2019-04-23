---
title: '方法: プログラムによって既存文書を開く'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], opening
- Word [Office development in Visual Studio], opening documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 490dda6e5357cd0933c6a8b494cc4373038e5c1c
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60062166"
---
# <a name="how-to-programmatically-open-existing-documents"></a>方法: プログラムによって既存文書を開く
  <xref:Microsoft.Office.Interop.Word.Documents.Open%2A>メソッドは、完全修飾パスとファイル名で指定された既存の Microsoft Office Word ドキュメントを開きます。 このメソッドが戻る、<xref:Microsoft.Office.Interop.Word.Document>開いているドキュメントを表します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-open-a-document"></a>ドキュメントを開く

- 呼び出す、<xref:Microsoft.Office.Interop.Word.Documents.Open%2A>のメソッド、<xref:Microsoft.Office.Interop.Word.Documents>コレクションをドキュメントへのパスを指定します。

     [!code-vb[Trin_VstcoreWordAutomation#5](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#5)]
     [!code-csharp[Trin_VstcoreWordAutomation#5](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#5)]

## <a name="to-open-a-document-as-read-only"></a>読み取り専用とドキュメントを開く

- 呼び出す、<xref:Microsoft.Office.Interop.Word.Documents.Open%2A>メソッドは、ドキュメントへのパスを指定し、設定、 *ReadOnly*引数**True**メソッドの呼び出しで。

     [!code-vb[Trin_VstcoreWordAutomation#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#6)]
     [!code-csharp[Trin_VstcoreWordAutomation#6](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#6)]

## <a name="compile-the-code"></a>コードのコンパイル
 このコード例で必要な要素は次のとおりです。

- という名前のドキュメント*NewDocument.doc*という名前のディレクトリに存在する必要があります*テスト*失われます。

## <a name="see-also"></a>関連項目
- [方法: プログラムで新しいドキュメントを作成します。](../vsto/how-to-programmatically-create-new-documents.md)
- [方法: プログラムによって文書を閉じる](../vsto/how-to-programmatically-close-documents.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
