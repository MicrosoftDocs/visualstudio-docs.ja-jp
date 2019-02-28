---
title: MSBuild 項目 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
helpviewer_keywords:
- MSBuild, Items
ms.assetid: d762eff4-c92a-4b5f-a944-1ca30aa22319
caps.latest.revision: 38
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 24756553f4b1f5eb1a0ce811842c2843debd71aa
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54770851"
---
# <a name="msbuild-items"></a>MSBuild 項目
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
MSBuild 項目はビルド システムへの入力であり、通常はファイルを表します。 項目は要素名に基づいてアイテムの種類にグループ化されます。 項目の種類は項目の名前付きリストであり、タスクのパラメーターとして使用できます。 タスクは項目値を使用して、ビルド処理のステップを実行します。  
  
 項目名はそれぞれが属するアイテムの種類によって指定されるため、「項目」と「項目値」という用語は同義です。  
  
 **このトピックの内容**  
  
-   [プロジェクト ファイルで項目を作成する](#BKMK_Creating1)  
  
-   [実行時に項目を作成する](#BKMK_Creating2)  
  
-   [プロジェクト ファイルの項目を参照する](#BKMK_ReferencingItems)  
  
-   [ワイルドカードを使用して項目を指定する](#BKMK_Wildcards)  
  
-   [Exclude 属性を使用する](#BKMK_ExcludeAttribute)  
  
-   [項目メタデータ](#BKMK_ItemMetadata)  
  
    -   [プロジェクト ファイルで項目メタデータを参照する](#BKMK_ReferencingItemMetadata)  
  
    -   [既知の項目メタデータ](#BKMK_WellKnownItemMetadata)  
  
    -   [メタデータを使用してアイテムの種類を変換する](#BKMK_Transforming)  
  
-   [項目定義](#BKMK_ItemDefinitions)  
  
-   [Target の ItemGroup の項目の属性](#BKMK_AttributesWithinTargets)  
  
    -   [Remove 属性](#BKMK_RemoveAttribute)  
  
    -   [KeepMetadata 属性](#BKMK_KeepMetadata)  
  
    -   [RemoveMetadata 属性](#BKMK_RemoveMetadata)  
  
    -   [KeepDuplicates 属性](#BKMK_KeepDuplicates)  
  
##  <a name="BKMK_Creating1"></a> プロジェクト ファイルに項目を作成する  
 プロジェクト ファイル内で、[ItemGroup](../msbuild/itemgroup-element-msbuild.md) 要素の子要素として項目を宣言します。 子要素の名前は、アイテムの種類です。 要素の `Include` 属性は、そのアイテムの種類に組み込まれる項目 (ファイル) を指定します。 たとえば、次の XML では、`Compile` という名前のアイテムの種類を作成し、2 つのファイルを含めています。  
  
```  
<ItemGroup>  
    <Compile Include = "file1.cs"/>  
    <Compile Include = "file2.cs"/>  
</ItemGroup>  
```  
  
 項目 "file2.cs" は項目 "file1.cs" に取って代わるのではなく、このファイル名がアイテムの種類 `Compile` の値のリストに付加されます。 ビルドの評価フェーズでアイテムの種類から項目を削除することはできません。  
  
 次の XML では、両方のファイルを 1 つの `Include` 属性で宣言することで、同じアイテムの種類を作成しています。 ファイル名はセミコロンで区切られます。  
  
```  
<ItemGroup>  
    <Compile Include = "file1.cs;file2.cs"/>  
</ItemGroup>  
```  
  
##  <a name="BKMK_Creating2"></a> 実行時に項目を作成する  
 [Target](../msbuild/target-element-msbuild.md) 要素の外側にある項目には、ビルドの評価フェーズで値が割り当てられます。 その後の実行フェーズで、次のようにして項目を作成または変更できます。  
  
-   どのタスクも項目を生成できます。 項目を生成するには、[Task](../msbuild/task-element-msbuild.md) 要素の子要素として、`ItemName` 属性を持つ [Output](../msbuild/output-element-msbuild.md) 要素が必要です。  
  
-   [CreateItem](../msbuild/createitem-task.md) タスクは、項目を生成できます。 この使用法は非推奨とされます。  
  
-   .NET Framework 3.5 以降では、項目要素を格納できる [ItemGroup](../msbuild/itemgroup-element-msbuild.md) 要素を `Target` 要素に含めることができます。  
  
##  <a name="BKMK_ReferencingItems"></a> プロジェクト ファイルの項目を参照する  
 プロジェクト ファイルでアイテムの種類を参照するには、構文 @(`ItemType`) を使用します。 たとえば、前の例に挙げたアイテムの種類を参照するには、`@(Compile)` を使用します。 この構文を使用してアイテムの種類をタスクのパラメーターとして指定すれば、項目をそのタスクに渡すことができます。 詳細については、「[方法: ビルドするファイルを選択する](../msbuild/how-to-select-the-files-to-build.md)」を参照してください。  
  
 既定では、アイテムの種類の項目は、それが展開されるときにセミコロン (;) によって区切られます。 構文 @(*ItemType*, '*separator*') を使用して、既定以外の区切り記号を指定できます。 詳細については、「[方法: 項目リストをコンマ区切りで表示する](../msbuild/how-to-display-an-item-list-separated-with-commas.md)」を参照してください。  
  
##  <a name="BKMK_Wildcards"></a> ワイルドカードを使用して項目を指定する  
 **、\*、および ? をワイルドカード文字として使用して、各ファイルを個別にリストする代わりに、ファイルのグループをビルドの入力として指定できます。  
  
- ? ワイルドカード文字は単一の文字と一致します。  
  
- \* ワイルドカード文字は 0 個以上の文字と一致します。  
  
- \*\* ワイルドカード文字のシーケンスはパスの一部と一致します。  
  
  たとえば、プロジェクト ファイルで次の要素を使用して、プロジェクト ファイルが格納されているディレクトリ内のすべての .cs ファイルを指定できます。  
  
```  
<CSFile Include="*.cs"/>  
```  
  
 次の要素は D: ドライブのすべての .vb ファイルを選択します。  
  
```  
<VBFile Include="D:/**/*.vb"/>  
```  
  
 ワイルドカード文字の詳細については、「[方法: ビルドするファイルを選択する](../msbuild/how-to-select-the-files-to-build.md)」を参照してください。  
  
##  <a name="BKMK_ExcludeAttribute"></a> Exclude 属性を使用する  
 項目の要素には `Exclude` 属性を含めることができます。この属性は、アイテムの種類から特定の項目 (ファイル) を除外します。 `Exclude` 属性は通常、ワイルドカード文字と一緒に使用されます。 たとえば、次の XML は、`DoNotBuild.cs` ファイルを除き、ディレクトリのすべての .cs ファイルをアイテムの種類 CSFile に追加します。  
  
```  
<ItemGroup>  
    <CSFile  Include="*.cs"  Exclude="DoNotBuild.cs"/>  
</ItemGroup>  
```  
  
 `Exclude` 属性は、同一の項目要素内にある `Include` 属性によって追加された項目のみに作用します。 次の例では、Form1.cs ファイルは前の項目要素で追加されているため、除外されません。  
  
```  
<Compile Include="*.cs" />  
<Compile Include="*.res" Exclude="Form1.cs">  
```  
  
 詳細については、「[方法: ビルドからファイルを除外する](../msbuild/how-to-exclude-files-from-the-build.md)」を参照してください。  
  
##  <a name="BKMK_ItemMetadata"></a> 項目メタデータ  
 項目には、`Include` および `Exclude` 属性の情報に加えて、メタデータを含めることができます。 このメタデータは、項目に関する詳細情報を必要とするタスクで使用できます。あるいは、タスクとターゲットをバッチ処理するために使用できます。 詳細については、「[MSBuild バッチ](../msbuild/msbuild-batching.md)」をご覧ください。  
  
 メタデータは、項目の要素の子要素としてプロジェクト ファイルで宣言されているキーと値のペアのコレクションです。 子要素の名前はメタデータの名前であり、子要素の値はメタデータの値です。  
  
 メタデータは、それが含まれる項目要素に関連付けられています。 たとえば、次の XML は、値 `Fr` を持つ `Culture` メタデータを、アイテムの種類 CSFile の "one.cs" と "two.cs" の両方の項目に追加します。  
  
```  
<ItemGroup>  
    <CSFile Include="one.cs;two.cs">  
        <Culture>Fr</Culture>  
    </CSFile>  
</ItemGroup>  
```  
  
 項目には 0 以上のメタデータ値を指定できます。 メタデータの値は、いつでも変更できます。 メタデータを空の値に設定すると、実質的にはビルドからメタデータが削除されます。  
  
###  <a name="BKMK_ReferencingItemMetadata"></a> プロジェクト ファイルで項目メタデータを参照する  
 プロジェクト ファイルで項目のメタデータを参照するには、%(`ItemMetadataName`) という構文を使用します。 あいまいさが存在する場合は、アイテムの種類の名前を使用して参照を修飾できます。 たとえば、%(*ItemType.ItemMetaDataName*) と指定できます。次の例では、Display メタデータを使用して Message タスクをバッチ処理します。 バッチ処理のために項目のメタデータを使用する方法の詳細については、「[タスクのバッチの項目メタデータ](../msbuild/item-metadata-in-task-batching.md)」を参照してください。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <Stuff Include="One.cs" >  
            <Display>false</Display>  
        </Stuff>  
        <Stuff Include="Two.cs">  
            <Display>true</Display>  
        </Stuff>  
    </ItemGroup>  
    <Target Name="Batching">  
        <Message Text="@(Stuff)" Condition=" '%(Display)' == 'true' "/>  
    </Target>  
</Project>  
```  
  
###  <a name="BKMK_WellKnownItemMetadata"></a> 既知の項目メタデータ  
 アイテムの種類に追加した項目には、既知のメタデータが割り当てられます。 たとえば、すべての項目には既知のメタデータ `%(Filename)` があり、その値は項目のファイル名です。 詳細については、「[既知の項目メタデータ](../msbuild/msbuild-well-known-item-metadata.md)」を参照してください。  
  
###  <a name="BKMK_Transforming"></a> メタデータを使用してアイテムの種類を変換する  
 メタデータを使用して、項目リストを新しい項目リストに変換できます。 たとえば、式 `@(CppFiles -> '%(Filename).obj')` を使用すると、.cpp ファイルを表す項目を持つアイテムの種類 `CppFiles` を、.obj ファイルの対応するリストに変換できます。  
  
 次のコードでは `CultureResource` というアイテムの種類を作成し、`Culture` メタデータを持つすべての `EmbeddedResource` 項目のコピーをそこに含めます。 `Culture` メタデータの値は、新しいメタデータ `CultureResource.TargetDirectory` の値になります。  
  
```  
<Target Name="ProcessCultureResources">  
    <ItemGroup>  
        <CultureResource Include="@(EmbeddedResource)"  
            Condition="'%(EmbeddedResource.Culture)' != ''">  
            <TargetDirectory>%(EmbeddedResource.Culture) </TargetDirectory>  
        </CultureResource>  
    </ItemGroup>  
</Target>  
```  
  
 詳細については、「[MSBuild 変換](../msbuild/msbuild-transforms.md)」を参照してください。  
  
##  <a name="BKMK_ItemDefinitions"></a> 項目定義  
 .NET Framework 3.5 以降、[ItemDefinitionGroup 要素](../msbuild/itemdefinitiongroup-element-msbuild.md)を使用して、既定のメタデータをアイテムの種類に追加できるようになりました。 既知のメタデータと同様に、既定のメタデータも、指定するアイテムの種類に含まれるすべての項目に関連付けられます。 既定のメタデータは、項目定義で明示的にオーバーライドできます。 たとえば、次の XML は `Compile` の項目 "one.cs" および "three.cs" に、"Monday" という値を持つメタデータ `BuildDay` を指定します。 コードは項目 "two.cs" に、値 "Tuesday" を持つメタデータ `BuildDay` を指定します。  
  
```  
<ItemDefinitionGroup>  
    <Compile>  
        <BuildDay>Monday</BuildDay>  
    </Compile>  
</ItemDefinitionGroup>  
<ItemGroup>  
    <Compile Include="one.cs;three.cs" />  
    <Compile Include="two.cs">  
        <BuildDay>Tuesday</BuildDay>  
    </Compile>  
</ItemGroup>  
```  
  
 詳細については、「[項目定義](../msbuild/item-definitions.md)」を参照してください。  
  
##  <a name="BKMK_AttributesWithinTargets"></a> Target の ItemGroup の項目の属性  
 .NET Framework 3.5 以降では、項目要素を格納できる [ItemGroup](../msbuild/itemgroup-element-msbuild.md) 要素を `Target` 要素に含めることができます。 このセクションの属性は、`Target` にある `ItemGroup` の項目に指定されている場合に有効です。  
  
###  <a name="BKMK_RemoveAttribute"></a> Remove 属性  
 ターゲットの `ItemGroup` の項目には `Remove` 属性を含めることができます。この属性は、アイテムの種類から特定の項目 (ファイル) を削除します。 この属性は、.NET Framework 3.5 で導入されました。  
  
 次の例では、アイテムの種類 Compile からすべての .config ファイルを削除します。  
  
```  
<Target>  
    <ItemGroup>  
        <Compile Remove="*.config"/>  
    </ItemGroup>  
</Target>  
```  
  
###  <a name="BKMK_KeepMetadata"></a> KeepMetadata 属性  
 ターゲット内に項目が生成される場合、項目要素に `KeepMetadata` 属性を含めることができます。 この属性が指定される場合、セミコロン区切りの名前リストで指定されているメタデータのみがソース項目からターゲット項目に転送されます。 この属性に空の値を指定することは、値を指定しないことと同じです。 `KeepMetadata` 属性は、.NET Framework 4.5 で導入されました。  
  
 次の例は、`KeepMetadata` 属性を使用する方法を示しています。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"  
ToolsVersion="4.0">  
  
    <ItemGroup>  
        <FirstItem Include="rhinoceros">  
            <Class>mammal</Class>  
            <Size>large</Size>  
        </FirstItem>  
  
    </ItemGroup>  
    <Target Name="MyTarget">  
        <ItemGroup>  
            <SecondItem Include="@(FirstItem)" KeepMetadata="Class" />  
        </ItemGroup>  
  
        <Message Text="FirstItem: %(FirstItem.Identity)" />  
        <Message Text="  Class: %(FirstItem.Class)" />  
        <Message Text="  Size:  %(FirstItem.Size)"  />  
  
        <Message Text="SecondItem: %(SecondItem.Identity)" />  
        <Message Text="  Class: %(SecondItem.Class)" />  
        <Message Text="  Size:  %(SecondItem.Size)"  />  
    </Target>  
</Project>  
  
<!--  
Output:  
  FirstItem: rhinoceros  
    Class: mammal  
    Size:  large  
  SecondItem: rhinoceros  
    Class: mammal  
    Size:   
-->  
```  
  
###  <a name="BKMK_RemoveMetadata"></a> RemoveMetadata 属性  
 ターゲット内に項目が生成される場合、項目要素に `RemoveMetadata` 属性を含めることができます。 この属性が指定される場合、名前がセミコロン区切りの名前リストに含まれているメタデータを除いて、すべてのメタデータがソース項目からターゲット項目に転送されます。 この属性に空の値を指定することは、値を指定しないことと同じです。 `RemoveMetadata` 属性は、.NET Framework 4.5 で導入されました。  
  
 次の例は、`RemoveMetadata` 属性を使用する方法を示しています。  
  
```  
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <PropertyGroup>  
        <MetadataToRemove>Size;Material</MetadataToRemove>  
    </PropertyGroup>  
  
    <ItemGroup>  
        <Item1 Include="stapler">  
            <Size>medium</Size>  
            <Color>black</Color>  
            <Material>plastic</Material>  
        </Item1>  
    </ItemGroup>  
  
    <Target Name="MyTarget">  
        <ItemGroup>  
            <Item2 Include="@(Item1)" RemoveMetadata="$(MetadataToRemove)" />  
        </ItemGroup>  
  
        <Message Text="Item1: %(Item1.Identity)" />  
        <Message Text="  Size:     %(Item1.Size)" />  
        <Message Text="  Color:    %(Item1.Color)" />  
        <Message Text="  Material: %(Item1.Material)" />  
        <Message Text="Item2: %(Item2.Identity)" />  
        <Message Text="  Size:     %(Item2.Size)" />  
        <Message Text="  Color:    %(Item2.Color)" />  
        <Message Text="  Material: %(Item2.Material)" />  
    </Target>  
</Project>  
  
<!--  
Output:   
  Item1: stapler  
    Size:     medium  
    Color:    black  
    Material: plastic  
  Item2: stapler  
    Size:       
    Color:    black  
    Material:   
-->  
```  
  
###  <a name="BKMK_KeepDuplicates"></a> KeepDuplicates 属性  
 ターゲット内に項目が生成される場合、項目要素に `KeepDuplicates` 属性を含めることができます。 `KeepDuplicates` は、項目が既存の項目の完全な複製である場合に、項目をターゲット グループに追加するかどうかを指定する `Boolean` 属性です。  
  
 ソースとターゲットの項目の Include 値が同じでメタデータが異なる場合、`KeepDuplicates` が `false` に設定されていても項目は追加されます。 この属性に空の値を指定することは、値を指定しないことと同じです。 `KeepDuplicates` 属性は、.NET Framework 4.5 で導入されました。  
  
 次の例は、`KeepDuplicates` 属性を使用する方法を示しています。  
  
```  
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <Item1 Include="hourglass;boomerang" />  
        <Item2 Include="hourglass;boomerang" />  
    </ItemGroup>  
  
    <Target Name="MyTarget">  
        <ItemGroup>  
            <Item1 Include="hourglass" KeepDuplicates="false" />  
            <Item2 Include="hourglass" />  
        </ItemGroup>  
  
        <Message Text="Item1: @(Item1)" />  
        <Message Text="  %(Item1.Identity)  Count: @(Item1->Count())" />  
        <Message Text="Item2: @(Item2)" />  
        <Message Text="  %(Item2.Identity)  Count: @(Item2->Count())" />  
    </Target>  
</Project>  
  
<!--  
Output:   
  Item1: hourglass;boomerang  
    hourglass  Count: 1  
    boomerang  Count: 1  
  Item2: hourglass;boomerang;hourglass  
    hourglass  Count: 2  
    boomerang  Count: 1  
-->  
```  
  
## <a name="see-also"></a>関連項目
 [MSBuild の概念](../msbuild/msbuild-concepts.md)  
 [MSBuild](msbuild.md)   
 [方法: ビルドするファイルを選択する](../msbuild/how-to-select-the-files-to-build.md)   
 [方法: ビルドからファイルを除外する](../msbuild/how-to-exclude-files-from-the-build.md)   
 [方法: 項目リストをコンマ区切りで表示する](../msbuild/how-to-display-an-item-list-separated-with-commas.md)   
 [項目定義](../msbuild/item-definitions.md)   
 [バッチ](../msbuild/msbuild-batching.md)   
 [Item 要素 (MSBuild)](../msbuild/item-element-msbuild.md)
