---
title: GetAssemblyIdentity タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GetAssemblyIdentity
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GetAssemblyIdentity task
- GetAssemblyIdentity task [MSBuild]
ms.assetid: a977e072-37ad-4941-84a6-32a4483be55d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aadbc72f3d7bb21f313ddaae0de97ec45a7e72a3
ms.sourcegitcommit: 01334abf36d7e0774329050d34b3a819979c95a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2019
ms.locfileid: "55853769"
---
# <a name="getassemblyidentity-task"></a>GetAssemblyIdentity タスク
指定されたファイルからアセンブリ ID を取得し、その ID を出力します。

## <a name="task-parameters"></a>タスク パラメーター
`GetAssemblyIdentity` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`Assemblies`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 取得したアセンブリ ID が含まれます。|
|`AssemblyFiles`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> ID の取得元のファイルを指定します。|

## <a name="remarks"></a>コメント
`Assemblies` パラメーターによって出力される項目には、`Version`、`PublicKeyToken`、`Culture` という名前の項目メタデータ エントリが含まれます。

上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例
次の例では、`MyAssemblies` 項目によって指定されているファイルの ID が取得され、それが `MyAssemblyIdentities` 項目に出力されます。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup>
        <MyAssemblies Include="File1.dll;File2.dll" />
    </ItemGroup>
    <Target Name="RetrieveIdentities">
        <GetAssemblyIdentity AssemblyFiles="@(MyAssemblies)">
            <Output TaskParameter="Assemblies" ItemName="MyAssemblyIdentities" />
        </GetAssemblyIdentity>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目
[タスク](../msbuild/msbuild-tasks.md)  
[タスク リファレンス](../msbuild/msbuild-task-reference.md)
