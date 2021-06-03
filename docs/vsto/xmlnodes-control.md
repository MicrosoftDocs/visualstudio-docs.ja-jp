---
title: XMLNodes コントロール
description: XMLNodes コントロールは、繰り返しスキーマ要素が Microsoft Word 文書にマップされている場合にのみ作成されることを説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNodes control, events
- XMLNodes control
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d920df609c8172b6329cac537d10868e5795be12
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894388"
---
# <a name="xmlnodes-control"></a>XMLNodes コントロール
  **重要** このトピックに記載されている Microsoft Word に関する情報は、Microsoft が カスタム XML に関連する特定の機能を Microsoft Word から削除した 2010 年 1 月より前に Microsoft によってライセンス供与された Microsoft Word 製品を使用している米国領土外を本拠地とする個人と組織、またはそのような Microsoft Word 製品上で実行されるプログラムを開発している個人または開発者のみを対象にしています。 Microsoft Word に関するこの情報は、2010 年 1 月 10 日以降に Microsoft によってライセンス供与された Microsoft Word 製品を使用している、またはその上で実行されるプログラムを開発している米国内の個人または組織は対象外であり、使用することはできません。それらの製品は、その日付より前にライセンス供与された製品または米国外で使用するために購入およびライセンス供与された製品と同様に動作することはありません。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールは、イベントを公開する、マップされた XML ノード オブジェクトのコレクションです。 <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールは、繰り返しスキーマ要素が Microsoft Office Word 文書にマップされている場合にのみ作成されます。 繰り返し要素に子要素が含まれている場合は、各子要素も <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールとして作成されます。

 Visual Studio によって XML ノードのコレクションが作成された後、Word オブジェクト モデルを調べずにコントロールに対して直接プログラミングできます。 <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールは、ドキュメントで要素のマッピングを削除することによってのみ削除できます。

> [!NOTE]
> <xref:Microsoft.Office.Tools.Word.XMLNodes.Item%2A> プロパティを使用して <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールの子要素にアクセスした場合、<xref:Microsoft.Office.Tools.Word.XMLNode> コントロールではなく、<xref:Microsoft.Office.Interop.Word.XMLNode> オブジェクトを返します。 詳細については、「[ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)」を参照してください。

## <a name="bind-data-to-the-control"></a>データをコントロールにバインドする
 <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールではデータ バインディングがサポートされていません。 これは、<xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールには複雑なデータ バインディング機能がなく、単純なデータ バインディングでは繰り返しデータを表すことができないためです。

## <a name="formatting"></a>書式設定
 ドキュメント内のテキストに適用できる書式設定は、<xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールに適用できます。

## <a name="events"></a>イベント
 <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールで使用できるイベントは次のとおりです。

- <xref:Microsoft.Office.Tools.Word.XMLNodes.AfterInsert>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.BeforeDelete>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextLeave>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.Deselect>

- <xref:System.ComponentModel.IComponent.Disposed>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.Select>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ValidationError>

## <a name="compare-events"></a>イベントを比較する
 ユーザーが特定の <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールのコンテキスト内でカーソルを移動したときにイベントをキャプチャできます。 たとえば、次に示すような、`Company` という名前の子 <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールを持つ `Customer` という名前の <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールがあり、この `Company` には `CompanyName` と `CompanyRegion` いう名前の 2 つの子 <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールがあるとします。

```xml
<Customer>
    <Company>
        <CompanyName>
        <CompanyRegion>
```

 カーソルが `Company` ノードに移動されたときに常に操作ウィンドウにコントロールを表示する場合、カーソルが `CompanyName` と `CompanyRegion` のどちらに置かれているかは問題ではありません。理由は、どちらも `Company` のコンテキスト内にあるためです。 この場合は、`Company` の <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> イベント内にコードを記述できます。

 ほとんどの場合、カーソルが <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールに入ると、<xref:Microsoft.Office.Tools.Word.XMLNodes.Select> イベントと <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> イベントの両方が発生します。 次の表は、これらのイベントの間の違いを示しています。

|イベントの選択|ContextEnter イベント|
|------------------|------------------------|
|カーソルが、<xref:Microsoft.Office.Tools.Word.XMLNodes> コレクションのノードの 1 つの内側に置かれると発生します。|カーソルが、ノードのコンテキストの外側の領域から、<xref:Microsoft.Office.Tools.Word.XMLNodes> コレクションのノードの 1 つ、または子孫ノードの内側に置かれると発生します。 つまり、コンテキストが変更されたときにのみ発生し、入れ子になった複数の <xref:Microsoft.Office.Tools.Word.XMLNodes> コントロールに対して発生させることができます。|

 たとえば、`Customer` の外側から `CompanyName` 内にカーソルを移動すると、`Customer`、`Company`、`CompanyName` の <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> イベントが発生します。 その後、`CompanyName` から `CompanyRegion` にカーソルを移動すると、`CompanyRegion` の <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> イベントのみが発生します。これは、コンテキストが `Company` と `Customer` の両方で同じであるためです。 ドキュメントに複数の `Company` ノードを指定できます。 カーソルをある `Company` の `CompanyName` ノードから別の `Company` の `CompanyName` ノードに移動した場合、コンテキストは同じであるため、<xref:Microsoft.Office.Tools.Word.XMLNodes.Select> イベントのみが発生します。

 <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextLeave> イベントと <xref:Microsoft.Office.Tools.Word.XMLNodes.Deselect> イベントの間にも同じ違いがあります。

## <a name="see-also"></a>関連項目
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [XMLNode コントロール](../vsto/xmlnode-control.md)
- [方法: Word 文書に XMLNodes コントロールを追加する](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md)
- [方法: Visual Studio 内で Word 文書にスキーマを割り当てる](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
