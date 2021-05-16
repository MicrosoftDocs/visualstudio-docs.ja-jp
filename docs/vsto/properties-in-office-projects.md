---
title: Office プロジェクトのプロパティ
description: Visual Studio で Office プロジェクトに使用できて、[プロパティ] ウィンドウからアクセスできるプロパティについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Trust Assemblies Location property
- Cache in Document property
- properties [Office development in Visual Studio]
- Namespace for Host Item property
- Office projects [Office development in Visual Studio], properties
- projects [Office development in Visual Studio], properties
- Value2 property
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 5f7a2ab04e1926a53c3d3aa05023103206c6aa01
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99971766"
---
# <a name="properties-in-office-projects"></a>Office プロジェクトのプロパティ
  Visual Studio で Office プロジェクトに使用できる重要なプロパティがいくつかあります。 これらのプロパティには [ **プロパティ** ] ウィンドウでアクセスできます。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="namespace-for-host-item"></a>ホスト項目の名前空間
 Visual C# プロジェクトでホスト項目クラス (たとえば、 **、** 、 `ThisAddIn`クラス) の名前空間を変更するには、[ `ThisWorkbook`ホスト項目の名前空間 `ThisDocument` ] プロパティを使用します。 このプロパティは、**ソリューション エクスプローラー** でドキュメント レベル プロジェクト (*ExcelWorkbook1.xlsx* や *WordDocument1.docx* など) のドキュメント ノードを選択するか、または VSTO アドイン プロジェクト (Excel や Word など) のアプリケーション ノードを選択した場合に、 **[プロパティ]** ウィンドウに表示されます。

 Visual C# Office プロジェクトを作成すると、プロジェクトの名前に基づいてホスト項目に名前空間が与えられます。 コード ファイルを直接編集するのではなく、[ **ホスト項目の名前空間** ] プロパティを使用して名前空間を変更することをお勧めします。 このプロパティを使用すると、名前空間は、生成されるコード ファイル (非表示) だけでなく、表示されるコード ファイル内でも変更されます。

## <a name="cacheindocument"></a>CacheInDocument
 **CacheInDocument** プロパティは、Visual Studio デザイナーで **のインスタンスを選択すると、ドキュメント レベルのプロジェクトの [** プロパティ <xref:System.Data.DataSet> ] ウィンドウに表示されます。 パブリック メンバーだけがキャッシュされます。 **をキャッシュする場合は、[** Modifiers **] プロパティを [** Public <xref:System.Data.DataSet>] に設定してください。

 このプロパティはブール値を受け取ります。

- ドキュメント内のデータセットをキャッシュする場合は、 **true** を選択します。

- ドキュメントのデータセットをキャッシュしない場合は、 **false** を選択します。

  データのキャッシュの詳細については、「[ドキュメント レベルのカスタマイズのキャッシュ データ](../vsto/cached-data-in-document-level-customizations.md)」を参照してください。

## <a name="value2"></a>Value2
 **Value2** プロパティは、Excel ブック プロジェクトまたはテンプレート プロジェクトにのみ使用できます。 ワークシート デザイナーで **コントロールを選択すると、[** プロパティ **] ウィンドウの** Databindings <xref:Microsoft.Office.Tools.Excel.NamedRange> プロパティの下に表示されます。

 **の** プロパティをデータ ソースのフィールドにバインドするには、[ **プロパティ** ] ウィンドウの <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> Value2 <xref:Microsoft.Office.Tools.Excel.NamedRange> プロパティを使用します。

## <a name="see-also"></a>関連項目
- [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)
- [Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)
- [Office プロジェクトのイベント](../vsto/events-in-office-projects.md)
