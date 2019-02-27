---
title: '方法: インクリメンタル ビルドを実行する | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, incremental builds
- incremental builds
- MSBuild, building incrementally
ms.assetid: 8d82d7d8-a2f1-4df6-9d2f-80b9e0cb3ac3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 59a637a530bfabe784aae2c1fab622e2c2380667
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56621332"
---
# <a name="how-to-build-incrementally"></a>方法: インクリメンタル ビルド
大規模なプロジェクトをビルドする場合、今でも最新の以前にビルドされたコンポーネントが再ビルドされないことが重要です。 すべてのターゲットが毎回ビルドされると、各ビルドが完了するのに長い時間がかかります。 インクリメンタル ビルド (ビルド内の以前にビルドされていないターゲット、または古くなっているターゲットだけが再ビルドされます) を有効にするため、[!INCLUDE[vstecmsbuildengine](../msbuild/includes/vstecmsbuildengine_md.md)] ([!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]) は入力ファイルのタイムスタンプと出力ファイルのタイムスタンプを比較して、ターゲットをスキップ、ビルド、または部分的に再ビルドするかどうかを判断できます。 ただし、入力と出力の間に一対一のマッピングが必要です。 変換を使用して、ターゲットがこの直接マッピングを識別できるようにすることができます。 変換の詳細については、「[MSBuild 変換](../msbuild/msbuild-transforms.md)」を参照してください。

## <a name="specify-inputs-and-outputs"></a>入力と出力を指定する
入力と出力がプロジェクト ファイルで指定されている場合は、ターゲットはインクリメンタル方式でビルドできます。

#### <a name="to-specify-inputs-and-outputs-for-a-target"></a>ターゲットに入力と出力を指定するには

- `Target` 要素の `Inputs` 属性と `Outputs` 属性を使用します。 次に例を示します。

  ```xml
  <Target Name="Build"
      Inputs="@(CSFile)"
      Outputs="hello.exe">
  ```

  [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] は入力ファイルのタイムスタンプと出力ファイルのタイムスタンプを比較し、ターゲットをスキップ、ビルド、または部分的に再ビルドするかどうかを判断できます。 次の例では、`@(CSFile)` 項目リスト内の任意のファイルが *hello.exe* ファイルより新しい場合、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] はターゲットを実行します。そうでない場合は、ターゲットがスキップされます。

```xml
<Target Name="Build"
    Inputs="@(CSFile)"
    Outputs="hello.exe">

    <Csc
        Sources="@(CSFile)"
        OutputAssembly="hello.exe"/>
</Target>
```

ターゲットで入力と出力が指定されている場合は、各出力を 1 つの入力のみにマップできるか、出力と入力の間に直接マッピングがないかのいずれかになります。 たとえば前の [Csc タスク](../msbuild/csc-task.md)では、出力 *hello.exe* はどの単一の入力にもマップできず、すべての入力に依存します。

> [!NOTE]
> 入力と出力の間の直接マッピングがないターゲットは、各ターゲットが 1 つの出力だけにマップできるターゲットよりもより頻繁にビルドされます。これは、入力の一部が変更された場合に、どの出力を再ビルドする必要があるかを [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] が判断できないからです。

[LC タスク](../msbuild/lc-task.md)など、出力と入力間の直接マッピングを識別できるタスクは、多くの入力から出力アセンブリを生成する [Csc](../msbuild/csc-task.md) や [Vbc](../msbuild/vbc-task.md) などとは異なり、インクリメンタル ビルドに最も適しています。

## <a name="example"></a>例
次の例では、架空のヘルプ システムのヘルプ ファイルをビルドするプロジェクトを使用します。 プロジェクトは、ソースの *.txt* ファイルを、中間の *.content* ファイルに変換し、これを XML メタデータ ファイルと結合してヘルプ システムで使用される最終の *.help* ファイルを生成することによって機能します。 プロジェクトでは、次の仮想タスクを使用します。

- `GenerateContentFiles`:*.txt* ファイルを *.content* ファイルに変換します。

- `BuildHelp`:*.content* ファイルと XML メタデータ ファイルを結合し、最終の *.help* ファイルをビルドします。


プロジェクトは、変換を使用して、`GenerateContentFiles` タスクで入力と出力間の一対一のマッピングを作成します。 詳細については、「[MSBuild 変換](../msbuild/msbuild-transforms.md)」をご覧ください。 また、`Output` 要素が `GenerateContentFiles` タスクからの出力を `BuildHelp` タスクの入力として自動的に使用するように設定されます。

このプロジェクト ファイルには、`Convert` と `Build` の両方のターゲットが含まれます。 `GenerateContentFiles` タスクと `BuildHelp` タスクはそれぞれ `Convert` と `Build` のターゲットに配置され、各ターゲットがそれぞれインクリメンタル方式でビルドできるようにします。 `Output` 要素を使用することで、`GenerateContentFiles` タスクの出力が `ContentFile` 項目リストに配置され、`BuildHelp` タスクの入力として使用できます。 このように `Output` 要素を使用することで、1 つのタスクからの出力が別のタスクの入力として自動的に提供されるため、各タスクで個々の項目または項目リストから手動でリストする必要はありません。

> [!NOTE]
> `GenerateContentFiles` ターゲットはインクリメンタル ビルドできますが、そのターゲットからのすべての出力は `BuildHelp` ターゲットの入力とし常に要求されます。 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] は、`Output` 要素を使用する場合に、1 つのターゲットからのすべての出力を別のターゲットの入力として自動的に提供します。

```xml
<Project DefaultTargets="Build"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >

    <ItemGroup>
        <TXTFile Include="*.txt"/>
        <XMLFiles Include="\metadata\*.xml"/>
    </ItemGroup>

    <Target Name = "Convert"
        Inputs="@(TXTFile)"
        Outputs="@(TXTFile->'%(Filename).content')">

        <GenerateContentFiles
            Sources = "@(TXTFile)">
            <Output TaskParameter = "OutputContentFiles"
                ItemName = "ContentFiles"/>
        </GenerateContentFiles>
    </Target>

    <Target Name = "Build" DependsOnTargets = "Convert"
        Inputs="@(ContentFiles);@(XMLFiles)"
        Outputs="$(MSBuildProjectName).help">

        <BuildHelp
            ContentFiles = "@(ContentFiles)"
            MetadataFiles = "@(XMLFiles)"
            OutputFileName = "$(MSBuildProjectName).help"/>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目
- [ターゲット](../msbuild/msbuild-targets.md)
- [Target 要素 (MSBuild)](../msbuild/target-element-msbuild.md)
- [変換](../msbuild/msbuild-transforms.md)
- [Csc タスク](../msbuild/csc-task.md)
- [Vbc タスク](../msbuild/vbc-task.md)
