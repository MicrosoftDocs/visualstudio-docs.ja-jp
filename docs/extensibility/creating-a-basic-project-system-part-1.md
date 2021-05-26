---
title: 基本的なプロジェクト システムの作成、パート 1 | Microsoft Docs
description: extension.myproj という名前のプロジェクト タイプを作成する方法を説明します。 Visual Studio では、プロジェクトはソースコードファイルやその他のアセットを整理するために使用されるコンテナーです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: 882a10fa-bb1c-4b01-943a-7a3c155286dd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 15d28ff154629d07c643430b210d6106ac99978c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089434"
---
# <a name="create-a-basic-project-system-part-1"></a>基本的なプロジェクト システムの作成、パート 1
Visual Studio でプロジェクトとは、ソース コード ファイルやその他のアセットを整理するために開発者が使用するコンテナーです。 **ソリューション エクスプローラー** でプロジェクトは、ソリューションの子として表示されます。 プロジェクトを使用すると、ソース コードの整理、ビルド、デバッグ、およびデプロイを実行したり、Web サービス、データベース、その他のリソースへの参照を作成したりすることができます。

 プロジェクトは、プロジェクト ファイル (Visual C# プロジェクトでは *.csproj* ファイル、など) で定義されます。 独自のプロジェクト ファイル名拡張子を持つ、独自のプロジェクト タイプを作成できます。 プロジェクト タイプの詳細については、「[プロジェクト タイプ](../extensibility/internals/project-types.md)」を参照してください。

> [!NOTE]
> カスタム プロジェクト タイプで Visual Studio を拡張する必要がある場合は、[Visual studio プロジェクトシステム](https://github.com/Microsoft/VSProjectSystem) (.vsps) を活用することを強くお勧めします。このシステムには、プロジェクト システムをゼロから構築するよりも多くの利点があります。
>
> - オンボードが容易になります。  基本的なプロジェクト システムにも、数万行のコードが必要です。  VSPS を活用すると、オンボード コストを数クリックまでに減らした後、自分のニーズに合わせてカスタマイズすることができます。
> - メンテナンスが容易になります。  VSPS を活用すると、必要な作業が、自分のシナリオを維持することだけになります。  VSPS が、すべてのプロジェクト システム インフラストラクチャの保守を処理します。
>
>   Visual Studio 2013 よりも前のバージョンの Visual Studio を対象とする必要がある場合、Visual Studio 拡張機能では VSPS を活用できません。  その場合は、このチュートリアルで対処を開始することをお勧めします。

 このチュートリアルでは、プロジェクト ファイル名拡張子が *myproj* であるプロジェクト タイプを作成する方法を説明します。 このチュートリアルでは、既存の Visual C# プロジェクト システムの例を使用します。

> [!NOTE]
> 拡張機能プロジェクトのその他の例については、[VSSDK のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)に関するページを参照してください。

 このチュートリアルでは、次のタスクを実行する方法を説明します。

- 基本的なプロジェクト タイプを作成する。

- 基本的なプロジェクト テンプレートを作成する。

- プロジェクト テンプレートを Visual Studio に登録する。

- **[新しいプロジェクト]** ダイアログ ボックスを開き、テンプレートを使用してプロジェクト インスタンスを作成する。

- プロジェクト システムのプロジェクト ファクトリを作成する。

- プロジェクト システムのプロジェクト ノードを作成する。

- プロジェクト システムのカスタム アイコンを追加する。

- 基本的なテンプレート パラメーターの代入を実装する。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

 また、[プロジェクトのマネージド パッケージ フレームワーク](https://github.com/tunnelvisionlabs/MPFProj10)のソース コードをダウンロードすることも必要です。 作成するソリューションがアクセスできる場所にファイルを抽出します。

## <a name="create-a-basic-project-type"></a>基本的なプロジェクト タイプを作成する
 **SimpleProject** という名前の C# VSIX プロジェクトを作成します ( **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** をクリックした後、 **[Visual C#]**  >  **[機能拡張]**  >  **[VSIX プロジェクト]** をクリックします)。 Visual Studio パッケージ プロジェクト項目テンプレートを追加します (**ソリューション エクスプローラー** でプロジェクト ノードを右クリックし、 **[追加]**  >  **[新しい項目]** を選択した後、 **[機能拡張]**  >  **[Visual Studio パッケージ]** に移動します)。 ファイルに、*SimpleProjectPackage* という名前を付けます。

## <a name="creating-a-basic-project-template"></a>基本的なプロジェクト テンプレートを作成する
 ここで、この基本的な VSPackage を変更して、新しい *.myproj* プロジェクト タイプを実装することができます。 *.myproj* プロジェクト タイプに基づくプロジェクトを作成するためには、新しいプロジェクトに追加するファイル、リソース、および参照を Visual Studio が認識している必要があります。 この情報を提供するには、プロジェクト ファイルをプロジェクト テンプレート フォルダーに配置します。 ユーザーが *.myproj* プロジェクトを使用してプロジェクトを作成すると、このファイルは、新しいプロジェクトにコピーされます。

### <a name="to-create-a-basic-project-template"></a>基本的なプロジェクト テンプレートを作成するには

1. *Templates\Projects\SimpleProject* という階層構造で、この 3 つのフォルダーをプロジェクトに追加します (**ソリューション エクスプローラー** で **SimpleProject** プロジェクト ノードを右クリックし、 **[追加]** をポイントしてから、 **[新しいフォルダー]** をクリックします。 フォルダーに、*Templates* という名前を付けます。 *Templates* フォルダーに、*Projects* という名前のフォルダーを追加します。 *Projects* フォルダーに、*SimpleProject* という名前のフォルダーを追加します)。

2. *Templates\Projects\SimpleProject* フォルダーに、*SimpleProject.ico* という名前のアイコンとして使用するビットマップ イメージ ファイルを追加します。 **[追加]** をクリックすると、アイコン エディターが開きます。

3. 特徴的なアイコンにします。 このアイコンは、このチュートリアルの後半の **[新しいプロジェクト]** ダイアログ ボックスに表示されます。

    ![単純なプロジェクト アイコン](../extensibility/media/simpleprojicon.png "SimpleProjIcon")

4. アイコンを保存し、アイコン エディターを終了します。

5. *Templates\Projects\SimpleProject* フォルダーに、*Program.cs* という名前の **クラス** 項目を追加します。

6. 既存のコードを、次の行に置き換えます。

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Text;

   namespace $nameSpace$
   {
       public class $className$
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Hello VSX!!!");
               Console.ReadKey();
           }
       }
   }
   ```

   > [!IMPORTANT]
   > これは、最終形式の *Program.cs* コードではありません。置換パラメーターについては、後の手順で説明します。 コンパイル エラーが発生する場合がありますが、ファイルの **[ビルド アクション]** が **[コンテンツ]** である限り、通常どおりにプロジェクトをビルドし、実行できます。

7. ファイルを保存します。

8. *Properties* フォルダーから *Projects\SimpleProject* フォルダーに *AssemblyInfo* ファイルをコピーします。

9. *Projects\SimpleProject* フォルダーに、*SimpleProject. myproj* という名前の XML ファイルを追加します。

   > [!NOTE]
   > このタイプのすべてのプロジェクトのファイル名拡張子は *.myproj* です。 これを変更する場合は、このチュートリアル内で出現するすべての場所で変更する必要があります。

10. 既存のコンテンツを、次の行に置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <SchemaVersion>2.0</SchemaVersion>
        <ProjectGuid></ProjectGuid>
        <OutputType>Exe</OutputType>
        <RootNamespace>MyRootNamespace</RootNamespace>
        <AssemblyName>MyAssemblyName</AssemblyName>
        <EnableUnmanagedDebugging>false</EnableUnmanagedDebugging>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
        <DebugSymbols>true</DebugSymbols>
        <OutputPath>bin\Debug\</OutputPath>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
        <DebugSymbols>false</DebugSymbols>
        <OutputPath>bin\Release\</OutputPath>
      </PropertyGroup>
      <ItemGroup>
        <Reference Include="mscorlib" />
        <Reference Include="System" />
        <Reference Include="System.Data" />
        <Reference Include="System.Xml" />
      </ItemGroup>
      <ItemGroup>
        <Compile Include="AssemblyInfo.cs">
          <SubType>Code</SubType>
        </Compile>
        <Compile Include="Program.cs">
          <SubType>Code</SubType>
        </Compile>
      </ItemGroup>
      <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
    </Project>
    ```

11. ファイルを保存します。

12. **[プロパティ]** ウィンドウで、*AssemblyInfo.cs*、*Program.cs*、*SimpleProject.ico*、および *SimpleProject.myproj* の **[ビルド アクション]** を **[コンテンツ]** に設定し、 **[VSIX に含める]** プロパティを **[True]** に設定します。

    このプロジェクト テンプレートには、デバッグ構成とリリース構成の両方を含む基本的な Visual C# プロジェクトが記述されています。 プロジェクトには、*AssemblyInfo.cs* と *Program.cs* の 2 つのソース ファイルと、いくつかのアセンブリ参照が含まれています。 プロジェクトがテンプレートから作成されると、ProjectGuid 値が自動的に、新しい GUID に置き換えられます。

    **ソリューション エクスプローラー** では、展開された **Templates** フォルダーが、次のように表示されます。

```
Templates
   Projects
      SimpleProject
         AssemblyInfo.cs
         Program.cs
         SimpleProject.ico
         SimpleProject.myproj
```

## <a name="create-a-basic-project-factory"></a>基本的なプロジェクト ファクトリを作成する
 プロジェクト テンプレート フォルダーの場所を Visual Studio に通知する必要があります。 これを行うには、プロジェクト ファクトリを実装する VSPackage クラスに属性を追加して、VSPackage のビルド時にテンプレートの場所がシステム レジストリに書き込まれるようにします。 まず、プロジェクト ファクトリ GUID で識別される基本的なプロジェクト ファクトリを作成します。 <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> 属性を使用してプロジェクト ファクトリを `SimpleProjectPackage` クラスに接続します。

### <a name="to-create-a-basic-project-factory"></a>基本的なプロジェクト ファクトリを作成するには

1. プロジェクト ファクトリの GUID を作成 ( **[ツール]** メニューの **[GUID の作成]** をクリック) するか、次の例でいずれかを使用します。 `PackageGuidString` が既に定義されているセクションの近くで、GUID を `SimpleProjectPackage` クラスに追加 します。 GUID は、GUID 形式と文字列形式の両方である必要があります。 その結果、次の例のようなコードになります。

   ```csharp
       public sealed class SimpleProjectPackage : Package
       {
           ...
           public const string SimpleProjectPkgString = "96bf4c26-d94e-43bf-a56a-f8500b52bfad";
           public const string SimpleProjectFactoryString = "471EC4BB-E47E-4229-A789-D1F5F83B52D4";

           public static readonly Guid guidSimpleProjectFactory = new Guid(SimpleProjectFactoryString);
       }
   ```

2. 一番上の *SimpleProject* フォルダーに、*SimpleProjectFactory.cs* という名前のファイルを追加します。

3. ディレクティブを使用して以下を追加します。

   ```csharp
   using System.Runtime.InteropServices;
   using Microsoft.VisualStudio.Shell;
   ```

4. `SimpleProjectFactory` クラスに GUID 属性を追加します。 属性の値が、新しいプロジェクト ファクトリ GUID です。

   ```csharp
   [Guid(SimpleProjectPackage.SimpleProjectFactoryString)]
   class SimpleProjectFactory
   {
   }
   ```

   これで、プロジェクト テンプレートを登録することができます。

### <a name="to-register-the-project-template"></a>プロジェクト テンプレートを登録するには

1. *Simpleprojectpackage.cs* で、次のように、<xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> 属性を `SimpleProjectPackage` クラスに追加します。

   ```csharp
   [ProvideProjectFactory(    typeof(SimpleProjectFactory),     "Simple Project",
       "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
       @"Templates\Projects\SimpleProject",     LanguageVsTemplate = "SimpleProject")]
   [Guid(SimpleProjectPackage.PackageGuidString)]
   public sealed class SimpleProjectPackage : Package
   ```

2. ソリューションを再ビルドし、エラーが発生することなくソリューションがビルドされることを確認します。

    再ビルドすると、プロジェクト テンプレートが登録されます。

   パラメーター、`defaultProjectExtension` および `possibleProjectExtensions` は、プロジェクトのファイル名拡張子 ( *.myproj*) に設定されます。 `projectTemplatesDirectory` パラメーターは、*Templates* フォルダーの相対パスに設定されます。 ビルド中に、このパスが完全ビルドに変換され、レジストリに追加されてプロジェクト システムが登録されます。

## <a name="test-the-template-registration"></a>テンプレートの登録をテストする
 テンプレートを登録すると、プロジェクト テンプレート フォルダーの場所が Visual Studio に指示され、Visual Studio が **[新しいプロジェクト]** ダイアログボックスにテンプレート名とアイコンを表示できるようになります。

### <a name="to-test-the-template-registration"></a>テンプレートの登録をテストするには

1. **F5** キーを押して、Visual Studio の実験用インスタンスのデバッグを開始します。

2. 実験用インスタンスで、新しく作成したプロジェクト タイプの新しいプロジェクトを作成します。 **[新しいプロジェクト]** ダイアログ ボックスで、 **[インストールされたテンプレート]** の下に **SimpleProject** が表示されます。

   これで、プロジェクト ファクトリが登録されました。 ただし、まだ、これでプロジェクトを作成することはできません。 プロジェクト パッケージとプロジェクト ファクトリが連携することにより、プロジェクトが作成され、初期化されます。

## <a name="add-the-managed-package-framework-code"></a>マネージド パッケージ フレームワーク コードを追加する
 プロジェクト パッケージとプロジェクト ファクトリの間の接続を実装します。

- マネージド パッケージ フレームワークのソースコード ファイルをインポートします。

    1. SimpleProject プロジェクトをアンロード (**ソリューション エクスプローラー** でプロジェクト ノードを選択し、コンテキスト メニューの **[プロジェクトのアンロード]** をクリック) し、XML エディターでプロジェクト ファイルを開きます。

    2. 次のブロックをプロジェクト ファイル (\<Import> ブロックのすぐ上) に追加します。 ダウンロードしたマネージド パッケージ フレームワーク コードで、*ProjectBase.files* ファイルの場所を `ProjectBasePath` に設定します。 場合によっては、パス名に円記号を追加する必要があります。 そうしないと、マネージド パッケージ フレームワークのソース コードをプロジェクトが見つけることができない可能性があります。

        ```
        <PropertyGroup>
             <ProjectBasePath>your path here\</ProjectBasePath>
             <RegisterWithCodebase>true</RegisterWithCodebase>
          </PropertyGroup>
          <Import Project="$(ProjectBasePath)\ProjectBase.Files" />
        ```

        > [!IMPORTANT]
        > この場合は、パスの末尾に円記号を必ず付けてください。

    3. プロジェクトを再度読み込みます。

    4. 次のアセンブリへの参照を追加します。

        - `Microsoft.VisualStudio.Designer.Interfaces` ( *\<VSSDK install>\VisualStudioIntegration\Common\Assemblies\v2.0* 内)

        - `WindowsBase`

        - `Microsoft.Build.Tasks.v4.0`

### <a name="to-initialize-the-project-factory"></a>プロジェクト ファクトリを初期化するには

1. *SimpleProjectPackage.cs* ファイルで、次の `using` ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

2. `Microsoft.VisualStudio.Package.ProjectPackage` から `SimpleProjectPackage` クラスを派生させます。

    ```csharp
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

3. プロジェクト テンプレートを登録します。 次の行を、`SimpleProjectPackage.Initialize` メソッドの `base.Initialize` の直後に追加します。

    ```csharp
    base.Initialize();
    this.RegisterProjectFactory(new SimpleProjectFactory(this));
    ```

4. 抽象プロパティ `ProductUserContext` を実装します。

    ```csharp
    public override string ProductUserContext
        {
            get { return ""; }
    }
    ```

5. *SimpleProjectFactory.cs* で、既存の `using` ディレクティブの後に次の `using` ディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

6. `ProjectFactory` から `SimpleProjectFactory` クラスを派生させます。

    ```csharp
    class SimpleProjectFactory : ProjectFactory
    ```

7. 次のダミー メソッドを `SimpleProjectFactory` クラスに追加します。 このメソッドは、後のセクションで実装します。

    ```csharp
    protected override ProjectNode CreateProject()
    {
        return null;
    }
    ```

8. 次のフィールドとコンストラクターを `SimpleProjectFactory` クラスに追加します。 この `SimpleProjectPackage` 参照は、プライベート フィールドにキャッシュされ、サービス プロバイダー サイトの設定に使用できます。

    ```csharp
    private SimpleProjectPackage package;

    public SimpleProjectFactory(SimpleProjectPackage package)
        : base(package)
    {
        this.package = package;
    }
    ```

9. ソリューションを再ビルドし、エラーが発生することなくソリューションがビルドされることを確認します。

## <a name="test-the-project-factory-implementation"></a>プロジェクト ファクトリの実装をテストする
 プロジェクト ファクトリの実装のコンストラクターが呼び出されているかどうかをテストします。

### <a name="to-test-the-project-factory-implementation"></a>プロジェクト ファクトリの実装をテストするには

1. *SimpleProjectFactory.cs* ファイルで、`SimpleProjectFactory` コンストラクターの次の行にブレークポイントを設定し ます。

    ```csharp
    this.package = package;
    ```

2. **F5** キーを押して、Visual Studio の実験用インスタンスを起動します。

3. 実験用インスタンスで、新しいプロジェクトの作成を開始します。 **[新しいプロジェクト]** ダイアログ ボックスで、**SimpleProject** プロジェクト タイプを選択し、 **[OK]** をクリックします。 ブレークポイントで実行が停止します。

4. ブレークポイントをクリアし、デバッグを停止します。 プロジェクト ノードをまだ作成していないため、プロジェクト作成コードでは、依然として例外がスローされます。

## <a name="extend-the-projectnode-class"></a>ProjectNode クラスを拡張する
 ここで、`ProjectNode` クラスから派生した `SimpleProjectNode` クラスを実装できます。 `ProjectNode` 基底クラスは、プロジェクト作成の次のタスクを処理します。

- プロジェクト テンプレート ファイル *SimpleProject.myproj* を、新しいプロジェクト フォルダーにコピーします。 **[新しいプロジェクト]** ダイアログ ボックスに入力された名前に従って、コピーの名前が変更されます。 `ProjectGuid` プロパティ値は、新しい GUID に置き換えられます。

- プロジェクト テンプレート ファイル *SimpleProject.myproj* の MSBuild 要素を走査し、`Compile` 要素を検索します。 `Compile` ターゲット ファイルごとに、新しいプロジェクト フォルダーにこのファイルがコピーされます。

  派生した `SimpleProjectNode` クラスは、次のタスクを処理します。

- **ソリューション エクスプローラー** 内のプロジェクト ノードとファイル ノードのアイコンを作成するか、選択することができるようにします。

- 追加のプロジェクト テンプレート パラメーターの代入を指定できるようにします。

### <a name="to-extend-the-projectnode-class"></a>ProjectNode クラスを拡張するには

1. `SimpleProjectNode.cs`という名前のクラスを追加します。

2. 既存のコードを次のコードに置き換えます。

   ```csharp
   using System;
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Project;

   namespace SimpleProject
   {
       public class SimpleProjectNode : ProjectNode
       {
           private SimpleProjectPackage package;

           public SimpleProjectNode(SimpleProjectPackage package)
           {
               this.package = package;
           }
           public override Guid ProjectGuid
           {
               get { return SimpleProjectPackage.guidSimpleProjectFactory; }
           }
           public override string ProjectType
           {
               get { return "SimpleProjectType"; }
           }

           public override void AddFileFromTemplate(
               string source, string target)
           {
               this.FileTemplateProcessor.UntokenFile(source, target);
               this.FileTemplateProcessor.Reset();
           }
       }
   }
   ```

   この `SimpleProjectNode` クラスの実装には、オーバーライドされた次のメソッドがあります。

- `ProjectGuid`。プロジェクト ファクトリ GUID を返します。

- `ProjectType`。プロジェクト タイプのローカライズされた名前を返します。

- `AddFileFromTemplate`。選択したファイルをテンプレート フォルダーからコピー先プロジェクトにコピーします。 このメソッドは、後のセクションでさらに実装されます。

  `SimpleProjectNode` コンストラクターは、`SimpleProjectFactory` コンストラクターと同様に、後で使用するためにプライベート フィールドに `SimpleProjectPackage` 参照をキャッシュします。

  `SimpleProjectFactory` クラスを `SimpleProjectNode` クラスに接続するには、新しい `SimpleProjectNode` を `SimpleProjectFactory.CreateProject` メソッドでインスタンス化し、後で使用できるようにプライベート フィールドにキャッシュする必要があります。

### <a name="to-connect-the-project-factory-class-and-the-node-class"></a>プロジェクト ファクトリ クラスとノード クラスを接続するには

1. *SimpleProjectFactory.cs* ファイルで、次の `using` ディレクティブを追加します。

    ```csharp
    using IOleServiceProvider =    Microsoft.VisualStudio.OLE.Interop.IServiceProvider;
    ```

2. 次のコードを使用して `SimpleProjectFactory.CreateProject` メソッドを置き換えます。

    ```csharp
    protected override ProjectNode CreateProject()
    {
        SimpleProjectNode project = new SimpleProjectNode(this.package);

        project.SetSite((IOleServiceProvider)        ((IServiceProvider)this.package).GetService(            typeof(IOleServiceProvider)));
        return project;
    }
    ```

3. ソリューションを再ビルドし、エラーが発生することなくソリューションがビルドされることを確認します。

## <a name="test-the-projectnode-class"></a>ProjectNode クラスをテストする
 プロジェクト ファクトリをテストして、プロジェクトの階層が作成されるかどうかを調べます。

### <a name="to-test-the-projectnode-class"></a>ProjectNode クラスをテストするには

1. **F5** キーを押してデバッグを開始します。 実験用インスタンスで、新しい SimpleProject を作成します。

2. Visual Studio では、プロジェクトを作成するためにプロジェクト ファクトリを呼び出す必要があります。

3. Visual Studio の実験用インスタンスを終了します。

## <a name="add-a-custom-project-node-icon"></a>カスタム プロジェクト ノードのアイコンを追加する
 前のセクションのプロジェクト ノードのアイコンは、既定のアイコンです。 これを、カスタム アイコンに変更できます。

### <a name="to-add-a-custom-project-node-icon"></a>カスタム プロジェクト ノードのアイコンを追加するには

1. **Resources** フォルダーに、*SimpleProjectNode.bmp* という名前のビットマップ ファイルを追加します。

2. **[プロパティ]** ウィンドウで、ビットマップを 16 x 16 ピクセルに縮小します。 特徴的なビットマップにします。

    ![単純なプロジェクト Comm](../extensibility/media/simpleprojprojectcomm.png "SimpleProjProjectComm")

3. **[プロパティ]** ウィンドウで、ビットマップの **[ビルド アクション]** を **[埋め込みリソース]** に変更します。

4. *SimpleProjectNode.cs* で、次の `using` ディレクティブを追加します。

   ```csharp
   using System.Drawing;
   using System.Windows.Forms;
   ```

5. 次の静的フィールドおよびコンストラクターを `SimpleProjectNode` クラスに追加します。

   ```csharp
   private static ImageList imageList;

   static SimpleProjectNode()
   {
       imageList =        Utilities.GetImageList(            typeof(SimpleProjectNode).Assembly.GetManifestResourceStream(                "SimpleProject.Resources.SimpleProjectNode.bmp"));
   }
   ```

6. `SimpleProjectNode` クラスの先頭に次のコードを追加します。

   ```csharp
   internal static int imageIndex;
      public override int ImageIndex
      {
          get { return imageIndex; }
      }
   ```

7. インスタンス コンストラクターを次のコードに置き換えます。

   ```csharp
   public SimpleProjectNode(SimpleProjectPackage package)
   {
       this.package = package;

       imageIndex = this.ImageHandler.ImageList.Images.Count;

       foreach (Image img in imageList.Images)
       {
           this.ImageHandler.AddImage(img);
       }
   }
   ```

   静的構築時に `SimpleProjectNode` は、アセンブリ マニフェスト リソースからプロジェクト ノード ビットマップを取得し、後で使用できるようにプライベート フィールドにキャッシュします。 <xref:System.Reflection.Assembly.GetManifestResourceStream%2A> イメージ パスの構文に注意してください。 アセンブリに埋め込まれているマニフェスト リソースの名前を調べるには、<xref:System.Reflection.Assembly.GetManifestResourceNames%2A> メソッドを使用します。 このメソッドを `SimpleProject` アセンブリに適用すると、次のような結果になります。

- *SimpleProject.Resources.resources*

- *VisualStudio.Project.resources*

- *SimpleProject.VSPackage.resources*

- *Resources.imagelis.bmp*

- *Microsoft.VisualStudio.Project.DontShowAgainDialog.resources*

- *Microsoft.VisualStudio.Project.SecurityWarningDialog.resources*

- *SimpleProject.Resources.SimpleProjectNode.bmp*

  インスタンスの構築時に、`ProjectNode` 基底クラスは *Resources.imagelis.bmp* を読み込みます。これには、一般的に使用される、*Resources\imagelis.bmp* の 16 x 16 ビットマップが埋め込まれています。 このビットマップ リストは、`SimpleProjectNode` で `ImageHandler.ImageList` として使用できるようになります。 `SimpleProjectNode` により、プロジェクト ノードのビットマップがリストに追加されます。 イメージ リスト内のプロジェクト ノード ビットマップのオフセットは、後でパブリック `ImageIndex` プロパティの値として使用できるようにキャッシュされます。 Visual Studio では、このプロパティを使用して、プロジェクト ノード アイコンとして表示するビットマップを決定します。

## <a name="test-the-custom-project-node-icon"></a>カスタム プロジェクト ノードのアイコンをテストする
 プロジェクト ファクトリをテストして、カスタム プロジェクト ノードのアイコンを持つプロジェクト階層が作成されているかどうかを確認します。

### <a name="to-test-the-custom-project-node-icon"></a>カスタム プロジェクト ノードのアイコンをテストするには

1. デバッグを開始し、新しい SimpleProject を実験用インスタンスに作成します。

2. 新しく作成したプロジェクトでは、*SimpleProjectNode.bmp* がプロジェクト ノードのアイコンとして使用されています。

     ![単純なプロジェクト New Project ノード](../extensibility/media/simpleprojnewprojectnode.png "SimpleProjNewProjectNode")

3. コード エディターで *Program.cs* を開きます。 次のコードのようなソース コードが表示されます。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace $nameSpace$
    {
        public class $className$
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

     テンプレート パラメーター、$nameSpace$ および $className$ には、新しい値がありません。 次のセクションでは、テンプレート パラメーターの代入を実装する方法を説明します。

## <a name="substitute-template-parameters"></a>テンプレート パラメーターを代入する
 前のセクションでは、`ProvideProjectFactory` 属性を使用してプロジェクト テンプレートを Visual Studio に登録しました。 この方法でテンプレート フォルダーのパスを登録すると、`ProjectNode.AddFileFromTemplate` クラスをオーバーライドして展開することで、基本的なテンプレート パラメーターの代入を可能にすることができ ます。 詳細については、「[新しいプロジェクトの生成: 内部、パート 2](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)」を参照してください。

 ここで、`AddFileFromTemplate` クラスに置換コードを追加します。

### <a name="to-substitute-template-parameters"></a>テンプレート パラメーターを代入するには

1. *SimpleProjectNode.cs* ファイルで、次の `using` ディレクティブを追加します。

   ```csharp
   using System.IO;
   ```

2. 次のコードを使用して `AddFileFromTemplate` メソッドを置き換えます。

   ```csharp
   public override void AddFileFromTemplate(
       string source, string target)
   {
       string nameSpace =
           this.FileTemplateProcessor.GetFileNamespace(target, this);
       string className = Path.GetFileNameWithoutExtension(target);

       this.FileTemplateProcessor.AddReplace("$nameSpace$", nameSpace);
       this.FileTemplateProcessor.AddReplace("$className$", className);

       this.FileTemplateProcessor.UntokenFile(source, target);
       this.FileTemplateProcessor.Reset();
   }
   ```

3. メソッドの `className` 代入ステートメントの直後にブレークポイントを設定します。

   代入ステートメントによって、名前空間と新しいクラス名の合理的な値が決定されます。 2 つの `ProjectNode.FileTemplateProcessor.AddReplace` メソッド呼び出しにより、これらの新しい値を使用して、対応するテンプレート パラメーターの値が置き換えられます。

## <a name="test-the-template-parameter-substitution"></a>テンプレート パラメーターの代入をテストする
 ここでは、テンプレート パラメーターの代入をテストできます。

### <a name="to-test-the-template-parameter-substitution"></a>テンプレート パラメーターの代入をテストするには

1. デバッグを開始し、新しい SimpleProject を実験用インスタンスに作成します。

2. `AddFileFromTemplate` メソッド内のブレークポイントで実行が停止します。

3. `nameSpace` パラメーターと `className` パラメーターの値を調べます。

   - `nameSpace` には、 *\Templates\Projects\SimpleProject\SimpleProject.myproj* プロジェクト テンプレート ファイル内の \<RootNamespace> 要素の値が与えられます。 この場合、値は `MyRootNamespace` です。

   - `className` には、ファイル名拡張子のない、クラス ソース ファイル名の値が与えられます。 この場合、コピー先フォルダーにコピーされる最初のファイルは *AssemblyInfo.cs* です。したがって、className の値は `AssemblyInfo` になります。

4. ブレークポイントを削除し、**F5** キーを押して実行を継続します。

    Visual Studio でプロジェクトの作成が完了します。

5. コード エディターで *Program.cs* を開きます。 次のコードのようなソース コードが表示されます。

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;

   namespace MyRootNamespace
   {
       public class Program
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Hello VSX!!!");
               Console.ReadKey();
           }
       }
   }
   ```

    名前空間が `MyRootNamespace`、クラス名が `Program` になっています。

6. プロジェクトのデバッグを開始します。 新しいプロジェクトは、コンパイルし、実行し、コンソール ウィンドウに "Hello VSX!!!" を表示する必要があります。 コンソール ウィンドウに表示します。

    ![単純なプロジェクト コマンド](../extensibility/media/simpleprojcommand.png "SimpleProjCommand")

   お疲れさまでした。 基本的なマネージド プロジェクト システムが実装されました。
