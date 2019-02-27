---
title: GetFrameworkPath タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GetFrameworkPath
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- GetFrameworkPath task [MSBuild]
- MSBuild, GetFrameworkPath task
ms.assetid: 5b7bcdd7-d4a0-442d-af29-8aadb3b10598
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b836a0fef26f34e83f7238ebe4f6c64731b84257
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56610360"
---
# <a name="getframeworkpath-task"></a>GetFrameworkPath タスク
[!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] アセンブリへのパスを取得します。

## <a name="task-parameters"></a>タスク パラメーター
`GetFrameworkPath` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`FrameworkVersion11Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 存在する場合、フレームワーク バージョン 1.1 アセンブリのパスが含まれます。 それ以外の場合は、`null` を返します。|
|`FrameworkVersion20Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 存在する場合、フレームワーク バージョン 2.0 アセンブリのパスが含まれます。 それ以外の場合は、`null` を返します。|
|`FrameworkVersion30Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 存在する場合、フレームワーク バージョン 3.0 アセンブリのパスが含まれます。 それ以外の場合は、`null` を返します。|
|`FrameworkVersion35Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 存在する場合、フレームワーク バージョン 3.5 アセンブリのパスが含まれます。 それ以外の場合は、`null` を返します。|
|`FrameworkVersion40Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 存在する場合、フレームワーク バージョン 4.0 アセンブリのパスが含まれます。 それ以外の場合は、`null` を返します。|
|`Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 利用できる場合、最新のフレームワーク アセンブリのパスが含まれます。 それ以外の場合は、`null` を返します。|

## <a name="remarks"></a>解説
[!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] のいくつかのバージョンがインストールされている場合、このタスクは、[!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] が実行されるように設計されているバージョンを返します。

上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例
次の例では、`GetFrameworkPath` タスクを使用し、[!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)] のパスを `FrameworkPath` プロパティに保存します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="GetPath">
        <GetFrameworkPath>
            <Output
                TaskParameter="Path"
                PropertyName="FrameworkPath" />
        </GetFrameworkPath>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
