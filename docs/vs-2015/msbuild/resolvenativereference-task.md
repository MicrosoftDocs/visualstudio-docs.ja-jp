---
title: ResolveNativeReference タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ResolveNativeReference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, ResolveNativeReference task
- ResolveNativeReference task [MSBuild]
ms.assetid: 56acd101-de77-4eec-92c6-f5c6d2187579
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 31de2c146accd71ae1606be62ab06fa368e7fb89
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54758549"
---
# <a name="resolvenativereference-task"></a>ResolveNativeReference タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
ネイティブ参照を解決します。 <xref:Microsoft.Build.Tasks.ResolveNativeReference> クラスを実行します。 このクラスは、.NET Framework インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません。  
  
## <a name="task-parameters"></a>タスク パラメーター  
 `ResolveNativeReference` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`AdditionalSearchPaths`|必須の [String](<!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  -->)`[]` 型のパラメーターです。<br /><br /> ネイティブ参照のアセンブリ ID を解決するための検索パスを取得または設定します。|  
|`ContainedComComponents`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> ネイティブ アセンブリの COM コンポーネントを取得または設定します。|  
|`ContainedLooseEtcFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> ネイティブ マニフェストに示されているルース Etc ファイルを取得または設定します。|  
|`ContainedLooseTlbFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> ネイティブ アセンブリの Loose .tlb ファイルを取得または設定します。|  
|`ContainedPrerequisiteAssemblies`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> マニフェストを使用する前に存在する必要があるアセンブリを取得または設定します。|  
|`ContainedTypeLibraries`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> ネイティブ アセンブリのタイプ ライブラリを取得または設定します。|  
|`ContainingReferenceFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 参照ファイルを取得または設定します。|  
|`NativeReferences`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> Win32 ネイティブ アセンブリ参照を取得または設定します。|  
  
## <a name="remarks"></a>解説  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
