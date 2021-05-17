---
title: XML データのデータセットへの読み込み
description: データセットに XML データを読み込みます。 このチュートリアルでは、XML データをデータセットに読み込む Windows アプリケーションを作成します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- reading XML
- data access [Visual Studio], XML data
- reading files, XML
- data [Visual Studio], reading from XML files
- reading data, XML files
- XML [Visual Studio], reading
- XML documents, reading
- datasets [Visual Basic], reading XML data
ms.assetid: fae72958-0893-47d6-b3dd-9d42418418e4
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: b3a238bf325819b340b983618b5aac8f723184f4
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216190"
---
# <a name="read-xml-data-into-a-dataset"></a>XML データのデータセットへの読み込み

ADO.NET には、XML データを操作するための単純なメソッドが用意されています。 このチュートリアルでは、XML データをデータセットに読み込む Windows アプリケーションを作成します。 次に、データセットが <xref:System.Windows.Forms.DataGridView> コントロールに表示されます。 最後に、XML ファイルの内容に基づく XML スキーマがテキスト ボックスに表示されます。

## <a name="create-a-new-project"></a>新しいプロジェクトを作成する

C# または Visual Basic 用の新しい **Windows フォーム アプリ** プロジェクトを作成します。 プロジェクトに **ReadingXML** という名前を付けます。

## <a name="generate-the-xml-file-to-be-read-into-the-dataset"></a>データセットに読み込む XML ファイルを生成する

このチュートリアルでは、XML データをデータセットに読み込むことに重点を置いて、XML ファイルの内容を示します。

1. **[プロジェクト]** メニューで、 **[新しい項目の追加]** を選択します。

2. **[XML ファイル]** を選択し、ファイルに **authors.xml** という名前を指定して、 **[追加]** を選択します。

   XML ファイルがデザイナーに読み込まれ、編集できる状態になります。

3. 次の XML データをエディターの XML 宣言の下に貼り付けます。

   ```xml
   <Authors_Table>
     <authors>
       <au_id>172-32-1176</au_id>
       <au_lname>White</au_lname>
       <au_fname>Johnson</au_fname>
       <phone>408 496-7223</phone>
       <address>10932 Bigge Rd.</address>
       <city>Menlo Park</city>
       <state>CA</state>
       <zip>94025</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>213-46-8915</au_id>
       <au_lname>Green</au_lname>
       <au_fname>Margie</au_fname>
       <phone>415 986-7020</phone>
       <address>309 63rd St. #411</address>
       <city>Oakland</city>
       <state>CA</state>
       <zip>94618</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>238-95-7766</au_id>
       <au_lname>Carson</au_lname>
       <au_fname>Cheryl</au_fname>
       <phone>415 548-7723</phone>
       <address>589 Darwin Ln.</address>
       <city>Berkeley</city>
       <state>CA</state>
       <zip>94705</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>267-41-2394</au_id>
       <au_lname>Hunter</au_lname>
       <au_fname>Anne</au_fname>
       <phone>408 286-2428</phone>
       <address>22 Cleveland Av. #14</address>
       <city>San Jose</city>
       <state>CA</state>
       <zip>95128</zip>
       <contract>true</contract>
     </authors>
     <authors>
       <au_id>274-80-9391</au_id>
       <au_lname>Straight</au_lname>
       <au_fname>Dean</au_fname>
       <phone>415 834-2919</phone>
       <address>5420 College Av.</address>
       <city>Oakland</city>
       <state>CA</state>
       <zip>94609</zip>
       <contract>true</contract>
     </authors>
   </Authors_Table>
   ```

4. **[ファイル]** メニューの **[authors.xml を保存]** を選択します。

## <a name="create-the-user-interface"></a>ユーザー インターフェイスを作成する

このアプリケーションのユーザー インターフェイスは、次の要素で構成されています。

- XML ファイルの内容をデータとして表示する <xref:System.Windows.Forms.DataGridView> コントロール。

- XML ファイルの XML スキーマを表示する <xref:System.Windows.Forms.TextBox> コントロール。

- 2 つの <xref:System.Windows.Forms.Button> コントロール。

  - ボタンの 1 つは、XML ファイルをデータセットに読み込み、<xref:System.Windows.Forms.DataGridView> コントロールに表示するために使用します。

  - 2 番目のボタンは、データセットからスキーマを抽出し、<xref:System.IO.StringWriter> を使用して <xref:System.Windows.Forms.TextBox> コントロールに表示するために使用します。

### <a name="to-add-controls-to-the-form"></a>フォームにコントロールを追加するには

1. デザイン ビューで `Form1` を開きます。

