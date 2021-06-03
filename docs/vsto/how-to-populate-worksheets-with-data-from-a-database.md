---
title: '方法: データベースのデータをワークシートに読み込む'
description: ソリューション内のオブジェクトのデータを使用する方法、および Windows フォーム コントロールを使用してワークシー内のデータを表示する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets [Office development in Visual Studio], populating
- databases [Office development in Visual Studio], populating worksheets
- data [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 66f37a1639cb6a86f107d9372704d5c8364c6a18
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99918569"
---
# <a name="how-to-populate-worksheets-with-data-from-a-database"></a>方法: データベースのデータをワークシートに読み込む

ドキュメント レベルの Office プロジェクトでは、Windows フォーム プロジェクトでデータにアクセスする場合と同じようにデータにアクセスできます。 同じツールとコードを使用してソリューションにデータを取り込むことができ、Windows フォーム コントロールを使用してデータを表示できます。 さらに、ホスト コントロールと呼ばれるコントロールを利用できます。これは、Microsoft Office Excel のネイティブ オブジェクトであり、イベントやデータ バインディング機能が強化されています。 詳細については、「[ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)」を参照してください。

[!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

次の例は、デザイナーを使用してドキュメント レベルのプロジェクトにデータ バインド コントロールを追加する方法を示しています。 実行時にアプリケーション レベルのプロジェクトのデータバインド コントロールを追加する方法の例については、「[チュートリアル: VSTO アドイン プロジェクトでの複合データ バインディング](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md)」を参照してください。

## <a name="add-a-data-bound-control-to-a-worksheet-at-design-time"></a>デザイン時にワークシートにデータバインド コントロールを追加する

### <a name="to-populate-a-worksheet-with-data-from-a-database"></a>データベースからワークシートにデータを読み込むには

1. デザイナーでワークシートを開いた状態で、Visual Studio で Excel ドキュメント レベルのプロジェクトを開きます。

2. **[データ ソース]** ウィンドウを開いて、プロジェクトのデータ ソースを作成します。 詳細については、「[新しい接続を追加する](../data-tools/add-new-connections.md)」を参照してください。

3. 目的のフィールドまたはテーブルを **[データ ソース]** ウィンドウからワークシートにドラッグします。

次のいずれかのコントロールがワークシートに作成されます。

- フィールドをドラッグすると、ワークシートに <xref:Microsoft.Office.Tools.Excel.NamedRange> コントロールが作成されます。 詳細については、「[NamedRange コントロール](../vsto/namedrange-control.md)」を参照してください。

- テーブルをドラッグすると、ワークシートに <xref:Microsoft.Office.Tools.Excel.ListObject> コントロールが作成されます。 詳細については、「[ListObject コントロール](../vsto/listobject-control.md)」を参照してください。

別のコントロールを追加するには、 **[データ ソース]** ウィンドウでテーブルまたはフィールドを選択し、ドロップダウン リストで別のコントロールを選択します。

## <a name="objects-in-the-project"></a>プロジェクト内のオブジェクト

プロジェクトには、コントロールに加えて、データに関連する以下のオブジェクトも自動的に追加されます。

- データベース内の接続したデータ テーブルをカプセル化する型指定されたデータセット。 詳細については、「[Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)」を参照してください。

- コントロールを型指定されたデータセットに接続する <xref:System.Windows.Forms.BindingSource>。 詳細については、「[BindingSource コンポーネントの概要](/dotnet/framework/winforms/controls/bindingsource-component-overview)」を参照してください。

- 型指定されたデータセットをデータベースに接続する TableAdapter。 詳細については、[TableAdapter の概要](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)に関するページを参照してください。

- データセット内の複数のテーブル アダプターを調整することによって階層更新を可能にするために使用される TableAdapterManager。 詳細については、「[階層更新](../data-tools/hierarchical-update.md)」と [TableAdapterManager](../data-tools/fill-datasets-by-using-tableadapters.md#tableadaptermanager-reference) のリファレンスに関するページを参照してください。

プロジェクトを実行すると、データ ソースの先頭のレコードがコントロールに表示されます。 <xref:System.Windows.Forms.BindingSource> を使用すると、ユーザーがレコードをスクロールできるようになります。

### <a name="to-scroll-through-the-records"></a>レコードをスクロールするには

- <xref:System.Windows.Forms.BindingSource.MoveNext%2A> や <xref:System.Windows.Forms.BindingSource.MovePrevious%2A> など、<xref:System.Windows.Forms.BindingSource> のメソッドを使用します。

型指定されたデータセットやデータベースに更新を送信する方法の詳細については、「[方法 : ホスト コントロールからのデータでデータ ソースを更新する](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [Office ソリューションでコントロールにデータをバインドする](../vsto/binding-data-to-controls-in-office-solutions.md)
- [新しいデータ ソースの追加](../data-tools/add-new-data-sources.md)
- [Visual Studio でのデータへの Windows フォーム コントロールのバインド](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [方法: オブジェクトのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [方法: データベースのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [方法: サービスのデータをドキュメントに読み込む](../vsto/how-to-populate-documents-with-data-from-services.md)
- [方法: ホスト コントロールのデータでデータ ソースを更新する](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)