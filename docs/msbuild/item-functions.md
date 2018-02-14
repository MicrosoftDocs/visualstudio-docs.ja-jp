---
title: "項目用の関数 | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology: msbuild
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- msbuild, Item functions
ms.assetid: 5e6df3cc-2db8-4cbd-8fdd-3ffd03ac0876
caps.latest.revision: 
author: Mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload:
- multiple
ms.openlocfilehash: 6ca0ed4d1f895216e9fb3a015796a2f9e4f95087
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2018
---
# <a name="item-functions"></a>項目用の関数
MSBuild 4.0 以降、タスクとターゲットのコードは項目用の関数を呼び出し、プロジェクトの項目に関する情報を取得できます。 これらの関数により、Distinct() 項目の取得が簡素化され、項目をループ処理するよりも処理が速くなります。  
  
## <a name="string-item-functions"></a>文字列項目関数  
 .NET Framework の String メソッドと String プロパティを利用し、あらゆる項目値を操作できます。 <xref:System.String> メソッドの場合、メソッド名を指定します。 <xref:System.String> プロパティの場合、"get_" の後にプロパティ名を指定します。  
  
 項目に複数の文字列が含まれる場合、String メソッドまたはプロパティは各文字列で実行されます。  
  
 次は、これらの文字列項目関数の使用方法を示す例です。  
  
```xml  
<ItemGroup>  
    <theItem Include="andromeda;tadpole;cartwheel" />  
</ItemGroup>  
  
<Target Name = "go">  
    <Message Text="IndexOf  @(theItem->IndexOf('r'))" />  
    <Message Text="Replace  @(theItem->Replace('tadpole', 'pinwheel'))" />  
    <Message Text="Length   @(theItem->get_Length())" />  
    <Message Text="Chars    @(theItem->get_Chars(2))" />  
</Target>  
  
  <!--  
  Output:  
    IndexOf  3;-1;2  
    Replace  andromeda;pinwheel;cartwheel  
    Length   9;7;9  
    Chars    d;d;r  
  -->  
```  
  
## <a name="intrinsic-item-functions"></a>組み込み項目関数  
 下の表は、項目に利用できる組み込み関数をまとめたものです。  
  
|関数|例|説明|  
|--------------|-------------|-----------------|  
|`Count`|`@(MyItem->Count())`|項目の数を返します。|  
|`DirectoryName`|`@(MyItem->DirectoryName())`|項目ごとに `Path.DirectoryName` の等価を返します。|  
|`Distinct`|`@(MyItem->Distinct())`|別個の `Include` 値を含む項目を返します。 メタデータは無視されます。 比較では、大文字と小文字が区別されません。|  
|`DistinctWithCase`|`@(MyItem->DistinctWithCase())`|別個の `itemspec` 値を含む項目を返します。 メタデータは無視されます。 比較では、大文字と小文字を区別します。|  
|`Reverse`|`@(MyItem->Reverse())`|項目を逆の順序で返します。|  
|`AnyHaveMetadataValue`|`@(MyItem->AnyHaveMetadataValue("MetadataName", "MetadataValue"))`|特定のメタデータの名前と値が項目に含まれているかどうかを示す `boolean` を返します。 比較では、大文字と小文字が区別されません。|  
|`ClearMetadata`|`@(MyItem->ClearMetadata())`|メタデータを消して項目を返します。 `itemspec` のみが保持されます。|  
|`HasMetadata`|`@(MyItem->HasMetadata("MetadataName"))`|特定のメタデータ名を含む項目を返します。 比較では、大文字と小文字が区別されません。|  
|`Metadata`|`@(MyItem->Metadata("MetadataName"))`|メタデータ名が含まれるメタデータの値を返します。|  
|`WithMetadataValue`|`@(MyItem->WithMetadataValue("MetadataName", "MetadataValue"))`|特定のメタデータの名前と値を含む項目を返します。 比較では、大文字と小文字が区別されません。|  
  
 次は、組み込み項目関数の使用方法を示す例です。  
  
```xml  
<ItemGroup>  
    <TheItem Include="first">  
        <Plant>geranium</Plant>  
    </TheItem>  
    <TheItem Include="second">  
        <Plant>algae</Plant>  
    </TheItem>  
    <TheItem Include="third">  
        <Plant>geranium</Plant>  
    </TheItem>  
</ItemGroup>  
  
<Target Name="go">  
    <Message Text="MetaData:    @(TheItem->Metadata('Plant'))" />  
    <Message Text="HasMetadata: @(theItem->HasMetadata('Plant'))" />  
    <Message Text="WithMetadataValue: @(TheItem->WithMetadataValue('Plant', 'geranium'))" />  
    <Message Text=" " />  
    <Message Text="Count:   @(theItem->Count())" />  
    <Message Text="Reverse: @(theItem->Reverse())" />  
</Target>  
  
  <!--   
  Output:  
    MetaData:    geranium;algae;geranium  
    HasMetadata: first;second;third  
    WithMetadataValue: first;third  
  
    Count:   3  
    Reverse: third;second;first  
  -->  
```  
  
## <a name="see-also"></a>参照  
 [項目](../msbuild/msbuild-items.md)
