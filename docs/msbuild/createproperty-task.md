---
title: CreateProperty タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#CreateProperty
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- CreateProperty task [MSBuild]
- MSBuild, CreateProperty task
ms.assetid: fbc31a88-62d4-43d2-b739-68ef3fac38f5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 39b732a962f648f0c812f3f9d37df7dcf17296ce
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56626610"
---
# <a name="createproperty-task"></a>CreateProperty タスク
渡された値をプロパティに入力します。 プロパティ間または文字列間で値をコピーできます。

## <a name="attributes"></a>属性
`CreateProperty` タスクのパラメーターの説明を次の表に示します。

| パラメーター | 説明 |
|------------------| - |
| `Value` | 省略可能な `String` 型の出力パラメーターです。<br /><br /> 新しいプロパティにコピーする値を指定します。 |
| `ValueSetByTask` | 省略可能な `String` 型の出力パラメーターです。<br /><br /> `Value` パラメーターと同じ値を含みます。 出力が最新の状態であるため、含まれているターゲットをスキップするとき、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] によって出力プロパティが設定されることを回避する場合にのみ、このパラメーターを使用します。 |

## <a name="remarks"></a>解説
上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例
次の例では、`CreateProperty` タスクによって `NewFile` プロパティが作成されます。`SourceFilename` および `SourceFileExtension` プロパティの値の組み合わせが使用されます。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
        <SourceFilename>Module1</SourceFilename>
        <SourceFileExtension>vb</SourceFileExtension>
    </PropertyGroup>

    <Target Name="CreateProperties">

        <CreateProperty
            Value="$(SourceFilename).$(SourceFileExtension)">
            <Output
                TaskParameter="Value"
                PropertyName="NewFile" />
        </CreateProperty>

    </Target>

</Project>
```

プロジェクトの実行後、`NewFile` プロパティの値は *Module1.vb* になります。

## <a name="see-also"></a>関連項目
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [タスク](../msbuild/msbuild-tasks.md)
