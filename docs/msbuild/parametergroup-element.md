---
title: ParameterGroup 要素 | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <ParameterGroup> element [MSBuild]
- ParameterGroup element [MSBuild]
ms.assetid: c3275e69-a427-4889-bc1d-51bff2c285fa
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d10b2e08b6e3f3c94c0a1f0cc1c24d239675c53
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56630549"
---
# <a name="parametergroup-element"></a>ParameterGroup 要素
`UsingTask` `TaskFactory` によって生成されるタスクで使用される省略可能なパラメーターのリストが格納されます。 詳細については、「[UsingTask 要素 (MSBuild)](../msbuild/usingtask-element-msbuild.md)」を参照してください。

 \<Project> \<UsingTask> \<ParameterGroup>

## <a name="syntax"></a>構文

```xml
<ParameterGroup />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[パラメーター](../msbuild/parameter-element.md)|`UsingTask` `TaskFactory` によって生成されるタスクの固有のパラメーターについての情報が格納されます。 要素の名前はパラメーターの名前です。|

### <a name="parent-elements"></a>親要素

| 要素 | 説明 |
| - | - |
| [UsingTask](../msbuild/usingtask-element-msbuild.md) | [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] にタスクを登録する方法を提供します。 1 つのプロジェクトに 0 個以上の `UsingTask` 要素を含めることができます。 |

## <a name="example"></a>例
 `ParameterGroup` 要素を使用する方法を次の例に示します。

```xml
<UsingTask TaskName="MyTask" AssemblyName="My.Assembly" TaskFactory="MyTaskFactory">
       <ParameterGroup>
              <Parameter1 ParameterType="System.String" Required="False" Output="False"/>
              <Parameter2 ParameterType="System.Int" Required="True" Output="False"/>
             ...
</ParameterGroup>
       <TaskBody Evaluate="true">
      ... Task factory-specific data ...
       </TaskBody>
</UsingTask>
```

## <a name="see-also"></a>関連項目
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)
