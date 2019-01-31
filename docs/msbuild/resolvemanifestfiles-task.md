---
title: ResolveManifestFiles タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ResolveManifestFiles task [MSBuild]
- MSBuild, ResolveManifestFiles task
ms.assetid: e1e14f67-9b69-433f-94d4-a783a68676b2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4e3d5fd327e6ef9db5029697d502d27574a8a8f7
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "55043220"
---
# <a name="resolvemanifestfiles-task"></a>ResolveManifestFiles タスク
ビルド処理に含まれる各種のアイテム (ビルド済みアイテム、依存関係、サテライト、コンテンツ、デバッグ シンボル、ドキュメントなど) をマニフェスト生成のためのファイルに解決します。  
  
## <a name="parameters"></a>パラメーター  
 `ResolveManifestFiles` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`DeploymentManifestEntryPoint`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> 配置マニフェストの名前を指定します。|  
|`EntryPoint`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> マニフェストへのエントリ ポイントであるマネージド アセンブリまたは ClickOnce マニフェストの参照を指定します。|  
|`ExtraFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 追加ファイルを指定します。|  
|`ManagedAssemblies`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> マネージド アセンブリを指定します。|  
|`NativeAssemblies`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> ネイティブ アセンブリを指定します。|  
|`OutputAssemblies`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 生成されたアセンブリを指定します。|  
|`OutputDeploymentManifestEntryPoint`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型の出力パラメーターです。<br /><br /> 出力される配置マニフェストのエントリ ポイントを指定します。|  
|`OutputEntryPoint`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型の出力パラメーターです。<br /><br /> 出力エントリ ポイントを指定します。|  
|`OutputFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 出力ファイルを指定します。|  
|`PublishFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 発行ファイルを指定します。|  
|`SatelliteAssemblies`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> サテライト アセンブリを指定します。|  
|`SigningManifests`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、マニフェストが署名されます。|  
|`TargetCulture`|省略可能な `String` 型のパラメーターです。<br /><br /> サテライト アセンブリのターゲット カルチャを指定します。|  
|`TargetFrameworkVersion`|省略可能な `String` 型のパラメーターです。<br /><br /> 対象とする .NET Framework のバージョンを指定します。|  
  
## <a name="remarks"></a>コメント  
 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [タスク](../msbuild/msbuild-tasks.md)   
 [タスク リファレンス](../msbuild/msbuild-task-reference.md)