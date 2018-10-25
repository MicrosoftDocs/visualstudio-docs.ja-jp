---
title: DGML ファイルを編集してコード マップをカスタマイズ |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- dependency graphs, creating path aliases
- dependency graphs, linking items to nodes
- graph documents, creating path aliases
- dependency graphs, grouping nodes
- graph documents, editing
- graph documents, linking items to nodes
- graph documents, customizing
- graph documentings, assigning categories and properties
- dependency graphs, editing
- dependency graphs, customizing
- graph documents, grouping nodes
- dependency graphs, assigning categories and properties
ms.assetid: a2e141f4-4fd8-4611-b236-6b9e7bc54fc1
caps.latest.revision: 93
author: alexhomer1
ms.author: gewarren
manager: douge
ms.openlocfilehash: cc6ef0463f98b5aec938ff7748a64b34b32c3934
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49843835"
---
# <a name="customize-code-maps-by-editing-the-dgml-files"></a>DGML ファイルを編集してコード マップをカスタマイズする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード マップをカスタマイズするには、マップの Directed Graph Markup Language (.dgml) ファイルを編集できます。 たとえば、要素を編集してカスタム スタイルを指定したり、コード要素とリンクにプロパティおよびカテゴリを割り当てたり、コード要素やリンクにドキュメントや URL をリンクしたりすることができます。 DGML 要素の詳細については、次を参照してください。 [Directed Graph Markup Language (DGML) リファレンス](../modeling/directed-graph-markup-language-dgml-reference.md)します。  
  
 テキスト エディターまたは XML エディターで、コード マップの .dgml ファイルを編集します。 マップが Visual Studio ソリューションの一部である場合でを選択します。**ソリューション エクスプ ローラー**、ショートカット メニューを開き、選択**ファイルを開く**、 **XML (テキスト) エディター**します。  
  
> [!NOTE]
>  コード マップを作成するには、Visual Studio Enterprise が必要です。 Visual Studio でコード マップを編集する場合、.dgml ファイルを保存すると、未使用の DGML 要素および属性が削除されクリーンアップされます。 また、新しいリンクを手動で追加すると、コード要素が自動的に作成されます。 .dgml ファイルを保存すると、要素に追加した属性によって、自身がアルファベット順に並べ替えられる場合があります。  
  
##  <a name="OrganizeNodes"></a> コード要素をグループ化  
 新しいグループを追加したり、既存のノードをグループに変換したりすることができます。  
  
1. テキスト エディターまたは XML エディターで、.dgml ファイルを開きます。  
  
2. コード要素をグループに変換するには、そのコード要素の `<Node/>` 要素を見つけます。  
  
    \- または -  
  
    新しいグループを追加するには、`<Nodes>` セクションを見つけます。 新しい `<Node/>` 要素を追加します。  
  
3. `<Node/>` 要素に、`Group` 属性を追加して、グループを展開した状態で表示するか、折りたたんだ状態で表示するかを指定します。 例:  
  
   ```xml  
   <Nodes>  
      <Node Id="MyFirstGroup" Group="Expanded" />  
      <Node Id="MySecondGroup" Group="Collapsed" />  
   </Nodes>  
   ```  
  
