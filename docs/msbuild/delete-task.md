---
title: Delete タスク | Microsoft Docs
description: MSBuild Delete タスクを使用して指定したファイルを削除する際のパラメーターと考慮事項について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/11/2020
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Delete
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Delete task [MSBuild]
- MSBuild, Delete task
ms.assetid: 916bb2e3-3017-4828-ae27-c0b5c99bbb48
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 09945306a2260bed5b264d380dcea745ff3f7c07
ms.sourcegitcommit: 8fb1500acb7e6314fbb6b78eada78ef5d61d39bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2021
ms.locfileid: "113280428"
---
# <a name="delete-task"></a>Delete タスク

指定されたファイルを削除します。

## <a name="parameters"></a>パラメーター

`Delete` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`DeletedFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 正常に削除されたファイルを指定します。|
|`Files`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 削除するファイルを指定します。|
|`TreatErrorsAsWarnings`|省略可能な `Boolean` 型のパラメーターです<br /><br /> `true` の場合、エラーは警告として記録されます。 既定値は `false` です。|

## <a name="remarks"></a>Remarks

上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

> [!WARNING]
> `Delete` タスクでワイルドカードを使用する場合は注意してください。 `$(SomeProperty)\**\*.*` や `$(SomeProperty)/**/*.*` などの式を使用すると、間違ったファイルを簡単に削除できます。プロパティが空の文字列に評価される場合は特に、`Files` パラメーターがドライブのルートに評価され、削除したいものよりもはるかに多く削除される場合があります。

## <a name="example"></a>例

次の例では、`DeleteDebugSymbolFile` ターゲットをビルドするときにファイル *ConsoleApp1.pdb* が削除されます。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
  </PropertyGroup>

    <PropertyGroup>
        <AppName>ConsoleApp1</AppName>
    </PropertyGroup>

    <Target Name="DeleteDebugSymbolFile">
        <Message Text="Deleting $(OutDir)$(AppName).pdb"/>
        <Delete Files="$(OutDir)$(AppName).pdb" />
    </Target>
  
</Project>

```

削除されたファイルを追跡する必要がある場合は、次のように、項目名を使用して `TaskParameter` を `DeletedFiles` に設定します。

```xml
      <Target Name="DeleteDebugSymbolFile">
        <Delete Files="$(OutDir)$(AppName).pdb" >
              <Output TaskParameter="DeletedFiles" ItemName="DeletedList"/>
        </Delete>
        <Message Text="Deleted files: '@(DeletedList)'"/>
    </Target>
```

`Delete` タスクでワイルドカードを直接使用する代わりに、削除するファイルの `ItemGroup` を作成し、それに対して `Delete` タスクを実行します。 ただし、`ItemGroup` は慎重に配置してください。 `ItemGroup` をプロジェクト ファイルの最上位レベルに配置すると、ビルドの開始前の早い段階で評価されるため、ビルド プロセスの一部としてビルドされたファイルは含まれません。 そのため、削除する項目のリストを作成する `ItemGroup` を、`Delete` タスクの近くのターゲットに配置します。 ドライブのルートから始まるパスを持つ項目リストを作成しないように、プロパティが空でないことを確認する条件を指定します。

`Delete` タスクはファイルを削除するためのものです。 ディレクトリを削除する場合は、[RemoveDir](removedir-task.md) を使用します。

`Delete` タスクには、読み取り専用ファイルを削除するオプションは用意されていません。 読み取り専用ファイルを削除するには、`Exec` タスクを使用して `del` コマンドまたは同等のものを実行し、適切なオプションを使用して読み取り専用ファイルの削除を有効にします。 コマンド ラインには長さの制限があるため、入力項目リストの長さに注意する必要があります。また、次の例のように、スペースを含むファイル名を処理するようにします。

```xml
<Target Name="DeleteReadOnly">
  <ItemGroup>
    <FileToDelete Include="read only file.txt"/>
  </ItemGroup>
  <Exec Command="del /F /Q &quot;@(FileToDelete)&quot;"/>
</Target>
```

一般に、ビルド スクリプトを作成するときは、削除が論理的に `Clean` 操作の一部であるかどうかを考慮します。 通常の `Clean` 操作の一部としてクリーニングするファイルを設定する必要がある場合は、それらを `@(FileWrites)` リストに追加すると、次の `Clean` で削除されます。 さらにカスタム処理が必要な場合は、ターゲットを定義し、属性 `BeforeTargets="Clean"` または `AfterTargets="Clean"` を設定して実行するように指定するか、`BeforeClean` または `AfterClean` ターゲットのカスタム バージョンを定義します。 「[ビルドのカスタマイズ](customize-your-build.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [RemoveDir タスク](removedir-task.md)
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
