---
title: MSBuild インライン タスク | Microsoft Docs
ms.date: 09/21/2017
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, tasks
ms.assetid: e72e6506-4a11-4edf-ae8d-cfb5a3b9d8a0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 37597d1e1f4fde2b2e81e7aa7868c0aaff935337
ms.sourcegitcommit: 59e5758036223ee866f3de5e3c0ab2b6dbae97b6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2019
ms.locfileid: "68416856"
---
# <a name="msbuild-inline-tasks"></a>MSBuild インライン タスク
MSBuild タスクは通常、<xref:Microsoft.Build.Framework.ITask> インターフェイスを実装するクラスをコンパイルして作成します。 詳細については、[タスク](../msbuild/msbuild-tasks.md)に関する記事を参照してください。

 .NET Framework Version 4 以降では、プロジェクト ファイルでタスクをインラインで作成できます。 個別のアセンブリを作成してタスクをホストする必要はありません。 これにより、ソース コードの追跡やタスクの配置が簡単になります。 ソース コードはスクリプトに統合されます。

 MSBuild 15.8 では、[RoslynCodeTaskFactory](../msbuild/msbuild-roslyncodetaskfactory.md) が追加され、.NET Standard クロスプラット フォーム インライン タスクを作成できるようになりました。  .NET Core 上でインライン タスクを使用する必要がある場合は、RoslynCodeTaskFactory を使用しなければなりません。
## <a name="the-structure-of-an-inline-task"></a>インライン タスクの構造
 インライン タスクは [UsingTask](../msbuild/usingtask-element-msbuild.md) 要素に格納されます。 インライン タスクとそれを格納する `UsingTask` 要素は通常、 *.targets* ファイルに含められ、必要に応じて他のプロジェクト ファイルにインポートされます。 基本的なインライン タスクの例を次に示します。 このタスクでは何も実行されないことに注意してください。

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <!-- This simple inline task does nothing. -->
  <UsingTask
    TaskName="DoNothing"
    TaskFactory="CodeTaskFactory"
    AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.Core.dll" >
    <ParameterGroup />
    <Task>
      <Reference Include="" />
      <Using Namespace="" />
      <Code Type="Fragment" Language="cs">
      </Code>
    </Task>
  </UsingTask>
</Project>
```

 この例の `UsingTask` 要素には、タスクとそれをコンパイルするインライン タスク ファクトリを記述した 3 つの属性が含まれています。

- `TaskName` 属性は、タスクの名前を指定します。この例では `DoNothing` と指定しています。

- `TaskFactory` 属性は、インライン タスク ファクトリを実装するクラスの名前を指定します。

- `AssemblyFile` 属性は、インライン タスク ファクトリの場所を指定します。 代わりに、`AssemblyName` 属性を使用してインライン タスク ファクトリ クラスの完全修飾名を指定することもできます。これは通常、グローバル アセンブリ キャッシュ (GAC: Global Assembly Cache) に配置されます。

`DoNothing` タスクの残りの要素は空になっていますが、ここではインライン タスクの順序と構造を示すために含めてあります。 具体的な例については、この後の例を参照してください。

- `ParameterGroup` 要素は省略可能です。 指定する場合は、タスクのパラメーターを宣言します。 入力パラメーターと出力パラメーターの詳細については、この後の「[入力パラメーターと出力パラメーター](#input-and-output-parameters)」を参照してください。

- `Task` 要素にはタスクのソース コードを記述して格納します。

- `Reference` 要素は、コードで使用する .NET アセンブリへの参照を指定します。 これは、Visual Studio でプロジェクトに参照を追加することに相当します。 `Include` 属性は参照アセンブリのパスを指定します。

- `Using` 要素には、アクセスする名前空間をリストします。 これは、Visual C# の `Using` ステートメントに似ています。 `Namespace` 属性は、含める名前空間を指定します。

`Reference` 要素と `Using` 要素は言語に依存しません。 インライン タスクは、サポートされているどの .NET CodeDom 言語 (Visual Basic や Visual C# など) でも記述できます。

> [!NOTE]
> `Task` 要素に含まれる要素はタスク ファクトリによって異なります。この例では、コード タスク ファクトリが格納されています。

### <a name="code-element"></a>コード要素
 `Task` 要素内の最後の子要素は `Code` 要素です。 `Code` 要素では、タスクにコンパイルするコードを記述するか参照します。 `Code` 要素に含める内容は、タスクを記述する方法に応じて異なります。

 `Language` 属性は、コードを記述する言語を指定します。 指定できる値は、`cs` (C# の場合) または `vb` (Visual Basic の場合) です。

 `Type` 属性は、`Code` 要素内のコードの種類を指定します。

- `Type` の値が `Class` の場合、`Code` 要素には <xref:Microsoft.Build.Framework.ITask> インターフェイスから派生したクラスのコードが含まれます。

- `Type` の値が `Method` の場合、コードは `Execute` インターフェイスの <xref:Microsoft.Build.Framework.ITask> メソッドのオーバーライドを定義します。

- `Type` の値が `Fragment` の場合、コードは `Execute` メソッドの内容を定義します。ただし、シグネチャや `return` ステートメントは含まれません。

コード自体は通常、`<![CDATA[` マーカーと `]]>` マーカーの間に記述します。 コードは CDATA セクション内に記述するため、"\<" や ">" などの予約文字のエスケープを気にする必要はありません。

また、`Source` 要素の `Code` 属性を使用して、タスクのコードを含むファイルの場所を指定することもできます。 ソース ファイルのコードの種類は、`Type` 属性で指定された種類である必要があります。 `Source` 属性が指定されている場合、`Type` の既定値は `Class` です。 `Source` が指定されていない場合の既定値は `Fragment` です。

> [!NOTE]
> ソース ファイル内のタスク クラスを定義する場合は、クラス名が、対応する [UsingTask](../msbuild/usingtask-element-msbuild.md) 要素の `TaskName` 属性と一致する必要があります。

## <a name="helloworld"></a>HelloWorld
 具体的なインライン タスクの例を次に示します。 HelloWorld タスクは、既定のエラー ログ デバイスに "Hello, world!" と表示します。通常、既定のデバイスは、システム コンソールまたは Visual Studio の**出力**ウィンドウです。 この例の `Reference` 要素は、例を示す目的でのみ含めてあります。

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <!-- This simple inline task displays "Hello, world!" -->
  <UsingTask
    TaskName="HelloWorld"
    TaskFactory="CodeTaskFactory"
    AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.Core.dll" >
    <ParameterGroup />
    <Task>
      <Reference Include="System.Xml"/>
      <Using Namespace="System"/>
      <Using Namespace="System.IO"/>
      <Code Type="Fragment" Language="cs">
<![CDATA[
// Display "Hello, world!"
Log.LogError("Hello, world!");
]]>
      </Code>
    </Task>
  </UsingTask>
</Project>
```

 HelloWorld タスクを *HelloWorld.targets* という名前のファイルに保存すると、次のようにしてプロジェクトから呼び出すことができます。

