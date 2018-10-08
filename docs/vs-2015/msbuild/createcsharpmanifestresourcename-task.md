---
title: CreateCSharpManifestResourceName タスク | Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, CreateCSharpManifestResourceName task
- CreateCSharpManifestResourceName task [MSBuild]
ms.assetid: 2ace88c1-d757-40a7-8158-c1d3f5ff0511
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bf5f98d4eddf7daa6099b97d805a50c59902572c
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47537099"
---
# <a name="createcsharpmanifestresourcename-task"></a>CreateCSharpManifestResourceName タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[CreateCSharpManifestResourceName タスク](https://docs.microsoft.com/visualstudio/msbuild/createcsharpmanifestresourcename-task)します。  
  
  
指定した .resx ファイル名または他のリソースから [!INCLUDE[csprcs](../includes/csprcs-md.md)] スタイルのマニフェスト名を作成します。  
  
## <a name="parameters"></a>パラメーター  
 次の表では、[CreateCSharpManifestResourceName タスク](../msbuild/createcsharpmanifestresourcename-task.md) のパラメーターについて説明します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`ManifestResourceNames`|<xref:Microsoft.Build.Framework.ITaskItem> `[]` 型の読み取り専用出力パラメーターです。<br /><br /> 生成されたマニフェスト名です。|  
|`ResourceFiles`|必須の `String` 型のパラメーターです。<br /><br /> [!INCLUDE[csprcs](../includes/csprcs-md.md)] マニフェスト名の作成元のリソース ファイルの名前。|  
|`RootNamespace`|省略可能な `String` 型のパラメーターです。<br /><br /> 通常はプロジェクト ファイルから取得される、リソース ファイルのルート名前空間。 `null` でもかまいません。|  
|`PrependCultureAsDirectory`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、カルチャの名前がマニフェスト リソース名の直前にディレクトリ名として追加されます。 既定値は `true` です。|  
|`ResourceFilesWithManifestResourceNames`|省略可能な `String` 型の読み取り専用の出力パラメーターです。<br /><br /> マニフェスト リソース名を含むようになったリソース ファイルの名前を返します。|  
  
## <a name="remarks"></a>Remarks  
 [CreateVisualBasicManifestResourceName タスク](../msbuild/createvisualbasicmanifestresourcename-task.md)は、特定の .resx または他のリソース ファイルに割り当てる適切なマニフェスト リソース名を決定します。 このタスクは、リソース ファイルに論理名を提供した後、それをメタデータとして出力パラメーターにアタッチします。  
  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)



