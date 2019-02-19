---
title: RemoveDuplicates タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#RemoveDuplicates
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, RemoveDuplicates task
- RemoveDuplicates task [MSBuild]
ms.assetid: 481cbab6-73ff-488c-aba5-2c09f9eb1e04
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ac8198d32db511aa908f5fa11618d449012715d3
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54798139"
---
# <a name="removeduplicates-task"></a>RemoveDuplicates タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
指定されたアイテム コレクションから、重複するアイテムを削除します。  
  
## <a name="parameters"></a>パラメーター  
 `RemoveDuplicates` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`Filtered`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> すべての重複する項目が削除された項目コレクションが含まれます。|  
|`Inputs`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 重複した項目を削除する対象となる項目コレクションです。|  
  
## <a name="remarks"></a>解説  
 このタスクでは大文字と小文字が区別されず、重複の判断時、項目メタデータは比較されません。  
  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`RemoveDuplicates` タスクを使用し、`MyItems` 項目コレクションから重複項目を削除します。 タスクが完了すると、`FilteredItems` 項目コレクションに含まれる項目が 1 つになります。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <MyItems Include="MyFile.cs"/>  
        <MyItems Include="MyFile.cs">  
            <Culture>fr</Culture>  
        </MyItems>  
        <MyItems Include="myfile.cs"/>  
    </ItemGroup>  
  
    <Target Name="RemoveDuplicateItems">  
        <RemoveDuplicates  
            Inputs="@(MyItems)">  
            <Output  
                TaskParameter="Filtered"  
                ItemName="FilteredItems"/>  
        </RemoveDuplicates>  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>参照  
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)   
 [MSBuild の概念](../msbuild/msbuild-concepts.md)   
 [タスク](../msbuild/msbuild-tasks.md)
