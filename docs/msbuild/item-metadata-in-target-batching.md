---
title: ターゲットのバッチの項目メタデータ | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- batching [MSBuild]
- MSBuild, target batching
- target batching [MSBuild]
ms.assetid: f3cc4186-6a4c-4161-bbe5-1ec638b4925b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e512ad9f932e34a6ddd95e165b116465aa359a09
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/19/2018
ms.locfileid: "31568325"
---
# <a name="item-metadata-in-target-batching"></a>ターゲットのバッチの項目メタデータ
[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] では、ビルド ターゲットの入力と出力の依存関係分析を分析できます。 ターゲットの入力または出力が最新の状態であると判断された場合、ターゲットはスキップされ、ビルドが進行します。 `Target` 要素は `Inputs` 属性と `Outputs` 属性を利用し、依存関係分析中に検査する項目を指定します。  
  
 入力または出力としてバッチの項目を利用するタスクがターゲットに含まれる場合、ターゲットの `Target` 要素では、既に最新の状態になっている項目のバッチを [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] でスキップするために、その `Inputs` または `Outputs` 属性でバッチ処理を利用する必要があります。  
  
## <a name="batching-targets"></a>ターゲットのバッチ処理  
 次の例には、`Culture` 項目メタデータに基づいて 2 つのバッチに分割されている `Res` という名前の項目一覧が含まれています。 これらのバッチのいずれも `AL` タスクに渡されます。このタスクで、バッチごとに出力アセンブリが作成されます。 `Target` 要素の `Outputs` 属性でバッチ処理を利用することで、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] では、ターゲットを実行する前に、個々のバッチが最新の状態になっているか判断できます。 ターゲットのバッチ処理を利用しないと、ターゲットが実行されるたびに項目の両方のバッチが実行されます。  
  
```xml  
<Project  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <Res Include="Strings.fr.resources">  
            <Culture>fr</Culture>  
        </Res>  
        <Res Include="Strings.jp.resources">  
            <Culture>jp</Culture>  
        </Res>  
        <Res Include="Menus.fr.resources">  
            <Culture>fr</Culture>  
        </Res>  
        <Res Include="Dialogs.fr.resources">  
            <Culture>fr</Culture>  
        </Res>  
        <Res Include="Dialogs.jp.resources">  
            <Culture>jp</Culture>  
        </Res>  
        <Res Include="Menus.jp.resources">  
            <Culture>jp</Culture>  
        </Res>  
    </ItemGroup>  
  
    <Target Name="Build"  
        Inputs="@(Res)"  
        Outputs="%(Culture)\MyApp.resources.dll">  
  
        <AL Resources="@(Res)"  
            TargetType="library"  
            OutputAssembly="%(Culture)\MyApp.resources.dll"  
  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>参照  
 [方法 : インクリメンタル ビルドを実行する](../msbuild/how-to-build-incrementally.md)   
 [バッチ](../msbuild/msbuild-batching.md)   
 [Target 要素 (MSBuild)](../msbuild/target-element-msbuild.md)   
 [タスクのバッチの項目メタデータ](../msbuild/item-metadata-in-task-batching.md)