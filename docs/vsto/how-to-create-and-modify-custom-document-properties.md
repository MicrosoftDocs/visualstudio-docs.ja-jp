---
title: '方法: 作成し、カスタム ドキュメント プロパティの変更'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom document properties
- documents [Office development in Visual Studio], properties
- document properties [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: 71ff5c37eee21092e186e50547cf9c0b72f1b20e
ms.sourcegitcommit: a205ff1b389fba1803acd32c54df7feb0ef7a203
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2018
ms.locfileid: "53646510"
---
# <a name="how-to-create-and-modify-custom-document-properties"></a>方法: 作成し、カスタム ドキュメント プロパティの変更
  上記の Microsoft Office アプリケーションは、ドキュメントで保存される組み込みのプロパティを提供します。 さらに、ドキュメントで保存する追加情報がある場合は、カスタム ドキュメント プロパティを作成し、変更することができます。  
  
 [!INCLUDE[appliesto_docprops](../vsto/includes/appliesto-docprops-md.md)]  
  
 カスタム プロパティを操作するには、ドキュメントの CustomDocumentProperties プロパティを使用します。 たとえば、Microsoft Office Excel のドキュメント レベルのプロジェクトでは、 <xref:Microsoft.Office.Tools.Excel.Workbook.CustomDocumentProperties%2A> クラスの `ThisWorkbook` プロパティを使用します。 Excel の VSTO アドイン プロジェクトでは、 <xref:Microsoft.Office.Interop.Excel._Workbook.CustomDocumentProperties%2A> オブジェクトの <xref:Microsoft.Office.Interop.Excel.Workbook> プロパティを使用します。 これらのプロパティは、 <xref:Microsoft.Office.Core.DocumentProperties> オブジェクトのコレクションである <xref:Microsoft.Office.Core.DocumentProperty> オブジェクトを返します。 このコレクションの `Item` プロパティを使用すると、名前またはコレクション内のインデックスに基づいて特定のプロパティを取得できます。  
  
 次の例は、Excel のドキュメント レベルのカスタマイズでカスタム プロパティを追加し、値を割り当てる方法を示します。  
  
 ![ビデオへのリンク](../vsto/media/playvideo.gif "ビデオへのリンク")関連するビデオ デモについては、次を参照してください[How do i:アクセスし、Microsoft Word のカスタム ドキュメント プロパティを操作しますか。](http://go.microsoft.com/fwlink/?LinkId=136772)  
  
## <a name="example"></a>例  
 [!code-vb[Trin_VstcoreProgramming#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/ThisWorkbook.vb#6)]
 [!code-csharp[Trin_VstcoreProgramming#6](../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/ThisWorkbook.cs#6)]  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 未定義の `Value` プロパティにアクセスしようとすると、例外が発生します。  
  
## <a name="see-also"></a>関連項目  
 [VSTO アドインをプログラミングします。](../vsto/programming-vsto-add-ins.md)   
 [プログラムのドキュメント レベルのカスタマイズ](../vsto/programming-document-level-customizations.md)   
 [方法: ドキュメント プロパティの読み書き](../vsto/how-to-read-from-and-write-to-document-properties.md)  
  
  