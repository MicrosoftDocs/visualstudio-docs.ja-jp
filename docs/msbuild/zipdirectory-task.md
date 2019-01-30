---
title: ZipDirectory タスク | Microsoft Docs
ms.date: 11/04/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ZipDirectory
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ZipDirectory task [MSBuild]
- MSBuild, ZipDirectory task
ms.assetid: 916bb2e3-3017-4828-ae27-c0b5c99bbb48
caps.latest.revision: 16
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b09c98fb41adcf1d094ca3cf35e9415773e5c292
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54963529"
---
# <a name="zipdirectory-task"></a>ZipDirectory タスク
ディレクトリのコンテンツから *.zip* アーカイブを作成します。

>[!NOTE]
>`ZipDirectory` タスクは MSBuild 15.8 以降でのみ使用できます。
  
## <a name="parameters"></a>パラメーター  
 `ZipDirectory` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`DestinationFile`|必須の <xref:Microsoft.Build.Framework.ITaskItem> パラメーター<br /><br /> 作成する *.zip* ファイルへの完全パス。|
|`Overwrite`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、対象ファイルが存在する場合はスキップすると上書きされます。 既定値は `false` です。|
|`SourceDirectory`|必須の <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> *.zip* アーカイブの作成元のディレクトリを指定します。|
  
## <a name="remarks"></a>コメント  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、プロジェクトのビルド後、出力ディレクトリから *.zip* アーカイブを作成します。
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <Target Name="ZipOutputPath" AfterTargets="Build">
        <ZipDirectory
            SourceDirectory="$(OutputPath)"
            DestinationFile="$(MSBuildProjectDirectory)\output.zip" />
    </Target>

</Project>
```
  
## <a name="see-also"></a>関連項目  
 [タスク](../msbuild/msbuild-tasks.md)   
 [タスク リファレンス](../msbuild/msbuild-task-reference.md)
