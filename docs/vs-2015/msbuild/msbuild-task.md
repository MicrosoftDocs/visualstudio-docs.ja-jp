---
title: MSBuild タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#MSBuild
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild task [MSBuild]
- MSBuild, MSBuild task
ms.assetid: 76577f6c-7669-44ad-a840-363e37a04d34
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 15a6f0d3a0a50068d05a96994cb01462f07f3258
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54772338"
---
# <a name="msbuild-task"></a>MSBuild タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
別の [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトから [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトをビルドします。  
  
## <a name="parameters"></a>パラメーター  
 `MSBuild` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`BuildInParallel`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、`Projects` パラメーターに指定されたプロジェクトが同時にビルドされます (可能な場合)。 既定値は `false` です。|  
|`Projects`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> ビルドするプロジェクト ファイルを指定します。|  
|`Properties`|省略可能な `String` 型のパラメーターです。<br /><br /> 子プロジェクトに対してグローバル プロパティとして適用するプロパティの名前/値ペアのセミコロンで区切られたリスト。 このパラメーターを指定することは、[MSBuild.exe](../msbuild/msbuild-command-line-reference.md) でビルドするときに **/property** スイッチを持つプロパティを設定することと同じ意味になります。 次に例を示します。<br /><br /> `Properties="Configuration=Debug;Optimize=$(Optimize)"`<br /><br /> `Properties` パラメーター経由でプロジェクトにプロパティを渡すと、プロジェクト ファイルが既に読み込まれている場合でも、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] はプロジェクトの新しいインスタンスを作成します。 プロジェクトの新しいインスタンスが作成されると、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] はそのインスタンスを、異なるグローバル プロパティを持ち、プロジェクトの他のインスタンスと同時にビルド可能な別のプロジェクトとして扱います。 たとえば、リリース構成をデバッグ構成と同時にビルドできます。|  
|`RebaseOutputs`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、ビルド プロジェクトからのターゲットの出力項目の相対パスを、呼び出し元プロジェクトからの相対パスに合わせます。 既定値は `false` です。|  
|`RemoveProperties`|省略可能な `String` 型のパラメーターです。<br /><br /> 削除するグローバル プロパティのセットを指定します。|  
|`RunEachTargetSeparately`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] タスクは [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] に渡される一覧内の各ターゲットを同時ではなく、一度に 1 つずつ呼び出します。 このパラメーターを `true` に設定すると、前に呼び出したターゲットが失敗しても、後に続くターゲットは呼び出されることが保証されます。 それ以外の場合は、ビルド エラーが発生すると、以降のすべてのターゲットの呼び出しは停止されます。 既定値は `false` です。|  
|`SkipNonexistentProjects`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、ディスク上に存在しないプロジェクト ファイルはスキップされます。 それ以外の場合は、そのようなプロジェクトによりエラーが発生します。|  
|`StopOnFirstFailure`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、プロジェクトの 1 つがビルドに失敗すると、プロジェクトはそれ以上ビルドされません。 この機能は現在、同時にビルド (複数のプロセッサを使用) する際にはサポートされていません。|  
|`TargetAndPropertyListSeparators`|省略可能な `String[]` 型のパラメーターです。<br /><br /> `Project` 項目メタデータとしてターゲットとプロパティのリストを指定します。 区切り記号は、処理の前にエスケープ解除されます。 たとえば、%3B (エスケープされた ';') はエスケープされていない ';' のように扱われます。|  
|`TargetOutputs`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の読み取り専用の出力パラメーターです。<br /><br /> すべてのプロジェクト ファイルからビルドされたターゲットの出力を返します。 指定したターゲットの出力だけが返されます。それらのターゲットが依存しているターゲットに存在する可能性があるすべての出力が返されるわけではありません。<br /><br /> `TargetOutputs` パラメーターには、次のメタデータも含まれています。<br /><br /> -   `MSBuildSourceProjectFile`: 出力を設定するターゲットを含む [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクト ファイル。<br />-   `MSBuildSourceTargetName`: 出力を設定するターゲット。 **注:**  各プロジェクト ファイルまたはターゲットの出力を個別に識別する場合は、プロジェクト ファイルまたはターゲットごとに `MSBuild` タスクを実行します。 `MSBuild` タスクを 1 回だけ実行してすべてのプロジェクト ファイルをビルドすると、すべてのターゲットの出力が 1 つの配列に収集されます。|  
|`Targets`|省略可能な `String` 型のパラメーターです。<br /><br /> プロジェクト ファイルでビルドする 1 つまたは複数のターゲットを指定します。 セミコロンを使用して、ターゲットの名前の一覧を区切ります。 `MSBuild` タスクにターゲットを指定しない場合は、プロジェクト ファイルで指定されている既定のターゲットがビルドされます。 **注:**  ターゲットは、すべてのプロジェクト ファイルに必要です。 ターゲットが存在しない場合は、ビルド エラーが発生します。|  
|`ToolsVersion`|省略可能な `String` 型のパラメーターです。<br /><br /> このタスクに渡されたプロジェクトのビルド時に使用する `ToolsVersion` を指定します。<br /><br /> [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] タスクが、プロジェクトで指定されたものとは別のバージョンの [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] をターゲットとするプロジェクトをビルドできるようにします。 有効な値は `2.0`、`3.0`、`3.5` です。 既定値は `3.5`にする必要があります。|  
|`UnloadProjectsOnCompletion`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、操作が完了したらプロジェクトはアンロードされます。|  
|`UseResultsCache`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、キャッシュされた結果が返されます (ある場合)。 MSBuild タスクが実行された場合、その結果はスコープ (ProjectFileName, GlobalProperties)[TargetNames] に<br /><br /> ビルド項目のリストとしてキャッシュされます。|  
  
## <a name="remarks"></a>解説  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
 [Exec Task](../msbuild/exec-task.md) を使用して MSBuild.exe を起動する場合と異なり、このタスクでは、同じ [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロセスを使用して子プロジェクトがビルドされます。 すでにビルドされていて、スキップできるターゲットの一覧は、親のビルドと子のビルドの両方で共有されます。 また、新しい [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロセスが作成されないため、このタスクは高速です。  
  
 このタスクでは、プロジェクト ファイルだけでなく、ソリューション ファイルも処理できます。  
  
 プロジェクトを同時にビルドできるようにするために [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] によって求められる構成は、構成に (ポート、プロトコル、タイムアウト、再試行などの) リモート インフラストラクチャが関連する場合でも、構成ファイルを使用して構成可能にする必要があります。 可能であれば、構成項目を `MSBuild` タスクのタスク パラメーターとして指定できるようにします。  
  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 3.5 以降、ソリューション プロジェクトは、ビルドするすべてのサブ プロジェクトから TargetOutputs を出力するようになりました。  
  
## <a name="passing-properties-to-projects"></a>プロジェクトへのプロパティの引き渡し  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 3.5 以前のバージョンの [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] では、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 項目に一覧表示されている別のプロジェクトに対してプロパティの別のセットを渡すことは困難でした。 [MSBuild タスク](../msbuild/msbuild-task.md)の Properties 属性を使用すると、その設定はビルド対象のすべてのプロジェクトに適用されていました (ただし、[MSBuild タスク](../msbuild/msbuild-task.md)をバッチ処理し、項目一覧内の各プロジェクトに対して別のプロパティを条件に応じて用意する場合は除く)。  
  
 しかし、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 3.5 には、新しい予約済みのメタデータ項目が 2 つあります (Properties と AdditionalProperties)。これらのメタデータ項目は、[MSBuild タスク](../msbuild/msbuild-task.md)を使用してビルドされる別プロジェクトに異なるプロパティを渡すための柔軟な方法を提供します。  
  
> [!NOTE]
>  これらの新しいメタデータ項目は、[MSBuild タスク](../msbuild/msbuild-task.md)の Projects 属性に渡される項目に対してのみ適用可能です。  
  
## <a name="multi-processor-build-benefits"></a>マルチプロセッサ ビルドの利点  
 この新しいメタデータを使用する最大の利点の 1 つを享受できるのは、マルチプロセッサ システム上でプロジェクトを同時にビルドする場合です。 メタデータを使用することで、すべてのプロジェクトを単一の [MSBuild タスク](../msbuild/msbuild-task.md)呼び出しに統合することができます。バッチ処理や条件付き [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] タスクを実行する必要はありません。 単一の [MSBuild タスク](../msbuild/msbuild-task.md)を呼び出すだけで、Projects 属性に指定されているすべてのプロジェクトが同時にビルドされます。 (ただし、`BuildInParallel=true` 属性が [MSBuild タスク](../msbuild/msbuild-task.md)に指定されている場合に限定されます。)詳細については、「[複数のプロジェクトの並行ビルド](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)」を参照してください。  
  
## <a name="properties-metadata"></a>Properties メタデータ  
 一般的なシナリオとして、[MSBuild タスク](../msbuild/msbuild-task.md)を使用し、ビルド構成だけは異なるものを使用して、複数のソリューション ファイルをビルドすることが挙げられます。 デバッグ構成を使用してソリューション a1 をビルドし、リリース構成を使用してソリューション a2 をビルドすることができます。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 2.0 では、このプロジェクト ファイルは次のようになります。  
  
> [!NOTE]
>  次の例で、"…" はその他のソリューション ファイルを表します。  
  
### <a name="aproj"></a>a.proj  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Target Name="Build">  
        <MSBuild Projects="a1.sln..." Properties="Configuration=Debug"/>  
        <MSBuild Projects="a2.sln" Properties="Configuration=Release"/>  
    </Target>  
</Project>  
```  
  
 しかし、Properties メタデータを使用すると、次の例に示すように、単一の [MSBuild タスク](../msbuild/msbuild-task.md)を使用して簡素化できます。  
  
### <a name="aproj"></a>a.proj  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <ProjectToBuild Include="a1.sln…">  
            <Properties>Configuration=Debug</Properties>  
        </ProjectToBuild>  
        <ProjectToBuild Include="a2.sln">  
            <Properties>Configuration=Release</Properties>  
        </ProjectToBuild>  
    </ItemGroup>  
    <Target Name="Build">  
        <MSBuild Projects="@(ProjectToBuild)"/>  
    </Target>  
</Project>  
```  
  
 \- または  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <ProjectToBuild Include="a1.sln…"/>  
        <ProjectToBuild Include="a2.sln">  
            <Properties>Configuration=Release</Properties>  
        </ProjectToBuild>  
    </ItemGroup>  
    <Target Name="Build">  
        <MSBuild Projects="@(ProjectToBuild)"   
          Properties="Configuration=Debug"/>  
    </Target>  
</Project>  
```  
  
## <a name="additionalproperties-metadata"></a>AdditionalProperties メタデータ  
 [MSBuild タスク](../msbuild/msbuild-task.md)を使用して 2 つのソリューション ファイルをビルドするシナリオを考えます。いずれのソリューション ファイルでもリリース構成を使用しますが、一方は x86 アーキテクチャ、もう一方は ia64 アーキテクチャを使用します。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 2.0 では、[MSBuild タスク](../msbuild/msbuild-task.md)の複数のインスタンスを作成する必要があります。一方は x86 アーキテクチャに基づいたリリース構成を使用してプロジェクトをビルドし、もう一方は ia64 アーキテクチャに基づいたリリース構成を使用してプロジェクトをビルドします。 プロジェクト ファイルは次のようになります。  
  
### <a name="aproj"></a>a.proj  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Target Name="Build">  
        <MSBuild Projects="a1.sln…" Properties="Configuration=Release;   
          Architecture=x86"/>  
        <MSBuild Projects="a2.sln" Properties="Configuration=Release;   
          Architecture=ia64"/>  
    </Target>  
</Project>  
```  
  
 AdditionalProperties メタデータを使用すると、次のコードを使用することによって、単一の [MSBuild タスク](../msbuild/msbuild-task.md)を使用して簡素化できます。  
  
### <a name="aproj"></a>a.proj  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <ProjectToBuild Include="a1.sln…">  
            <AdditionalProperties>Architecture=x86  
              </AdditionalProperties>  
        </ProjectToBuild>  
        <ProjectToBuild Include="a2.sln">  
            <AdditionalProperties>Architecture=ia64  
              </AdditionalProperties>  
        </ProjectToBuild>  
    </ItemGroup>  
    <Target Name="Build">  
        <MSBuild Projects="@(ProjectToBuild)"   
          Properties="Configuration=Release"/>  
    </Target>  
</Project>  
```  
  
## <a name="example"></a>例  
 次の例では、`MSBuild` タスクを使用して、`ProjectReferences` 項目コレクションで指定されたプロジェクトをビルドしています。 ターゲットの出力結果は、`AssembliesBuiltByChildProjects` 項目コレクションに格納されます。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <ProjectReferences Include="*.*proj" />  
    </ItemGroup>  
  
    <Target Name="BuildOtherProjects">  
        <MSBuild  
            Projects="@(ProjectReferences)"  
            Targets="Build">  
            <Output  
                TaskParameter="TargetOutputs"  
                ItemName="AssembliesBuiltByChildProjects" />  
        </MSBuild>  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>関連項目
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
