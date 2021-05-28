---
title: XMLNode コントロール
description: XMLNode コントロールは、イベントを公開する XML ノード オブジェクトであり、データにバインドできることについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNode control
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9e86bfbe7af122e2557178f5d70256903d0cc740
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949715"
---
# <a name="xmlnode-control"></a>XMLNode コントロール
  **重要** このトピックに記載されている Microsoft Word に関する情報は、Microsoft がカスタム XML に関連する特定の機能を Microsoft Word から削除した 2010 年 1 月より前に Microsoft によってライセンス供与された Microsoft Word 製品を使用している米国領土外を本拠地とする個人と組織、またはそのような Microsoft Word 製品上で実行されるプログラムを開発している個人または開発者のみを対象にしています。 Microsoft Word に関するこの情報は、2010 年 1 月 10 日以降に Microsoft によってライセンス供与された Microsoft Word 製品を使用している、またはその上で実行されるプログラムを開発している米国内の個人または組織は対象外であり、使用することはできません。それらの製品は、その日付より前にライセンス供与された製品または米国外で使用するために購入およびライセンス供与された製品と同様に動作することはありません。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールはイベントを公開する XML ノード オブジェクトであり、データにバインドできます。 <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールは、非繰り返しスキーマ要素が Microsoft Office Word 文書にマップされている場合にのみ作成されます。 Visual Studio によって XML ノードが作成された後、Word オブジェクト モデルを使用せずに直接プログラミングできます。

 <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールは、Word で要素のマッピングを削除することによってのみ削除できます。

## <a name="bind-data-to-the-control"></a>データをコントロールにバインドする
 <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールでは、単純データ バインディングがサポートされます。 XML ノードは、<xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> プロパティを使用してデータ ソースにバインドする必要があります。 バインドされたデータセット内のデータが更新されると、 <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールがその変更を反映させます。

## <a name="formatting"></a>書式設定
 <xref:Microsoft.Office.Interop.Word.XMLNode> オブジェクトに適用できる書式設定を、<xref:Microsoft.Office.Tools.Word.XMLNode> コントロールに適用できます。 これには、フォント、下線スタイル、および文字スタイルが含まれます。

## <a name="events"></a>イベント
 次のイベントは <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールに対して利用できます。

- <xref:Microsoft.Office.Tools.Word.XMLNode.AfterInsert>

- <xref:Microsoft.Office.Tools.Word.XMLNode.BeforeDelete>

- <xref:Microsoft.Office.Tools.Word.XMLNode.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter>

- <xref:Microsoft.Office.Tools.Word.XMLNode.ContextLeave>

- <xref:Microsoft.Office.Tools.Word.XMLNode.Deselect>

- <xref:System.ComponentModel.IComponent.Disposed>

- <xref:Microsoft.Office.Tools.Word.XMLNode.Select>

- <xref:Microsoft.Office.Tools.Word.XMLNode.ValidationError>

## <a name="compare-events"></a>イベントを比較する
 ユーザーが特定の <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールのコンテキスト内でカーソルを移動したときにイベントをキャプチャできます。 たとえば、次に示すような、`Company` という名前の子 <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールを持つ `Customer` という名前の <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールがあり、この `Company` コントロールには `CompanyName` と `CompanyRegion` いう名前の 2 つの子 <xref:Microsoft.Office.Tools.Word.XMLNode> があるとします。

```xml
<Customer>
    <Company>
        <CompanyName>
        <CompanyRegion>
```

 カーソルが `Company` ノードに移動されたときに常に操作ウィンドウにコントロールを表示する場合、カーソルが `CompanyName` と `CompanyRegion` のどちらに置かれているかは問題ではありません。理由は、どちらも `Company` のコンテキスト内にあるためです。 この場合は、`Company` の <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> イベント内にコードを記述できます。

 ほとんどの場合、カーソルが <xref:Microsoft.Office.Tools.Word.XMLNode> コントロールに入ると、<xref:Microsoft.Office.Tools.Word.XMLNode.Select> イベントと <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> イベントの両方が発生します。 次の表は、これらのイベントの間の違いを示しています。

|イベントの選択|ContextEnter イベント|
|------------------|------------------------|
|カーソルが <xref:Microsoft.Office.Tools.Word.XMLNode> の内側に置かれたときに発生します。|ポインターが <xref:Microsoft.Office.Tools.Word.XMLNode> またはその子孫ノードの内部に、ノードのコンテキスト外から配置されたときに発生します。 つまり、コンテキストが変更された場合にのみ発生します。|

 たとえば、`Customer` の外側から `CompanyName` 内にカーソルを移動すると、`Customer`、`Company`、および `CompanyName` の <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> イベントが発生します。 その後、`CompanyName` から `CompanyRegion` にカーソルを移動すると、`Company` と `Customer` の両方のコンテキスト内にあるため、`CompanyRegion` の <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> イベントのみが発生します。

 <xref:Microsoft.Office.Tools.Word.XMLNode.ContextLeave> イベントと <xref:Microsoft.Office.Tools.Word.XMLNode.Deselect> イベントの間にも同じ違いがあります。

## <a name="see-also"></a>関連項目
- [ホスト項目とホスト コントロールの概要](../vsto/host-items-and-host-controls-overview.md)
- [拡張オブジェクトを使用して Word を自動化する](../vsto/automating-word-by-using-extended-objects.md)
- [XMLNodes コントロール](../vsto/xmlnodes-control.md)
- [方法: Word 文書に XMLNode コントロールを追加する](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)
- [方法: Visual Studio 内で Word 文書にスキーマを割り当てる](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [ホスト項目とホスト コントロールのプログラム上の制限事項](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