```xml
<Project ToolsVersion="15.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Import Project="HelloWorld.targets" />
  <Target Name="Hello">
    <HelloWorld />
  </Target>
</Project>
```

## <a name="input-and-output-parameters"></a>入力パラメーターと出力パラメーター
 インライン タスクのパラメーターは、`ParameterGroup` 要素の子要素です。 どのパラメーターも、それを定義する要素の名前を受け取ります。 次のコードは、`Text` パラメーターを定義しています。

```xml
<ParameterGroup>
  <Text />
</ParameterGroup>
```

 パラメーターには、以下の 1 つ以上の属性を含めることができます。

- `Required` は省略可能な属性で、既定値は `false` です。 `true` の場合、そのパラメーターは必須で、タスクを呼び出す前に値を指定する必要があります。

- `ParameterType` は省略可能な属性で、既定値は `System.String` です。 System.Convert.ChangeType を使用して文字列との間で変換できる項目または値の完全修飾型に設定できます (つまり、外部タスクとの受け渡しが可能なすべての型)。

- `Output` は省略可能な属性で、既定値は `false` です。 `true` の場合、そのパラメーターの値を、Execute メソッドから戻る前に指定する必要があります。

たとえば、オブジェクトに適用された

```xml
<ParameterGroup>
  <Expression Required="true" />
  <Files ParameterType="Microsoft.Build.Framework.ITaskItem[]" Required="true" />
  <Tally ParameterType="System.Int32" Output="true" />
</ParameterGroup>
```

この例では、以下の 3 つのパラメーターを定義しています。

- `Expression` は、System.String 型の必須の入力パラメーターです。

- `Files` は、必須の項目リスト入力パラメーターです。

- `Tally` は、System.Int32 型の出力パラメーターです。

`Code` 要素の `Type` 属性が `Fragment` または `Method` の場合、すべてのパラメーターに対して自動的にプロパティが作成されます。 それ以外の場合は、タスクのソース コードで明示的にプロパティを宣言する必要があります。プロパティはパラメーター定義と完全に一致している必要があります。

## <a name="example"></a>例
 指定されたファイル内のすべてのトークンを指定された値に置き換えるインライン タスクの例を次に示します。

```xml
<Project xmlns='http://schemas.microsoft.com/developer/msbuild/2003' ToolsVersion="15.0">

  <UsingTask TaskName="TokenReplace" TaskFactory="CodeTaskFactory" AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.Core.dll">
    <ParameterGroup>
      <Path ParameterType="System.String" Required="true" />
      <Token ParameterType="System.String" Required="true" />
      <Replacement ParameterType="System.String" Required="true" />
    </ParameterGroup>
    <Task>
      <Code Type="Fragment" Language="cs"><![CDATA[
string content = File.ReadAllText(Path);
content = content.Replace(Token, Replacement);
File.WriteAllText(Path, content);

]]></Code>
    </Task>
  </UsingTask>

  <Target Name='Demo' >
    <TokenReplace Path="C:\Project\Target.config" Token="$MyToken$" Replacement="MyValue"/>
  </Target>
</Project>
```

## <a name="see-also"></a>関連項目
- [タスク](../msbuild/msbuild-tasks.md)
- [チュートリアル: インライン タスクを作成する](../msbuild/walkthrough-creating-an-inline-task.md)
