---
title: ドキュメント ホスト項目
description: ドキュメント ホスト項目は、Word のプライマリ相互運用機能アセンブリの Document 型を拡張する型であることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio]
- documents [Office development in Visual Studio], document host items
- document host items
- Word [Office development in Visual Studio], Word documents
- Word [Office development in Visual Studio]
- Word documents
- host items [Office development in Visual Studio], Document
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b7eb29a9cae9e43bd0372088298d2bd6b122c7a1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99910579"
---
# <a name="document-host-item"></a>ドキュメント ホスト項目
  <xref:Microsoft.Office.Tools.Word.Document> ホスト項目は、Word のプライマリ相互運用機能アセンブリの <xref:Microsoft.Office.Interop.Word.Document> 型を拡張する型です。 <xref:Microsoft.Office.Tools.Word.Document> ホスト項目には、 <xref:Microsoft.Office.Interop.Word.Document> オブジェクトと同じプロパティ、メソッド、イベントがすべて用意されています。また、追加のイベントも公開し、ホスト コントロールおよび Windows フォーム コントロールのコンテナーとしても機能します。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 ドキュメント レベルのプロジェクトには、プロジェクト内のドキュメントを表す既定の <xref:Microsoft.Office.Tools.Word.Document> ホスト項目があります。 VSTO アドイン プロジェクトでは、実行時に <xref:Microsoft.Office.Tools.Word.Document> ホスト項目を生成できます。

## <a name="understand-the-document-host-item-in-document-level-projects"></a>ドキュメント レベルのプロジェクトのドキュメント ホスト項目について
 プロジェクトのドキュメントにアクセスするには、 `ThisDocument` クラスを使用します。 ドキュメント レベルのプロジェクトを作成すると、Visual Studio が、Word とカスタマイズ コード間の通信リンクとして機能する `ThisDocument` クラスを生成します。 `ThisDocument` クラスによって、 <xref:Microsoft.Office.Tools.Word.Document> ホスト項目のメンバーにアクセスし、ドキュメントが開かれたり閉じられたりしたときにコードを実行するなど、カスタマイズの基本的なタスクを実行できます。 また、このクラスを使用して、ドキュメントにコントロールを追加することもできます。 さまざまな種類のコントロールを組み合わせ、コードを記述することによって、コントロールのデータへのバインド、ユーザー情報の収集、およびユーザーの操作への応答を実行できます。 詳細については、「[プログラムによるドキュメントレベルのカスタマイズ](../vsto/programming-document-level-customizations.md)」を参照してください。

 `ThisDocument` クラスには、プロジェクトでコードの記述を開始できる場所が用意されています。 このクラスには、Word のプライマリ相互運用機能アセンブリの <xref:Microsoft.Office.Interop.Word.Document> オブジェクトと同じプロパティ、メソッド、イベントがすべて用意されているため、 `ThisDocument` を使用して Word のオブジェクト モデルにアクセスすることもできます。 詳細については、「[Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)」を参照してください。

### <a name="limitations-of-the-document-host-item-in-document-level-projects"></a>ドキュメント レベルのプロジェクトのドキュメント ホスト項目に関する制限
 ドキュメント レベルのプロジェクトには、1 つの <xref:Microsoft.Office.Tools.Word.Document> ホスト項目のみ (つまり `ThisDocument` クラス) を含めることができます。 デザイン時に新しい <xref:Microsoft.Office.Tools.Word.Document> ホスト項目をプロジェクトに追加することはできません。また、実行時にドキュメント レベルのカスタマイズから新しい <xref:Microsoft.Office.Tools.Word.Document> ホスト項目を作成することもできません。

 実行時に新しい Word ドキュメントを作成すると、そのワークシートは <xref:Microsoft.Office.Interop.Word.Document>型になります。 これはホスト項目ではないため、ホスト コントロールや Windows フォーム コントロールを含めることはできません。 実行時にドキュメントを作成する方法の詳細については、「[方法: プログラムで新しい文書を作成する](../vsto/how-to-programmatically-create-new-documents.md)」を参照してください。

## <a name="understand-document-host-items-in-application-level-projects"></a>アプリケーションレベルのプロジェクトのドキュメント ホスト項目について
 VSTO アドイン プロジェクトでは、Word で開いている任意のドキュメントで <xref:Microsoft.Office.Tools.Word.Document> ホスト項目を実行時に生成できます。 <xref:Microsoft.Office.Tools.Word.Document> ホスト項目を使用して、関連付けられたドキュメントにコントロールを追加したり、 <xref:Microsoft.Office.Interop.Word.Document> オブジェクトで使用できないイベントを処理したりできます。

 <xref:Microsoft.Office.Tools.Word.Document> ホスト項目を生成するには、`GetVstoObject` メソッドを使用します。 詳細については、「[実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [Word オブジェクト モデルの概要](../vsto/word-object-model-overview.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [実行時に VSTO アドインの Word 文書と Excel ブックを拡張する](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
