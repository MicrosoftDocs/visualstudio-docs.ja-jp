---
title: GenerateTrustInfo タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateTrustInfo task
- GenerateTrustInfo task [MSBuild]
ms.assetid: 3ca60816-4bb0-4fef-ae43-ca0bfb63def3
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4f1cf52286de97980eb269c3b52055be4455c38d
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54790153"
---
# <a name="generatetrustinfo-task"></a>GenerateTrustInfo タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
基本マニフェスト、`TargetZone` パラメーター、および `ExcludedPermissions` パラメーターからアプリケーションの信頼を生成します。  
  
## <a name="parameters"></a>パラメーター  
 `GenerateTrustInfo` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`ApplicationDependencies`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 依存アセンブリを指定します。|  
|`BaseManifest`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> アプリケーションの信頼を生成する基本マニフェストを指定します。|  
|`ExcludedPermissions`|省略可能な `String` 型のパラメーターです。<br /><br /> ゾーンの既定のアクセス許可セットから除外する、セミコロンで区切られた 1 つまたは複数のアクセス許可 ID 値を指定します。|  
|`TargetZone`|省略可能な `String` 型のパラメーターです。<br /><br /> コンピューター ポリシーから取得される、ゾーンの既定のアクセス許可セットを指定します。|  
|`TrustInfoFile`|必須の <xref:Microsoft.Build.Framework.ITaskItem> 型の出力パラメーターです。<br /><br /> アプリケーション セキュリティ信頼情報が含まれるファイルを指定します。|  
  
## <a name="remarks"></a>コメント  
 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>「  
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