2. **[ツールボックス]** から、次のコントロールをフォームにドラッグします。

    - 1 つの <xref:System.Windows.Forms.DataGridView> コントロール

    - 1 つの <xref:System.Windows.Forms.TextBox> コントロール

    - 2 つの <xref:System.Windows.Forms.Button> コントロール

3. 次のプロパティを設定します。

    |コントロール|プロパティ|設定|
    |-------------|--------------|-------------|
    |`TextBox1`|**Multiline**|`true`|
    ||**スクロールバー**|**垂直方向**|
    |`Button1`|**名前**|`ReadXmlButton`|
    ||**[テキスト]**|`Read XML`|
    |`Button2`|**名前**|`ShowSchemaButton`|
    ||**Text**|`Show Schema`|

## <a name="create-the-dataset-that-receives-the-xml-data"></a>XML データを受け取るデータセットを作成する

この手順では、`authors` という名前の新しいデータセットを作成します。 データセットの詳細については、「[Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)」を参照してください。

1. **ソリューション エクスプローラー** で、**Form1** のソース ファイルを選択し、 **[ソリューション エクスプローラー]** ツールバーの **[ビュー デザイナー]** ボタンを選択します。

2. [ツールボックス、[データ] タブ](../ide/reference/toolbox-data-tab.md)から、**DataSet** を **Form1** にドラッグします。

3. **[データセットの追加]** ダイアログ ボックスで、 **[型指定されていないデータセット]** 、 **[OK]** の順に選択します。

     **DataSet1** がコンポーネント トレイに追加されます。

4. **[プロパティ]** ウィンドウで、`AuthorsDataSet` の **[名前]** と <xref:System.Data.DataSet.DataSetName%2A> プロパティを設定します。

## <a name="create-the-event-handler-to-read-the-xml-file-into-the-dataset"></a>XML ファイルをデータセットに読み込むイベント ハンドラーを作成する

**[XML の読み取り]** ボタンを使用すると、XML ファイルがデータセットに読み込まれます。 次に、それをデータセットにバインドする <xref:System.Windows.Forms.DataGridView> コントロールのプロパティが設定されます。

1. **ソリューション エクスプローラー** で、**Form1** を選択し、 **[ソリューション エクスプローラー]** ツールバーの **[ビュー デザイナー]** ボタンを選択します。

2. **[XML の読み取り]** ボタンを選択します。

     **コード エディター** に `ReadXmlButton_Click` イベント ハンドラーが表示されます。

3. 次のコードを `ReadXmlButton_Click` イベント ハンドラーに入力します。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form1.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form1.vb" id="Snippet2":::

4. `ReadXMLButton_Click` イベント ハンドラーのコードで、`filepath =` エントリを正しいパスに変更します。

## <a name="create-the-event-handler-to-display-the-schema-in-the-textbox"></a>イベント ハンドラーを作成し、テキスト ボックスにスキーマを表示する

**[スキーマの表示]** ボタンを使用すると、スキーマを格納した <xref:System.IO.StringWriter> オブジェクトが作成され、<xref:System.Windows.Forms.TextBox> コントロールに表示されます。

1. **ソリューション エクスプローラー** で、**Form1** を選択し、 **[ビュー デザイナー]** ボタンを選択します。

2. **[スキーマの表示]** ボタンを選択します。

     **コード エディター** に `ShowSchemaButton_Click` イベント ハンドラーが表示されます。

3. `ShowSchemaButton_Click` イベント ハンドラーに次のコードを貼り付けます。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/CS/Form1.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataFillingAndExecuting/VB/Form1.vb" id="Snippet3":::

## <a name="test-the-form"></a>フォームをテストする

フォームをテストして、期待どおりに動作することを確認します。

1. **F5** キーを選択してアプリケーションを実行します。

2. **[XML の読み取り]** ボタンを選択します。

     DataGridView に XML ファイルの内容が表示されます。

3. **[スキーマの表示]** ボタンを選択します。

     テキスト ボックスに XML ファイルの XML スキーマが表示されます。

## <a name="next-steps"></a>次のステップ

このチュートリアルでは、XML ファイルをデータセットに読み込む方法、および XML ファイルの内容に基づいてスキーマを作成する方法の基本について説明します。 次に行う作業を以下に示します。

- データセット内のデータを編集し、XML として書き戻します。 詳細については、「<xref:System.Data.DataSet.WriteXml%2A>」を参照してください。

- データセット内のデータを編集し、データベースに書き込みます。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
- [Visual Studio の XML ツール](../xml-tools/xml-tools-in-visual-studio.md)
