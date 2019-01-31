---
title: Item 要素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Item Element [MSBuild]
- <Item> Element [MSBuild]
ms.assetid: dcef5f91-0613-4bfc-8ee9-d7004bb6d3a9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: befac75f321863784f6977e99e00b36dfc077563
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54943027"
---
# <a name="item-element-msbuild"></a>Item 要素 (MSBuild)
ユーザー定義のアイテムおよびそのメタデータが含まれます。 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] プロジェクトで使用されるすべてのアイテムが、`ItemGroup` 要素の子として指定されている必要があります。  

 \<Project>  
 \<ItemGroup>  
 \<Item>  

## <a name="syntax"></a>構文  

```xml  
<Item Include="*.cs"  
        Exclude="MyFile.cs"  
        Remove="RemoveFile.cs"  
        Condition="'String A'=='String B'" >  
    <ItemMetadata1>...</ItemMetadata1>  
    <ItemMetadata2>...</ItemMetadata2>  
</Item>  
```  

## <a name="specify-metadata-as-attributes"></a>メタデータを属性として指定する
MSBuild 15.1 以降では、現行の属性リストと競合しない名前のメタデータを任意で属性として表現できます。

たとえば、NuGet パッケージの一覧を指定するには、通常、次のような構文を使用します。

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json">
    <Version>9.0.1-beta1<Version>
  </PackageReference>
</ItemGroup>
```

ただし、次の構文のように、`Version` メタデータを属性として渡すことができます。

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" Version="9.0.1-beta1" />  
</ItemGroup>
```

## <a name="attributes-and-elements"></a>属性と要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  

### <a name="attributes"></a>属性  

|属性|説明|  
|---------------|-----------------|  
|`Include`|省略可能な属性です。<br /><br /> アイテムの一覧に含めるファイルまたはワイルドカードです。|  
|`Exclude`|省略可能な属性です。<br /><br /> アイテムの一覧から除外するファイルまたはワイルドカードです。|  
|`Condition`|省略可能な属性です。<br /><br /> 評価する条件です。 詳細については、「[条件](../msbuild/msbuild-conditions.md)」を参照してください。|  
|`Remove`|省略可能な属性です。<br /><br /> アイテムの一覧から削除するファイルまたはワイルドカードです。<br /><br />|  
|`KeepDuplicates`|省略可能な属性です。<br /><br /> 既存のアイテムの完全な複製である場合に、アイテムをターゲット グループに追加するかどうかを指定します。 ソースとターゲットのアイテムの `Include` 値が同じでメタデータが異なる場合、`KeepDuplicates` が `false` に設定されていてもアイテムは追加されます。 詳細については、「[MSBuild 項目](../msbuild/msbuild-items.md)」をご覧ください。<br /><br /> この属性は、`ItemGroup` 内にある `Target` のアイテムに指定されている場合にのみ有効です。|  
|`KeepMetadata`|省略可能な属性です。<br /><br /> ターゲット アイテムに追加するソース アイテムのメタデータ。 名前がセミコロン区切りのリストで指定されているメタデータのみ、ソース アイテムからターゲット アイテムに転送されます。 詳細については、「[MSBuild 項目](../msbuild/msbuild-items.md)」をご覧ください。<br /><br /> この属性は、`ItemGroup` 内にある `Target` のアイテムに指定されている場合にのみ有効です。|  
|`RemoveMetadata`|省略可能な属性です。<br /><br /> ターゲット アイテムに転送しないソース アイテムのメタデータ。 名前がセミコロン区切りの名前リストに含まれているメタデータを除いて、すべてのメタデータがソース アイテムからターゲット アイテムに転送されます。 詳細については、「[MSBuild 項目](../msbuild/msbuild-items.md)」をご覧ください。<br /><br /> この属性は、`ItemGroup` 内にある `Target` のアイテムに指定されている場合にのみ有効です。|  
|`Update`|省略可能な属性です。 (Visual Studio 2017 以降の .NET Core プロジェクトでのみ利用できます。)<br /><br /> glob で追加されたファイルのメタデータを変更できます。<br /><br />  この属性は、`Target` にない `ItemGroup` のアイテムに指定されている場合にのみ有効です。|  

### <a name="child-elements"></a>子要素  

|要素|説明|  
|-------------|-----------------|  
|[ItemMetadata](../msbuild/itemmetadata-element-msbuild.md)|アイテム メタデータ値を含むユーザー定義のアイテム メタデータ キーです。 1 つのアイテムに 0 個以上の `ItemMetadata` 要素を含めることができます。|  

### <a name="parent-elements"></a>親要素  

|要素|説明|  
|-------------|-----------------|  
|[ItemGroup](../msbuild/itemgroup-element-msbuild.md)|アイテムの grouping 要素です。|  

## <a name="remarks"></a>コメント  
 `Item` 要素はビルド システムへの入力を定義し、ユーザー定義のコレクション名に基づいてアイテム コレクションにグループ化されます。 これらのアイテム コレクションは、[タスク](../msbuild/msbuild-tasks.md)のパラメーターとして使用できます。タスクは、コレクション内の個々のアイテムを使用してビルド処理の各ステップを実行します。 詳細については、「[MSBuild 項目](../msbuild/msbuild-items.md)」をご覧ください。  

 @(\<myType>) という表記を使用すると、\<myType> 型のアイテムのコレクションをセミコロン区切りの文字列リストに展開して、パラメーターに渡すことができます。 パラメーターが `string` 型の場合は、パラメーターの値がセミコロンで区切られた要素のリストになります。 パラメーターが文字列の配列の場合 (`string[]`)、各要素はセミコロンの位置に基づいて配列に挿入されます。 タスク パラメーターが <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の場合、値は、アイテム コレクションの内容と、アタッチされているすべてのメタデータになります。 セミコロン以外の文字を使用して各アイテムを区切るには、@(<myType>, '<separator>') という構文を使用します。  

 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] エンジンでは、`*` や `?` などのワイルドカードや、*/\*\*/\*.cs* などの再帰的なワイルドカードを評価できます。 詳細については、「[MSBuild 項目](../msbuild/msbuild-items.md)」をご覧ください。  

## <a name="examples"></a>使用例  
 次のコード例は、`CSFile` 型の 2 つのアイテムを宣言する方法を示しています。 2 番目に宣言されているアイテムには、`MyMetadata` が `HelloWorld` に設定されたメタデータが含まれています。  

```xml  
<ItemGroup>  
    <CSFile Include="engine.cs; form.cs" />  
    <CSFile Include="main.cs" >  
        <MyMetadata>HelloWorld</MyMetadata>  
    </CSFile>  
</ItemGroup>  
```  
次のコード サンプルは、`Update` 属性を利用し、glob 経由で追加された *somefile.cs* という名前のファイルのメタデータを修正する方法を示しています。 (Visual Studio 2017 以降の .NET Core プロジェクトでのみ利用できます。)

```xml  
<ItemGroup>
    <Compile Update="somefile.cs">  // or Update="*.designer.cs"
        <MetadataKey>MetadataValue</MetadataKey>
    </Compile>
</ItemGroup>  
```  


## <a name="see-also"></a>関連項目  
 [項目](../msbuild/msbuild-items.md)   
 [MSBuild プロジェクトの共通項目](../msbuild/common-msbuild-project-items.md) [MSBuild プロパティ](../msbuild/msbuild-properties.md)   
 [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
