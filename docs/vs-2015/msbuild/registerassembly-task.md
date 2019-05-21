---
title: RegisterAssembly タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#RegisterAssembly
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, RegisterAssembly task
- RegisterAssembly task [MSBuild]
ms.assetid: ba5f19ac-6764-4d28-9b79-a86de58f8987
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 71ef27b61e162fedbf0b8fcaac38d93bedbc77c1
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65682401"
---
# <a name="registerassembly-task"></a>RegisterAssembly タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定されたアセンブリに含まれるメタデータを読み込み、必要なエントリをレジストリに追加します。このため、COM クライアントは特別な処理を必要とすることなく [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] クラスを作成できます。 このタスクの動作は、完全に同じではありませんが、[Regasm.exe (アセンブリ登録ツール)](https://msdn.microsoft.com/library/e190e342-36ef-4651-a0b4-0e8c2c0281cb) の動作に似ています。  
  
## <a name="parameters"></a>パラメーター  
 `RegisterAssembly` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`Assemblies`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> COM に登録するアセンブリを指定します。|  
|`AssemblyListFile`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> `RegisterAssembly` タスクと [UnregisterAssembly](../msbuild/unregisterassembly-task.md) タスクの間の状態に関する情報が含まれます。 これにより、`RegisterAssembly` タスクで登録に失敗したアセンブリを `UnregisterAssembly` タスクで登録解除しようとすることを防止できます。|  
|`CreateCodeBase`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` に設定すると、レジストリに Codebase エントリが作成されます。Codebase エントリは、グローバル アセンブリ キャッシュにインストールされていないアセンブリのファイル パスを指定するものです。 登録しようとしているアセンブリを、後でグローバル アセンブリ キャッシュにインストールする場合は、このオプションを指定する必要はありません。|  
|`TypeLibFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 指定したアセンブリから生成するタイプ ライブラリを指定します。 生成されるタイプ ライブラリには、アセンブリ内で定義されているアクセス可能なタイプが格納されます。 タイプ ライブラリは、以下のいずれかの条件を満たす場合にだけ作成されます。<br /><br /> - 指定の場所に、同じ名前のタイプ ライブラリが存在しない。<br />- タイプ ライブラリが存在するが、渡されたアセンブリよりも古い。<br /><br /> 渡されたアセンブリよりもタイプ ライブラリの方が新しい場合、新しいタイプ ライブラリは作成されませんが、アセンブリの登録は行われます。<br /><br /> このパラメーターを指定する場合には、`Assemblies` パラメーターに指定したアイテムと同じ数のアイテムを指定する必要があります。数が異なると、タスクは失敗します。 指定しなかった場合には、既定でアセンブリの名前が使用され、アイテムの拡張子は .tlb に変更されます。|  
  
## <a name="remarks"></a>解説  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 `RegisterAssembly` タスクを使用して、`MyAssemblies` アイテム コレクションで指定されたアセンブリを登録する例を次に示します。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <MyAssemblies Include="MyAssembly.dll" />  
    <ItemGroup>  
  
    <Target Name="RegisterAssemblies">  
        <RegisterAssembly  
            Assemblies="@(MyAssemblies)" >  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>関連項目  
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
