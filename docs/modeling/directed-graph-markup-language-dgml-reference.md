---
title: Directed Graph Markup Language (DGML) リファレンス
ms.date: 11/04/2016
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b473dc706cd7183835c5d84091fb53e45337c013
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60040223"
---
# <a name="directed-graph-markup-language-dgml-reference"></a>Directed Graph Markup Language (DGML) リファレンス

Directed Graph Markup Language (DGML) は、視覚化と、複雑性の分析を実行するために使用する情報を記述する、Visual Studio でコード マップを保持するために使用される形式です。 DGML では、単純な XML を使用して、循環と非循環の両方の有向グラフを記述します。 有向グラフは、リンク (エッジ) によって接続されている一連のノードです。 ノードとリンクを使用すると、ネットワーク構造 (ソフトウェア プロジェクトの要素など) を表すことができます。

Visual Studio のバージョンによっては、DGML 機能のサブセットのみをサポートしてを参照してください[アーキテクチャとモデリング ツールのバージョンのサポート](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)します。

> [!NOTE]
> .dgml ファイルを編集するときは、各要素とその値に使用できる属性が IntelliSense によって識別されます。 属性で色を指定するには、一般的な色の名前 ("Blue" など) または ARGB 16 進値 ("#ffa0b1c3" など) を使用してください。 DGML では、WPF (Windows Presentation Foundation) 色定義形式の小さいサブセットを使用します。 詳細については、次を参照してください。 [Colors クラス](http://go.microsoft.com/fwlink/?LinkId=182345)します。

## <a name="DGML"></a> DGML の構文

次の表は、DGML で使用される要素の種類について説明しています。

- `<DirectedGraph></DirectedGraph>`

   この要素は、コード マップ (.dgml) ドキュメントのルート要素です。 他のすべての DGML 要素は、この要素のスコープ内に表示されます。

   追加できる属性 (省略可能) は次のとおりです。

   `Background` - マップの背景色

   `BackgroundImage` - マップの背景として使用するイメージ ファイルの場所。

   `GraphDirection` - マップがツリー レイアウト (`Sugiyama`) に設定された場合に、ほとんどのリンクが指定方向 (`TopToBottom`、`BottomToTop`、`LeftToRight`、または `RightToLeft`) に向かうようにノードを配置します。 参照してください[マップ レイアウトを変更する](../modeling/browse-and-rearrange-code-maps.md#Selecting)します。

   `Layout` - マップのレイアウトを `None`、`Sugiyama` (ツリー レイアウト)、`ForceDirected` (クイック クラスター)、または `DependencyMatrix` に設定します。 参照してください[マップ レイアウトを変更する](../modeling/browse-and-rearrange-code-maps.md#Selecting)します。

   `NeighborhoodDistance` - マップがツリー レイアウトまたはクイック クラスター レイアウトに設定された場合に、選択したノードから指定されたリンク数 (1 ～ 7) 離れたノードのみ表示します。 参照してください[マップ レイアウトを変更する](../modeling/browse-and-rearrange-code-maps.md#Selecting)します。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" Background="Blue" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        ...
     </Nodes>
     <Links>
        ...
     </Links>
     <Categories>
        ...
     </Categories>
     <Properties>
        ...
     </Properties>
  </DirectedGraph>
  ```

- `<Nodes></Nodes>`

   この省略可能な要素には、マップ上のノードを定義する `<Node/>` 要素の一覧が含まれます。 詳細については、`<Node/>` 要素を参照してください。

  > [!NOTE]
  > `<Link/>` 要素内の未定義のノードを参照すると、マップは `<Node/>` 要素を自動的に作成します。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node ... />
     </Nodes>
     <Links>
        <Link ... />
     </Links>
  </DirectedGraph>
  ```

- `<Node/>`

   この要素は、単一のノードを定義します。 この要素は、`<Nodes><Nodes/>` 要素の一覧内に表示されます。

   この要素には、次の属性が必要です。

   `Id` - ノードの一意の名前。`Label` 属性が別途指定されていない場合は、`Label` 属性の既定値です。 この名前は、名前を参照するリンクの `Source` 属性または `Target` 属性と一致する必要があります。

   追加できる属性 (省略可能) の一部を次に示します。

   `Label` -ノードの表示名。

   スタイル属性。 「 [DGML ファイルを編集してコード マップをカスタマイズする](../modeling/customize-code-maps-by-editing-the-dgml-files.md)」を参照してください。

   `Category` - この属性を共有する要素を識別するカテゴリの名前。 詳細については、`<Category/>` 要素を参照してください。

   `Property` - プロパティ値が同じ要素を識別するプロパティの名前。 詳細については、`<Property/>` 要素を参照してください。

   `Group` - ノードに他のノードが含まれている場合は、この属性を `Expanded` または `Collapsed` に設定して、そのコンテンツの表示と非表示を切り替えます。 `<Link/>` 属性を含み、親ノードをリンク元ノード、子ノードをリンク先ノードとして指定する `Category="Contains"` 要素が必要です。 参照してください[コード要素をグループ化](../modeling/customize-code-maps-by-editing-the-dgml-files.md#OrganizeNodes)します。

   `Visibility` - この属性を `Visible`、`Hidden`、または `Collapsed` に設定します。 `System.Windows.Visibility`が使用されます。 参照してください[非表示にするか、ノードの表示とリンク](../modeling/browse-and-rearrange-code-maps.md#HidingShowing)します。

   `Reference` - この属性をドキュメントまたは URL へのリンクに設定します。 参照してください[コード要素およびリンクにドキュメントまたは Url をリンク](../modeling/customize-code-maps-by-editing-the-dgml-files.md#AddReferences)します。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Student" Category="Person" />
        <Node Id="Passenger" Label="Instructor" Category="Person" />
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
     </Nodes>
     <Links>
        <Link ... />
     </Links>
     <Categories>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
     </Categories>
  </DirectedGraph>
  ```

- `<Links></Links>`

   この要素には、ノード間のリンクを定義する `<Link>` 要素の一覧が含まれます。 詳細については、`<Link/>` 要素を参照してください。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Links>
        <Link ... />
     </Links>
  </DirectedGraph>
  ```

- `<Link/>`

   この要素は、リンク元ノードをリンク先ノードに接続する単一のリンクを定義します。 この要素は、`<Links></Links>` 要素の一覧内に表示されます。

  > [!NOTE]
  > この要素が未定義のノードを参照すると、マップ ドキュメントでは、指定された属性 (存在する場合) を含むノードが自動的に作成されます。

   この要素には、次の属性が必要です。

   `Source` - リンク元ノード。

   `Target` - リンク先ノード。

   追加できる属性 (省略可能) の一部を次に示します。

   `Label` - リンクの表示名。

   スタイル属性。 「 [DGML ファイルを編集してコード マップをカスタマイズする](../modeling/customize-code-maps-by-editing-the-dgml-files.md)」を参照してください。

   `Category` - この属性を共有する要素を識別するカテゴリの名前。 詳細については、`<Category/>` 要素を参照してください。

   `Property` - プロパティ値が同じ要素を識別するプロパティの名前。 詳細については、`<Property/>` 要素を参照してください。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Student" Category="Person" />
        <Node Id="Passenger" Label="Instructor" Category="Person" />
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
     </Nodes>
     <Links>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
        <Link Source="Driver" Target="Car" Label="Passed" Stroke="Black" Background="Green" Category="PassedTest" />
        <Link Source="Driver" Target="Truck" Label="Failed" Stroke="Black" Background="Red" Category="PassedTest" />
     </Links>
  </DirectedGraph>
  ```

- `<Categories></Categories>`

   この要素には、`<Category/>` 要素の一覧が含まれます。 詳細については、`<Category/>` 要素を参照してください。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Categories>
         <Category ... />
     </Categories>
  </DirectedGraph>
  ```

- `<Category/>`

   この要素は、この属性を共有する要素を識別するために使用される `Category` 属性を定義します。 `Category` 属性を使用すると、マップ要素の整理、継承による共有属性の提供、または追加のメタデータの定義が可能になります。

   この要素には、次の属性が必要です。

   `Id` - カテゴリの一意の名前。`Label` 属性が別途指定されていない場合は、`Label` 属性の既定値です。

   追加できる属性 (省略可能) の一部を次に示します。

   `Label` - カテゴリのわかりやすい名前。

   `BasedOn` - 現在の要素の `<Category/>` の継承元の親カテゴリ。

   この要素の例では、`FailedTest` カテゴリは、`Stroke` カテゴリから `PassedTest` 属性を継承します。 参照してください「階層構造カテゴリを作成するには" [DGML ファイルを編集してカスタマイズ コード マップを](../modeling/customize-code-maps-by-editing-the-dgml-files.md)します。

   カテゴリでは、マップに表示されるノードおよびリンクの外観を制御するいくつかの基本的なテンプレート動作も提供します。 「 [DGML ファイルを編集してコード マップをカスタマイズする](../modeling/customize-code-maps-by-editing-the-dgml-files.md)」を参照してください。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Driver" Category="Person" />
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
        <Node Id="Passenger" Category="Person" />
     </Nodes>
     <Links>
        <Link Source="Driver" Target="Car" Label="Passed" Category="PassedTest" />
        <Link Source="Driver" Target="Truck" Label="Failed" Category="FailedTest" />
     </Links>
     <Categories>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
        <Category Id="PassedTest" Label="Passed" Stroke="Black" Background="Green" />
        <Category Id="FailedTest" Label="Failed" BasedOn="PassedTest" Background="Red" />
     </Categories>
  </DirectedGraph>
  ```

- `<Properties></Properties>`

   この要素には、`<Property/>` 要素の一覧が含まれます。 詳細については、`<Property/>` 要素を参照してください。

   例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Properties>
         <Property ... />
     </Properties>
  </DirectedGraph>
  ```

- `<Property/>`

   この要素は、カテゴリおよびその他のプロパティを含む任意の DGML 要素または属性に値を代入する際に使用できる `Property` 属性を定義します。

   この要素には、次の属性が必要です。

  - `Id` - プロパティの一意の名前。`Label` 属性が別途指定されていない場合は、`Label` 属性の既定値です。

  - `DataType` - プロパティに格納されるデータの型。

    表示されるプロパティの場合、**プロパティ**ウィンドウで、使用、`Label`プロパティの表示名を指定するプロパティ。

    参照してください[コード要素およびリンクにカテゴリを割り当てる](../modeling/customize-code-maps-by-editing-the-dgml-files.md#AssignCategories)します。

    例:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <DirectedGraph Title="DrivingTest" xmlns="http://schemas.microsoft.com/vs/2009/dgml">
     <Nodes>
        <Node Id="Driver" Label="Driver" Category="Person" DrivingAge="18"/>
        <Node Id="Car" Label="Car" Category="Automobile" />
        <Node Id="Truck" Label="Truck" Category="Automobile" />
        <Node Id="Passenger" Category="Person" />
     </Nodes>
     <Links>
        <Link Source="Driver" Target="Car" Label="Passed" Category="PassedTest" />
        <Link Source="Driver" Target="Truck" Label="Failed" Category="FailedTest" />
     </Links>
     <Categories>
        <Category Id="Person" Background="Orange" />
        <Category Id="Automobile" Background="Yellow"/>
        <Category Id="PassedTest" Label="Passed" Stroke="Black" Background="Green" />
        <Category Id="FailedTest" Label="Failed" BasedOn="PassedTest" Background="Red" />
     </Categories>
     <Properties>
         <Property Id="DrivingAge" Label="Driving Age" DataType="System.Int32" />
     </Properties>
  </DirectedGraph>
  ```

### <a name="AddAlias"></a> 一般的に使用されるパスのエイリアス

よく使用されるパスをエイリアスに置き換えると、.dgml ファイルのサイズを小さくして、ファイルの読み込みまたは保存に必要な時間を短縮することができます。 エイリアスを作成するには、.dgml ファイルの末尾に `<Paths></Paths>` セクションを追加します。 このセクションには、パスのエイリアスを定義する `<Path/>` 要素を追加します。

```xml
<Paths>
   <Path Id="MyPathAlias" Value="C:\...\..." />
</Paths>
```

.Dgml ファイル内の要素からエイリアスを参照するには、囲む、`Id`の\<パス/> 要素はドル記号 ($) と括弧 (())。

```xml
<Nodes>
   <Node Id="MyNode" Reference="$(MyPathAlias)MyDocument.txt" />
</Nodes>
<Properties>
   <Property Id="Reference" Label="My Document" DataType="System.String" IsReference="True" />
</Properties>
```

## <a name="see-also"></a>関連項目

- [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)
- [コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)
- [コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)