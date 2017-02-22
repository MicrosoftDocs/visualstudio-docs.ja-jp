---
title: "XML スキーマ エクスプローラー | Microsoft Docs"
ms.custom: ""
ms.date: "12/03/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2fc39e98-b194-456b-a452-cfafb0a52d66
caps.latest.revision: 3
caps.handback.revision: 3
author: "kempb"
ms.author: "kempb"
manager: "ghogen"
---
# XML スキーマ エクスプローラー
[!INCLUDE[vs2017banner](../code-quality/includes/vs2017banner.md)]

XML スキーマ エクスプローラーは Microsoft Visual Studio および XML エディターに統合されており、これを使用すると、XML スキーマ定義言語 \(XSD\) スキーマの操作が可能になります。XML スキーマ ファイルを開くと、XML スキーマ エクスプローラーに **\[スキーマ セット\]** ノードが表示されます。XML スキーマ エクスプローラーには、対象ファイルに対してインクルード、インポート、または再定義されたすべてのスキーマだけでなく、`include` ステートメントまたは `import` ステートメントを通じて参照されているファイルも表示されます。  
  
 XML スキーマ エクスプローラーでは、次の操作を実行できます。  
  
-   スキーマ セットの概要をすばやく確認する。  
  
-   ツリーを参照して移動する。  
  
-   キーワード検索とスキーマ固有の検索を実行する。詳細については、「[スキーマ セットの検索](../xml-tools/searching-the-schema-set.md)」を参照してください。  
  
-   グラフ ビューまたはコンテンツ モデル ビューに検索結果を追加する。  
  
-   ドキュメントの順序、ドキュメントの種類、またはドキュメント名でツリーを並べ替える。詳細については、「[並べ替え、フィルター処理、およびグループ化](../xml-tools/sorting-filtering-and-grouping-xml-schema-explorer.md)」を参照してください。  
  
-   XML エディターを開き、XSD ファイルのコードの場所にジャンプする。詳細については、「[XML エディターとの統合](../xml-tools/integration-with-xml-editor.md)」を参照してください。  
  
-   グローバル要素のサンプル XML を生成する。  
  
 XML スキーマ エクスプローラーでは、ツリー ビューでスキーマ セットの階層を表示することができます。また、検索、フィルター処理、ナビゲーション、および並べ替えを行うこともできます。XML スキーマ エクスプローラーにアクセスするには、次のいずれかの操作を実行します。  
  
-   [スタート ビュー](../xml-tools/start-view.md)が表示されている場合は、**\[XML スキーマ エクスプローラー\]** リンクをクリックします。  
  
-   [グラフ ビュー](../xml-tools/graph-view.md)または[コンテンツ モデル ビュー](../xml-tools/content-model-view.md)が表示されており、ワークスペース内にノードが存在する場合は、コンテキスト メニューを使用して XML スキーマ エクスプローラーを選択します。  
  
-   **\[表示\]** メニューからも **\[XML スキーマ エクスプローラー\]** を選択できます。  
  
-   .xsd ファイルに関連付けられた Visual Basic の XML リテラルが記述されている .vb ファイルからも XML スキーマ エクスプローラーにアクセスできます。XML スキーマ エクスプローラーでスキーマ セットを表示するには、XML リテラルまたは XML 名前空間インポートで XML ノードを右クリックして、**\[スキーマ エクスプローラーで表示\]** コマンドをクリックします。詳細については、「[XML リテラルと XML スキーマ エクスプローラーの統合](../xml-tools/integration-of-xml-literals-with-xml-schema-explorer.md)」を参照してください。  
  
## ツリー ビュー  
 XML スキーマ エクスプローラーでは、事前にコンパイルされたスキーマ セット情報がツリー構造で表示されます。ツリー構造は、次のように構成されます。  
  
-   最上位レベルは、スキーマ セット ノードです。  
  
-   2 番目のレベルには名前空間が含まれます。  
  
-   3 番目のレベルにはファイルが含まれます。  
  
-   4 番目のレベルにはグローバル ノードが含まれます。これには、要素、グループ、複合型、単純型、属性、属性グループ、`include` ステートメント`import` ステートメント、および `redefine` ステートメントを含めることができます。  
  
 ツリー構造の例を次に示します。  
  
 ![XML スキーマ エクスプローラー](../xml-tools/media/xmlschemaexplorer.gif "XMLSchemaExplorer")  
  
## 選択とアクティブ化  
 ノードを強調表示して選択するには、スキーマ エクスプローラーでそのノードをクリックします。  
  
 ノードをアクティブ化するには、ノードをダブルクリックするか、ノードを選択して **Enter** キーを押します。  
  
-   ノードをアクティブ化すると、このノードが定義されているファイルが開き \(ファイルが既に開かれていない場合\)、ファイル内でノードが選択されます。  
  
-   ファイル ノードをアクティブ化すると、選択されたファイルが開き \(既に開かれていない場合\)、`<schema>` ノードが強調表示されます。  
  
-   SchemaSet または名前空間ノードをアクティブ化しても、何も行われません。  
  
## ノードのドラッグ アンド ドロップ  
 グローバル ノード、ファイル ノード、名前空間ノードを XSD デザイナーのビューにドラッグ アンド ドロップすることができます。現在のビューが[スタート ビュー](../xml-tools/start-view.md)の場合は、ビューにノードをドラッグすると、[グラフ ビュー](../xml-tools/graph-view.md)が開きます。現在のビューが[コンテンツ モデル ビュー](../xml-tools/content-model-view.md)またはグラフ ビューの場合は、ビューにノードをドロップしてもビューは変化しません。  
  
 ビューにファイルをドロップすると、ファイル内のすべてのグローバル ノードが [XSD デザイナーのワークスぺース](../xml-tools/xml-schema-designer-workspace.md)に追加されます。ビューに名前空間をドロップすると、名前空間内のすべてのグローバル ノードがワークスぺースに追加されます。ワークスペースは、すべてのビューで共有されます。  
  
 ローカル ノードまたはローカル インポートをドラッグ アンド ドロップすることはできません。  
  
## このセクションのトピック  
  
-   [スキーマ セットの検索](../xml-tools/searching-the-schema-set.md)  
  
-   [並べ替え、フィルター処理、およびグループ化](../xml-tools/sorting-filtering-and-grouping-xml-schema-explorer.md)  
  
-   [コンテキスト メニュー](../xml-tools/context-menus-xml-schema-explorer.md)  
  
-   [XML リテラルと XML スキーマ エクスプローラーの統合](../xml-tools/integration-of-xml-literals-with-xml-schema-explorer.md)  
  
## 参照  
 [方法: XML スキーマ エクスプローラーからワークスペースにノードを追加する](../Topic/How%20to:%20Add%20Nodes%20to%20the%20Workspace%20from%20the%20XML%20Schema%20Explorer.md)