4. `<Links>` セクションで、次の属性を持つ `<Link/>` 要素が、グループ コード要素とその子コード要素の間のリレーションシップごとに存在することを確認します。  
  
   - グループ コード要素を指定する `Source` 属性  
  
   - 子コード要素を指定する `Target` 属性  
  
   - グループ コード要素とその子コード要素との間の `Category` リレーションシップを指定する `Contains` 属性  
  
     例えば:  
  
   ```xml  
   <Links>  
      <Link Category="Contains" Source="MyFirstNewGroup" Target="FirstGroupChildOne" />  
      <Link Category ="Contains" Source="MyFirstNewGroup" Target="FirstGroupChildTwo" />  
      <Link Category ="Contains" Source="MySecondNewGroup" Target="SecondGroupChildOne" />  
      <Link Category="Contains" Source="MySecondNewGroup" Target="SecondGroupChildTwo" />  
   </Links>  
   ```  
  
    詳細については、`Category`属性は、「[コード要素およびリンクにカテゴリを割り当てる](#AssignCategories)します。  
  
##  <a name="ChangeGraphStyle"></a> マップのスタイルを変更します。  
 マップの .dgml ファイルを編集することで、マップの背景色および境界線の色を変更できます。 コード要素およびリンクのスタイルを変更するを参照してください。[コード要素およびリンクのスタイルを変更する](#Highlight)します。  
  
1.  テキスト エディターまたは XML エディターで、.dgml ファイルを開きます。  
  
2.  `<DirectedGraph>` 要素に次の任意の属性を追加して、グラフのスタイルを変更します。  
  
     背景色  
  
    ```xml  
    Background="ColorNameOrHexadecimalValue"  
    ```  
  
     境界線の色  
  
    ```xml  
    Stroke="StrokeValue"  
    ```  
  
     例えば:  
  
    ```xml  
    <DirectedGraph Background="Green" xmlns="http://schemas.microsoft.com/vs/2009/dgml" >  
       ...  
       ...  
    </DirectedGraph>  
    ```  
  
##  <a name="Highlight"></a> コード要素およびリンクのスタイルを変更します。  
  
###  <a name="CreateCustomStyles"></a>   
 次のコード要素にカスタム スタイルを適用できます。  
  
-   単一のコード要素およびリンク  
  
-   コード要素およびリンクのグループ  
  
-   特定の条件に基づくコード要素およびリンクのグループ  
  
> [!TIP]
>  多くのコード要素またはリンクで繰り返し使用するスタイルがある場合は、これらのコード要素またはリンクにカテゴリを適用し、そのカテゴリにスタイルを適用することも検討できます。 詳細については、次を参照してください。[コード要素およびリンクにカテゴリを割り当てる](#AssignCategories)と[コード要素およびリンク プロパティを割り当てる](#AssignProperties)します。  
  
##### <a name="to-apply-a-custom-style-to-a-single-code-element"></a>単一のコード要素にカスタム スタイルを適用するには  
  
1.  テキスト エディターまたは XML エディターで、.dgml ファイルを開きます。  
  
2.  コード要素の `<Node/>` 要素を見つけます。 次の属性のいずれかを追加して、そのスタイルをカスタマイズします。  
  
     背景色  
  
    ```xml  
    Background="ColorNameOrHexadecimalValue"  
    ```  
  
     アウトライン  
  
    ```xml  
    Stroke="ColorNameOrHexadecimalValue"  
    ```  
  
     外枠の太さ  
  
    ```xml  
    StrokeThickness="StrokeValue"  
    ```  
  
     テキストの色  
  
    ```xml  
    Foreground="ColorNameOrHexadecimalValue"  
    ```  
  
     アイコン  
  
    ```xml  
    Icon="IconFilePathLocation"  
    ```  
  
     テキストのサイズ  
  
    ```xml  
    FontSize="FontSizeValue"  
    ```  
  
     テキストの種類  
  
    ```xml  
    FontFamily="FontFamilyName"  
    ```  
  
     テキストの太さ  
  
    ```xml  
    FontWeight="FontWeightValue"  
    ```  
  
     テキストのスタイル  
  
    ```xml  
    FontStyle="FontStyleName"  
    ```  
  
     たとえば、テキストのスタイルとして `Italic` を指定できます。  
  
     テクスチャ  
  
    ```xml  
    Style="Glass"  
    ```  
  
     - または  
  
    ```xml  
    Style="Plain"  
    ```  
  
     形式  
  
     シェイプをアイコンに置き換えるには、`Shape` プロパティを `None` に設定し、`Icon` プロパティをアイコン ファイルがあるパスに設定します。  
  
    ```xml  
    Shape="ShapeFilePathLocation"  
    ```  
  
     例:  
  
    ```xml  
    <Nodes>  
       <Node Id="MyNode" Background="#FF008000" Stroke="#FF000000"  
       Foreground="#FFFFFFFF" Icon="...\Icons\Globe.png"/>  
    </Nodes>  
    ```  
  
##### <a name="to-apply-a-custom-style-to-a-single-link"></a>単一のリンクにカスタム スタイルを適用するには  
  
1.  テキスト エディターまたは XML エディターで、.dgml ファイルを開きます。  
  
2.  ソース コード要素とターゲット コード要素の両方の名前を含む `<Link/>` 要素を探します。  
  
3.  `<Link/>` 要素に次の属性を追加して、スタイルをカスタマイズします。  
  
     外枠と矢じりの色  
  
    ```xml  
    Stroke="ColorNameOrHexadecimalValue"  
    ```  
  
     外枠の太さ  
  
    ```xml  
    StrokeThickness="StrokeValue"  
    ```  
  
     外枠のスタイル  
  
    ```xml  
    StrokeDashArray="StrokeArrayValues"  
    ```  
  
     例:  
  
    ```xml  
    <Links>  
       <Link Source="MyFirstNode" Target="MySecondNode" Background="Green" Stroke="#FF000000" StrokeDashArray="2,2"/>  
    </Links>  
    ```  
  
##### <a name="to-apply-custom-styles-to-a-group-of-code-elements-or-links"></a>コード要素またはリンクのグループにカスタム スタイルを適用するには  
  
1. テキスト エディターまたは XML エディターで、.dgml ファイルを開きます。  
  
2. `<Styles></Styles>` 要素が存在しない場合、`<DirectedGraph></DirectedGraph>` 要素の後の `<Links></Links>` 要素の下位に、この要素を追加します。  
  
3. `<Styles></Styles>` 要素で、`<Style/>` 要素の下位に次の属性を指定します。  
  
   - `TargetType="Node` &#124; `Link | Graph"`  
  
   - `GroupLabel="` *NameInLegendBox* `"`  
  
   - `ValueLabel="` *NameInStylePickerBox* `"`  
  
     全種類の対象にカスタム スタイルを適用する場合、条件は使用しません。  
  
##### <a name="to-apply-a-conditional-style-to-groups-of-code-elements-or-links"></a>コード要素またはリンクのグループに条件付きスタイルを適用するには  
  
1. テキスト エディターまたは XML エディターで、.dgml ファイルを開きます。  
  
2. `<Style/>` 要素に、`<Condition/>` 属性を含む `Expression` 要素を追加して、ブール値を返す式を指定します。  
  
    例えば:  
  
   ```xml  
   <Condition Expression="MyCategory"/>  
   ```  
  
    - または  
  
   ```xml  
   <Condition Expression="MyCategory > 100"/>  
   ```  
  
    - または  
  
   ```xml  
   <Condition Expression="HasCategory('MyCategory')"/>  
   ```  
  
    この式では、次のバッカス・ナウア記法 (BNF: Backus-Naur Form) 構文を使用します。  
  
    <Expression> ::= <BinaryExpression> &#124; <UnaryExpression> &#124; "("<Expression>")" &#124; <MemberBindings> &#124; <Literal> &#124; <Number>  
  
    <BinaryExpression> ::= <Expression> <Operator> <Expression>  
  
    <UnaryExpression> ::= "!" <Expression> &#124; "+" <Expression> &#124; "-" <Expression>  
  
    <Operator> ::= "<" &#124; "\<=" &#124; "=" &#124; ">=" &#124; ">" &#124; "!=" &#124; "or" &#124; "and" &#124; "+" &#124; "*" &#124; "/" &#124; "-"  
  
    <MemberBindings> ::= <MemberBindings> &#124; <MemberBinding> "." <MemberBinding>  
  
    <MemberBinding> ::= <MethodCall> &#124; <PropertyGet>  
  
    <MethodCall> ::= <Identifier> "(" <MethodArgs> ")"  
  
    <PropertyGet> : = 識別子  
  
    <MethodArgs> ::= <Expression> &#124; <Expression> "," <MethodArgs> &#124; <empty>  
  
    <Identifier> ::= [^. ]*  
  
    <Literal> : = 一重または二重引用符で囲まれた文字列リテラル  
  
    <Number> 省略可能な小数点 10 進数字の文字列を =  
  
    複数を指定した`<Condition/>`要素で、すべて必要があります、スタイルを適用する場合は true。  
  
3. `<Condition/>` 要素の次の行に、1 つ以上の `<Setter/>` 要素を追加して、条件を満たすマップ、コード要素、またはリンクに適用する `Property` 属性と、固定の `Value` 属性または計算される `Expression` 属性を指定します。  
  
    例:  
  
   ```xml  
   <Setter Property="BackGround" Value="Green"/>  
   ```  
  
   以下に簡単な完成例を示します。この例の条件では、コード要素の `Passed` カテゴリが `True` と `False` のどちらに設定されているかに基づいてコード要素が緑色または赤色で表示されるように指定しています。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DirectedGraph xmlns="http://schemas.microsoft.com/vs/2009/dgml">  
   <Nodes>  
      <Node Id="MyFirstNode" Passed="True" />  
      <Node Id="MySecondNode" Passed="False" />  
   </Nodes>  
   <Links>  
   </Links>  
   <Styles>  
      <Style TargetType="Node" GroupLabel="Passed" ValueLabel="True">  
         <Condition Expression="Passed='True'"/>  
         <Setter Property="Background" Value="Green"/>  
      </Style>  
      <Style TargetType="Node" GroupLabel="Passed" ValueLabel="False">  
         <Condition Expression="Passed='False'"/>  
         <Setter Property="Background" Value="Red"/>  
      </Style>  
   </Styles>  
</DirectedGraph>  
```  
  
 次の表に、実際に使用できる条件例をいくつか示します。  
  
 フォント サイズをコードの行数の関数として設定する。それによってコード要素のサイズも変更されます。 この例では、単一の条件式を使用して、複数のプロパティ (`FontSize` および `FontFamily`) を設定しています。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DirectedGraph xmlns="http://schemas.microsoft.com/vs/2009/dgml">  
<Nodes>  
   <Node Id="Class1" LinesOfCode ="200" />  
   <Node Id="Class2" LinesOfCode ="1000" />  
   <Node Id="Class3" LinesOfCode ="20" />  
</Nodes>  
<Properties>  
   <Property Id="LinesOfCode" Label="LinesOfCode" Description="LinesOfCode" DataType="System.Int32" />  
</Properties>  
<Styles>  
   <Style TargetType="Node" GroupLabel="LinesOfCode" ValueLabel="Function">  
      <Condition Expression="LinesOfCode > 0" />  
      <Setter Property="FontSize" Expression="Math.Max(9,Math.Sqrt(LinesOfCode))" />  
      <Setter Property="FontFamily" Value="Papyrus" />  
   </Style>  
</Styles>  
</DirectedGraph>  
```  
  
 `Coverage` プロパティに基づいて、コード要素の背景色を設定する。 スタイルは、`if-else` ステートメントと同様に、出現する順番で評価されます。  
  
 この例では、次のように記述されています。  
  
1.  `Coverage`&gt; 80 の場合、`Background` プロパティを緑色に設定します。  
  
2.  `Coverage`&gt; 50 の場合、`Background` プロパティの値に基づいて、`Coverage` プロパティをオレンジ色の網かけに設定します。  
  
3.  それ以外の場合、`Background` プロパティの値に基づいて、`Coverage` プロパティを赤色の網かけに設定します。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DirectedGraph xmlns="http://schemas.microsoft.com/vs/2009/dgml">  
<Nodes>  
   <Node Id="Class1" Coverage="58" />  
   <Node Id="Class2" Coverage="95" />  
   <Node Id="Class3" Coverage="32" />  
</Nodes>  
<Properties>  
   <Property Id="Coverage" Label="Coverage" Description="Code coverage as a percentage of blocks" DataType="Double" />  
</Properties>  
<Styles>  
   <Style TargetType="Node" GroupLabel="Coverage" ValueLabel="Good">  
      <Condition Expression="Coverage > 80" />  
      <Setter Property="Background" Value="Green" />  
   </Style>  
   <Style TargetType="Node" GroupLabel="Coverage" ValueLabel="OK">  
      <Condition Expression="Coverage > 50" />  
      <Setter Property="Background" Expression="Color.FromRgb(180 * Math.Max(1, (80 - Coverage) / 30), 180, 0)" />  
   </Style>  
   <Style TargetType="Node" GroupLabel="Coverage" ValueLabel="Bad">  
      <Setter Property="Background" Expression="Color.FromRgb(180, 180 * Coverage / 50, 0)" />  
   </Style>  
</Styles>  
</DirectedGraph>  
```  
  
 `Shape` プロパティを `None` に設定して、図形をアイコンで置き換える。 `Icon` プロパティを使用して、アイコンの場所を指定します。  
  
```xml  
<DirectedGraph xmlns="http://schemas.microsoft.com/vs/2009/dgml">  
<Nodes>  
   <Node Id="Automation" Category="Test" Label="Automation" />  
   <Node Id="C# Provider" Category="Provider" Label="C# Provider" />  
</Nodes>  
<Categories>  
   <Category Id="Provider" Icon="...\Icons\Module.png" Shape="None" />  
   <Category Id="Test" Icon="...\Icons\Page.png" Shape="None" />  
</Categories>  
<Properties>  
   <Property Id="Icon" DataType="System.String" />  
   <Property Id="Label" Label="Label" Description="Displayable label of an Annotatable object" DataType="System.String" />  
   <Property Id="Shape" DataType="System.String" />  
</Properties>  
<Styles>  
   <Style TargetType="Node" GroupLabel="Group" ValueLabel="Has category">  
      <Condition Expression="HasCategory('Group')" />  
      <Setter Property="Background" Value="#80008080" />  
   </Style>  
   <Style TargetType="Node">  
      <Setter Property="HorizontalAlignment" Value="Center" />  
   </Style>  
</Styles>  
</DirectedGraph>  
```  
  
##  <a name="AssignProperties"></a> コード要素およびリンクにプロパティを割り当てる  
 コード要素およびリンクにプロパティを割り当てることで、コード要素およびリンクを編成できます。 たとえば、特定のプロパティを持つコード要素を選択して、それらのグループ化、スタイルの変更、または非表示化を実行できます。  
  
#### <a name="to-assign-a-property-to-a-code-element"></a>コード要素にプロパティを割り当てるには  
  
1.  テキスト エディターまたは XML エディターで、.dgml ファイルを開きます。  
  
2.  そのコード要素の `<Node/>` 要素を見つけます。 プロパティの名前とその値を指定します。 例:  
  
    ```xml  
    <Nodes>  
       <Node Id="MyNode" MyPropertyName="PropertyValue" />  
    </Nodes>  
    ```  
  
3.  `<Property/>` 要素を `<Properties>` セクションに追加して、属性 (要素の表示名、データ型など) を指定します。  
  
    ```xml  
    <Properties>  
       <Property Id="MyPropertyName" Label="My Property" DataType="System.DataType"/>  
    </Properties>  
    ```  
  
#### <a name="to-assign-a-property-to-a-link"></a>リンクにプロパティを割り当てるには  
  
1.  テキスト エディターまたは XML エディターで、.dgml ファイルを開きます。  
  
2.  ソース コード要素とターゲット コード要素の両方の名前を含む `<Link/>` 要素を探します。  
  
3.  `<Node/>` 要素で、プロパティの名前とその値を指定します。 例:  
  
    ```xml  
    <Links>  
       <Link Source="MyFirstNode" Target="MySecondNode" MyPropertyName="PropertyValue" />  
    </Links>  
    ```  
  
4.  `<Property/>` 要素を `<Properties>` セクションに追加して、属性 (要素の表示名、データ型など) を指定します。  
  
    ```xml  
    <Properties>  
       <Property Id="MyPropertyName" Label="My Property Name" DataType="System.DataType"/>  
    </Properties>  
    ```  
  
##  <a name="AssignCategories"></a> コード要素およびリンクにカテゴリを割り当てる  
 次のセクションでは、コード要素にカテゴリを割り当てることでコード要素を整理する方法と、コード要素を編成したり子カテゴリに属性を追加したりするのに役立つ階層カテゴリを継承を使用して作成する方法について説明します。  
  
#### <a name="to-assign-a-category-to-a-code-element"></a>コード要素にカテゴリを割り当てるには  
  
-   テキスト エディターまたは XML エディターで、.dgml ファイルを開きます。  
  
-   目的のコード要素の `<Node/>` 要素を見つけます。  
  
-   `<Node/>` 要素に `Category` 属性を追加して、カテゴリの名前を指定します。 例:  
  
    ```xml  
    <Nodes>  
       <Node Id="MyNode" Category="MyCategory" />  
    </Nodes>  
    ```  
  
     `<Category/>` セクションに `<Categories>` 要素を追加することで、`Label` 属性を使用してそのカテゴリの表示テキストを指定できます。  
  
    ```xml  
    <Categories>  
       <Category Id="MyCategory" Label="My Category" />  
    </Categories>  
    ```  
  
#### <a name="to-assign-a-category-to-a-link"></a>リンクにカテゴリを割り当てるには  
  
1.  テキスト エディターまたは XML エディターで、.dgml ファイルを開きます。  
  
2.  ソース コード要素とターゲット コード要素の両方の名前を含む `<Link/>` 要素を探します。  
  
3.  `<Link/>` 要素に `Category` 属性を追加して、カテゴリの名前を指定します。 例:  
  
    ```xml  
    <Links>  
       <Link Source="MyFirstNode" Target="MySecondNode" Category="MyCategory"  
    </Links>  
    ```  
  
4.  `<Category/>` セクションに `<Categories>` 要素を追加することで、`Label` 属性を使用してそのカテゴリの表示テキストを指定できます。  
  
    ```xml  
    <Categories>  
       <Category Id="MyCategory" Label="My Category" />  
    </Categories>  
    ```  
  
#### <a name="to-create-hierarchical-categories"></a>階層構造のカテゴリを作成するには  
  
1.  テキスト エディターまたは XML エディターで、.dgml ファイルを開きます。  
  
2.  親カテゴリを示す `<Category/>` 要素を追加し、次に子カテゴリの `BasedOn` 要素に `<Category/>` 属性を追加します。  
  
     例:  
  
    ```xml  
    <Nodes>  
       <Node Id="MyFirstNode" Label="My First Node" Category= "MyCategory" />  
       <Node Id="MySecondNode" Label="My Second Node" />  
    </Nodes>  
    <Links>  
       <Link Source="MyFirstNode" Target="MySecondNode" />  
    </Links>  
    <Categories>  
       <Category Id="MyCategory" Label="My Category" BasedOn="MyParentCategory"/>  
       <Category Id="MyParentCategory" Label="My Parent Category" Background="Green"/>  
    </Categories>  
    ```  
  
     この例では、`MyFirstNode` の背景は緑色になります。これは、その `Category` 属性が `Background` の `MyParentCategory` 属性を継承するためです。  
  
##  <a name="AddReferences"></a> コード要素およびリンクにドキュメントまたは Url をリンクします。  
 マップの .dgml ファイルを編集したり `Reference` 属性をコード要素の `<Node/>` 要素またはリンクの `<Link/>` 要素に追加することで、ドキュメントまたは URL をコード要素またはリンクに対してリンク付けできます。 これで、そのコンテンツをコード要素またはリンクから開いて参照できるようになります。 `Reference` 属性では、そのコンテンツのパスを指定します。 これには、.dgml ファイルの場所に対する相対パス、または絶対パスを使用できます。  
  
> [!CAUTION]
>  相対パスを使用し、.dgml ファイルが別の位置に移動された場合、それらのパスは解決しません。 リンクされたコンテンツを開いて参照しようとした場合、コンテンツを表示できないことを示すエラーが発生します。  
  
 たとえば、次のコード要素をリンクできます。  
  
-   クラスに対する変更を示すために、クラスを示すコード要素に、作業コード要素、ドキュメント、または別の .dgml ファイルの URL をリンクすることができます。  
  
-   ソフトウェアの論理アーキテクチャのレイヤーを表すグループ コード要素にレイヤー図をリンクすることもできます。  
  
-   インターフェイスを公開するコンポーネントに関する詳細情報を表示するために、そのインターフェイスを示すコード要素にコンポーネント図をリンクすることができます。  
  
-   コード要素を Team Foundation Server 作業項目やバグ、またはコード要素に関連するその他の情報にリンクします。  
  
#### <a name="to-link-a-document-or-url-to-a-code-element"></a>ドキュメントまたは URL をコード要素にリンクするには  
  
1. テキスト エディターまたは XML エディターで、.dgml ファイルを開きます。  
  
2. 目的のコード要素の `<Node/>` 要素を見つけます。  
  
3. 次の表にあるタスクのいずれかを実行します。  
  
    単一のコード要素  
  
   - `<Node/>` 要素または `<Link/>` 要素で、`Reference` 属性を追加してコード要素の場所を指定します。  
  
     > [!NOTE]
     >  1 つの要素に対して 1 つの `Reference` 属性のみを使用できます。  
  
     例:  
  
   ```xml  
   <Nodes>  
      <Node Id="MyNode" Reference="MyDocument.txt" />  
   </Nodes>  
   <Properties>  
      <Property Id="Reference" Label="My Document" DataType="System.String" IsReference="True" />  
   </Properties>  
   ```  
  
    複数のコード要素  
  
   1. `<Node/>` 要素または `<Link/>` 要素で、各参照の場所を指定する新しい属性を追加します。  
  
   2. `<Properties>` セクションで、次の操作を行います。  
  
      1.  新しい種類の参照ごとに `<Property/>` 要素を追加します。  
  
      2.  新しい参照属性の名前に `Id` 属性を設定します。  
  
      3.  追加、`IsReference`属性およびに設定`True`コード要素の上に表示される参照**参照へジャンプ**ショートカット メニュー。  
  
      4.  使用して、`Label`でコード要素の表示テキストを指定する属性**参照へジャンプ**ショートカット メニュー。  
  
      例えば:  
  
   ```xml  
   <Nodes>  
      <Node Id="MyNode" SequenceDiagram="MySequenceDiagram.sequencediagram" ActiveBugs="MyActiveBugs.wiq"/>  
   </Nodes>  
   <Properties>  
      <Property Id="SequenceDiagram" Label="My Sequence Diagram" DataType="System.String" IsReference="True" />  
      <Property Id="ActiveBugs" Label="Active Bugs" DataType="System.String" IsReference="True" />  
   </Properties>  
   ```  
  
    マップでは、コード要素の名前は下線付きで表示されます。 コード要素またはリンクのショートカット メニューを開くと表示されます、**参照へジャンプ**ショートカット メニューを選択するためのリンクされたコード要素を格納します。  
  
4. 参照で文字列を繰り返し使用する代わりに、`ReferenceTemplate` 属性を使用して、複数の参照で使用する共通の文字列 (URL など) を指定します。  
  
    `ReferenceTemplate` 属性では、参照の値のプレースホルダーを指定します。 次の例では、`{0}` 属性の `ReferenceTemplate` プレースホルダーは、 `MyFirstReference` 要素の `MySecondReference` 属性と `<Node/>` 属性の値に置換され、完全なパスが生成されます。  
  
   ```xml  
   <Nodes>  
      <Node Id="MyNode" MyFirstReference="MyFirstDocument" MySecondReference="MySecondDocument"/>  
      <Node Id="MySecondNode" MyFirstReference="AnotherFirstDocument" MySecondReference="AnotherSecondDocument"/>  
   </Nodes>  
   <Properties>  
      <Property Id="MyFirstReference" Label="My First Document" DataType="System.String" IsReference="True" ReferenceTemplate="http://www.Fabrikam.com/FirstDocuments/{0}.asp"/>  
      <Property Id="MySecondReference" Label="My Second Document" DataType="System.String" IsReference="True" ReferenceTemplate=" http://www.Fabrikam.com/SecondDocuments/{0}.asp"/>  
   </Properties>  
   ```  
  
5. マップから参照先のコード要素を表示するには、コード要素またはリンクのショートカット メニューを開きます。 選択**参照へジャンプ**とからコード要素。  
  
## <a name="see-also"></a>関連項目  
 [ソリューション間の依存関係をマップします。](../modeling/map-dependencies-across-your-solutions.md)   
 [アプリケーションをデバッグするコード マップの使用](../modeling/use-code-maps-to-debug-your-applications.md)   
 [コード マップ アナライザーを使った潜在的な問題を検索します。](../modeling/find-potential-problems-using-code-map-analyzers.md)   
 [参照およびコード マップを再配置](../modeling/browse-and-rearrange-code-maps.md)   
 [Directed Graph Markup Language (DGML) リファレンス](../modeling/directed-graph-markup-language-dgml-reference.md)