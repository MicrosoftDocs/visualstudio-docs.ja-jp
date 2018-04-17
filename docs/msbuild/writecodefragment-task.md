---
title: WriteCodeFragment タスク | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.reviewer: ''
ms.suite: ''
ms.technology: msbuild
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, WriteCodeFragment task
- WriteCodeFragment task [MSBuild]
ms.assetid: 1d2514b4-5bef-43bb-bebe-496da8ef063c
caps.latest.revision: 5
author: Mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload:
- multiple
ms.openlocfilehash: 6d08d4499ba0fcdc044b7189abeb9de1716b7ba4
ms.sourcegitcommit: 3b692c9bf332b7b9150901e16daf99a64b599fee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/10/2018
---
# <a name="writecodefragment-task"></a>WriteCodeFragment タスク
指定された生成済みのコード片から一時コード ファイルを生成します。 ファイルは削除されません。  
  
## <a name="parameters"></a>パラメーター  
 `WriteCodeFragment` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`AssemblyAttributes`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 書き込む属性の説明です。 項目 `Include` 値は、属性の種類の完全名になります。たとえば、"System.AssemblyVersionAttribute" です。<br /><br /> 各メタデータはパラメーターの名前/値の組みになります。この種類は `String` である必要があります。 一部の属性では、位置指定コンストラクター引数のみ許可されます。 ただし、このような引数はあらゆる属性で使用できます。 位置指定コンストラクター引数を設定するには、"_Parameter1"、"_Parameter2" のようなメタデータ名を使用します。<br /><br /> パラメーターのインデックスをスキップすることはできません。|  
|`Language`|必須の `String` 型のパラメーターです。<br /><br /> 生成するコードの言語を指定します。<br /><br /> `Language` には、"C#" や "VisualBasic" など、CodeDom プロバイダーが利用できるあらゆる言語を指定できます。 出力ファイルには、その言語の既定のファイル名拡張子が与えられます。|  
|`OutputDirectory`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> 生成されたコードの出力先フォルダーを指定します。一般的には、中間フォルダーにします。|  
|`OutputFile`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型の出力パラメーターです。<br /><br /> 生成されたファイルのパスを指定します。 ファイル名を使用してこのパラメーターを設定する場合、出力先フォルダーがファイル名の前に付加されます。 ルートを使用して設定される場合、出力先フォルダーは無視されます。<br /><br /> このパラメーターが設定されない場合、出力ファイル名が出力先フォルダー、任意のファイル名、指定言語の既定のファイル名拡張子になります。|  
  
## <a name="remarks"></a>コメント  
 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)