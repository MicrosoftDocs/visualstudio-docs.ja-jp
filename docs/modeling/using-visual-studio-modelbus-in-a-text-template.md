---
title: テキスト テンプレートで ModelBus を使用する
description: Visual Studio ModelBus 参照を含むモデルを読み取るテキスト テンプレートを作成する場合に、ターゲット モデルにアクセスするための参照を解決する方法について説明します。
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0f65ece27122949fec006d73858c8c89483441f1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99924374"
---
# <a name="using-visual-studio-modelbus-in-a-text-template"></a>テキスト テンプレートでの Visual Studio ModelBus の使用

Visual Studio ModelBus 参照を含むモデルを読み取るテキスト テンプレートを作成する場合は、ターゲット モデルにアクセスするための参照を解決します。 その場合は、テキスト テンプレートと参照先のドメイン固有言語 (DSL) を調整する必要があります。

- 参照のターゲットである DSL には、テキスト テンプレートからアクセスできるように構成されている ModelBus アダプターが必要です。 他のコードからも DSL にアクセスする場合は、標準の ModelBus アダプターに加えて、再構成されたアダプターが必要です。

     アダプター マネージャーは [VsTextTemplatingModelingAdapterManager](/previous-versions/ee844317(v=vs.140)) から継承し、`[HostSpecific(HostName)]` 属性を持っている必要があります。

- このテンプレートは [ModelBusEnabledTextTransformation](/previous-versions/ee844263(v=vs.140)) から継承する必要があります。

> [!NOTE]
> ModelBus 参照を含まない DSL モデルを読み取る場合は、DSL プロジェクトで生成されたディレクティブ プロセッサを使用できます。 詳細については、「[テキスト テンプレートからモデルへのアクセス](../modeling/accessing-models-from-text-templates.md)」を参照してください。

テキスト テンプレートの詳細については、「[T4 テキスト テンプレートを使用したデザイン時コード生成](../modeling/design-time-code-generation-by-using-t4-text-templates.md)」を参照してください。

## <a name="create-a-model-bus-adapter-for-access-from-text-templates"></a>テキスト テンプレートからアクセスするためのモデル バス アダプターを作成する

テキスト テンプレートで ModelBus 参照を解決するには、ターゲット DSL に互換性のあるアダプターが必要です。 テキスト テンプレートは、Visual Studio ドキュメント エディターとは別の AppDomain で実行されるため、アダプターは DTE 経由でアクセスするのではなく、モデルを読み込む必要があります。

1. ターゲット DSL ソリューションに **ModelBusAdapter** プロジェクトがない場合は、Modelbus 拡張機能ウィザードを使用して作成します。

    1. Visual Studio ModelBus 拡張機能をダウンロードしてインストールします (まだインストールしていない場合)。 詳細については、[Visualization and Modeling SDK](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/) に関するページを参照してください。

    2. DSL 定義ファイルを開きます。 デザイン サーフェイスを右クリックし、 **[Modelbus の有効化]** をクリックします。

    3. ダイアログ ボックスで、 **[この DSL を ModelBus に公開する]** を選択します。 この DSL のモデルを公開すると同時に他の DSL への参照を利用する場合は、両方のオプションを選択できます。

    4. **[OK]** をクリックします。 新しいプロジェクト "ModelBusAdapter" が DSL ソリューションに追加されます。

    5. **[すべてのテンプレートの変換]** をクリックします。

    6. ソリューションをリビルドします。

2. テキスト テンプレートと、コマンドなどの他のコードから DSL にアクセスする場合は、**ModelBusAdapter** プロジェクトを複製します。

    1. Windows エクスプローラーで、**ModelBusAdapter.csproj** を含むフォルダーをコピーして貼り付けます。

    2. プロジェクト ファイルの名前を変更します (たとえば、**T4ModelBusAdapter.csproj**)。

    3. **ソリューション エクスプローラー** でソリューション ノードを右クリックし、 **[追加]** をポイントして、 **[既存のプロジェクト]** をクリックします。 新しいアダプター プロジェクト **T4ModelBusAdapter.csproj** を探します。

    4. 新しいプロジェクトの各 `*.tt` ファイルで、名前空間を変更します。

    5. **ソリューション エクスプローラー** で新しいプロジェクトを右クリックし、 **[プロパティ]** をクリックします。 プロパティ エディターで、生成されたアセンブリの名前と既定の名前空間を変更します。

    6. DslPackage プロジェクトで、新しいアダプター プロジェクトへの参照を追加して、両方のアダプターを参照できるようにします。

    7. DslPackage\source.extension.tt で、新しいアダプター プロジェクトを参照する行を追加します。

        ```
        <MefComponent>|T4ModelBusAdapter|</MefComponent>
        ```

    8. **[すべてのテンプレートの変換]** をクリックし、ソリューションをリビルドします。 ビルド エラーは発生しません。

3. 新しいアダプター プロジェクトで、次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.TextTemplating.11.0
    - Microsoft.VisualStudio.TextTemplating.Modeling.11.0

4. AdapterManager.tt で次の操作を行います。

    - AdapterManagerBase の宣言を変更して、[VsTextTemplatingModelingAdapterManager](/previous-versions/ee844317(v=vs.140)) から継承するようにします。

         `public partial class <#= dslName =>AdapterManagerBase :`

         `Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager { ...`

    - ファイルの末尾付近で、AdapterManager クラスの前の HostSpecific 属性を置き換えます。 次の行を削除します。

         `[DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]`

         次の行を挿入します。

         `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

         この属性では、ModelBus コンシューマーがアダプターを検索するときに使用できるアダプターのセットをフィルター処理します。

5. **[すべてのテンプレートの変換]** をクリックし、ソリューションをリビルドします。 ビルド エラーは発生しません。

## <a name="write-a-text-template-that-can-resolve-modelbus-references"></a>ModelBus 参照を解決できるテキスト テンプレートを作成する

通常は、"ソース" DSL から読み取り、ファイルを生成するテンプレートから始めます。 このテンプレートでは、ソース DSL プロジェクトで生成されたディレクティブを使用して、「[テキスト テンプレートからモデルへのアクセス](../modeling/accessing-models-from-text-templates.md)」で説明されている方法でソース モデル ファイルを読み取ります。 ただし、ソース DSL には、"ターゲット" DSL への ModelBus 参照が含まれています。 このため、テンプレート コードを有効にして、参照を解決し、ターゲット DSL にアクセスする必要があります。 そのため、次の手順に従ってテンプレートを調整する必要があります。

- テンプレートの基底クラスを [ModelBusEnabledTextTransformation](/previous-versions/ee844263(v=vs.140)) に変更します。

- template ディレクティブに `hostspecific="true"` を含めます。

- ターゲット DSL とそのアダプターにアセンブリ参照を追加し、ModelBus を有効にします。

- ターゲット DSL の一部として生成されるディレクティブは必要ありません。

```
<#@ template debug="true" hostspecific="true" language="C#"
inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
<#@ SourceDsl processor="SourceDslDirectiveProcessor" requires="fileName='Sample.source'" #>
<#@ output extension=".txt" #>
<#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
<#@ assembly name = "Company.TargetDsl.Dsl.dll" #>
<#@ assembly name = "Company.TargetDsl.T4ModelBusAdapter.dll" #>
<#@ assembly name = "System.Core" #>
<#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
<#@ import namespace="Company.TargetDsl" #>
<#@ import namespace="Company.TargetDsl.T4ModelBusAdapters" #>
<#@ import namespace="System.Linq" #>
<#
  SourceModelRoot source = this.ModelRoot; // Usual access to source model.
  // In the source DSL Definition, the root element has a model reference:
  using (TargetAdapter adapter = this.ModelBus.CreateAdapter(source.ModelReference) as TargetAdapter)
  {if (adapter != null)
   {
      // Get the root of the target model:
      TargetRoot target = adapter.ModelRoot;
    // The source DSL Definition has a class "SourceElement" embedded under the root.
    // (Let's assume they're all in the same model file):
    foreach (SourceElement sourceElement in source.Elements)
    {
      // In the source DSL Definition, each SourceElement has a MBR property:
      ModelBusReference elementReference = sourceElement.ReferenceToTarget;
      // Resolve the target model element:
      TargetElement element = adapter.ResolveElementReference<TargetElement>(elementReference);
#>
     The source <#= sourceElement.Name #> is linked to: <#= element.Name #> in target model: <#= target.Name #>.
<#
    }
  }}
  // Other useful code: this.Host.ResolvePath(filename) gets an absolute filename
  // from a path that is relative to the text template.
#>
```

 このテキスト テンプレートを実行すると、`SourceDsl` ディレクティブによって `Sample.source` ファイルが読み込まれます。 テンプレートでは、`this.ModelRoot` から開始して、そのモデルの要素にアクセスできます。 このコードでは、その DSL のドメイン クラスとプロパティを使用できます。

 さらに、テンプレートで ModelBus 参照を解決できます。 参照がターゲット モデルを指す場合、アセンブリ ディレクティブを使用すると、コードではそのモデルの DSL のドメイン クラスとプロパティを使用できます。

- DSL プロジェクトによって生成されるディレクティブを使用しない場合は、次も含める必要があります。

    ```
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.11.0" #>
    <#@ assembly name = "Microsoft.VisualStudio.TextTemplating.Modeling.11.0" #>
    ```

- ModelBus へのアクセスを取得するには、`this.ModelBus` を使用します。

## <a name="walkthrough-testing-a-text-template-that-uses-modelbus"></a>チュートリアル: ModelBus を使用するテキスト テンプレートのテスト
 このチュートリアルでは、次の手順を行います。

1. 2 つの DSL を構築します。 一方の DSL ("*コンシューマー*") には、もう一方の DSL ("*プロバイダー*") を参照できる `ModelBusReference` プロパティがあります。

2. プロバイダーで 2 つの ModelBus アダプターを作成します。1 つはテキスト テンプレートによるアクセス用、もう 1 つは通常のコード用です。

3. 1 つの実験用プロジェクトに DSL のインスタンス モデルを作成します。

4. 一方のモデルのドメイン プロパティをもう一方のモデルを指すように設定します。

5. 参照されているモデルを開くダブルクリック ハンドラーを作成します。

6. 最初のモデルを読み込んで、もう一方のモデルへの参照に従い、もう一方のモデルを読み取ることができるテキスト テンプレートを作成します。

### <a name="construct-a-dsl-that-is-accessible-to-modelbus"></a>ModelBus にアクセス可能な DSL を構築する

1. 新しい DSL ソリューションを作成します。 この例では、タスク フロー ソリューション テンプレートを選択します。 言語名を `MBProvider` に設定し、ファイル名拡張子を ".provide" に設定します。

2. DSL 定義図で、上部以外の図の空白部分を右クリックし、 **[Modelbus の有効化]** をクリックします。

   **[Modelbus の有効化]** が表示されない場合は、VMSDK ModelBus 拡張機能をダウンロードしてインストールします。

3. **[Modelbus の有効化]** ダイアログ ボックスで、 **[この DSL を ModelBus に公開する]** を選択し、 **[OK]** をクリックします。

    ソリューションに新しいプロジェクト `ModelBusAdapter` が追加されます。

これで、ModelBus を使用してテキスト テンプレートからアクセスできる DSL が作成されました。 この参照は、コマンド、イベント ハンドラー、またはルールのコードで解決できます。これらはすべて、モデル ファイル エディターの AppDomain で動作します。 ただし、テキスト テンプレートは別の AppDomain で実行され、編集時にモデルにアクセスすることはできません。 テキスト テンプレートからこの DSL への ModelBus 参照にアクセスするには、別の ModelBusAdapter が必要です。

### <a name="create-a-modelbus-adapter-that-is-configured-for-text-templates"></a>テキスト テンプレート用に構成されている ModelBus アダプターを作成する

1. エクスプローラーで、*ModelBusAdapter.csproj* を含むフォルダーをコピーして貼り付けます。

    フォルダーに、**T4ModelBusAdapter** という名前を付けます。

    プロジェクト ファイルの名前を *T4ModelBusAdapter.csproj* に変更します。

2. ソリューション エクスプローラーで、MBProvider ソリューションに T4ModelBusAdapter を追加します。 ソリューション ノードを右クリックして **[追加]** をポイントし、 **[既存のプロジェクト]** をクリックします。

3. T4ModelBusAdapter プロジェクト ノードを右クリックし、[プロパティ] をクリックします。 プロジェクトのプロパティ ウィンドウで、 **[アセンブリ名]** と **[既定の名前空間]** を `Company.MBProvider.T4ModelBusAdapters` に変更します。

4. T4ModelBusAdapter 内の各 *.tt ファイルで、名前空間の最後の部分に "T4" を挿入して、行が次のようになるようにします。

    `namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters`

5. `DslPackage` プロジェクトで、プロジェクト参照を `T4ModelBusAdapter` に追加します。

6. DslPackage\source.extension.tt で、`<Content>` の下に次の行を追加します。

    `<MefComponent>|T4ModelBusAdapter|</MefComponent>`

7. `T4ModelBusAdapter` プロジェクトで、**Microsoft.VisualStudio.TextTemplating.Modeling.11.0** への参照を追加します。

8. T4ModelBusAdapter\AdapterManager.tt を開きます。

   1. AdapterManagerBase の基底クラスを [VsTextTemplatingModelingAdapterManager](/previous-versions/ee844317(v=vs.140)) に変更します。 ファイルのこの部分は次のようになります。

       ```
       namespace <#= CodeGenerationUtilities.GetPackageNamespace(this.Dsl) #>.T4ModelBusAdapters
       {
           /// <summary>
           /// Adapter manager base class (double derived pattern) for the <#= dslName #> Designer
           /// </summary>
           public partial class <#= dslName #>AdapterManagerBase
           : Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager
           {
       ```

   2. ファイルの終わり近くで、クラス AdapterManager の前に次の追加属性を挿入します。

        `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`

        結果は次のようになります。

       ```
       /// <summary>
       /// ModelBus modeling adapter manager for a <#= dslName #>Adapter model adapter
       /// </summary>
       [Mef::Export(typeof(DslIntegration::ModelBusAdapterManager))]
       [Mef::ExportMetadata(DslIntegration::CompositionAttributes.AdapterIdKey,<#= dslName #>Adapter.AdapterId)]
       [DslIntegration::HostSpecific(DslIntegrationShell::VsModelingAdapterManager.HostName)]
       [Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]
       public partial class <#= dslName #>AdapterManager : <#= dslName #>AdapterManagerBase
       {
       }
       ```

9. ソリューション エクスプローラーのタイトル バーで、 **[すべてのテンプレートの変換]** をクリックします。

10. **F5** キーを押します。

11. DSL が動作していることを確認します。 実験用プロジェクトで `Sample.provider` を開きます。 Visual Studio の実験用インスタンスを終了します。

    この DSL への ModelBus 参照は、テキスト テンプレートおよび通常のコードでも解決できるようになりました。

### <a name="construct-a-dsl-with-a-modelbus-reference-domain-property"></a>ModelBus 参照ドメイン プロパティを使用して DSL を構築する

1. [最小言語] ソリューション テンプレートを使用して、新しい DSL を作成します。 言語に MBConsumer という名前を付け、ファイル名拡張子を ".consume" に設定します。

2. DSL プロジェクトで、MBProvider DSL アセンブリへの参照を追加します。 `MBConsumer\Dsl\References` を右クリックし、 **[参照の追加]** をクリックします。 **[参照]** タブで `MBProvider\Dsl\bin\Debug\Company.MBProvider.Dsl.dll` を探します。

    これにより、他の DSL を使用するコードを作成できます。 複数の DSL への参照を作成する場合は、それらも追加します。

3. DSL 定義図で、図を右クリックし、 **[ModelBus の有効化]** をクリックします。 ダイアログ ボックスで、 **[この DSL が ModelBus を利用可能にする]** を選択します。

4. `ExampleElement` クラスで、新しいドメイン プロパティ `MBR` を追加し、[プロパティ] ウィンドウで、その型を `ModelBusReference` に設定します。

5. 図のドメイン プロパティを右クリックし、 **[ModelBusReference 固有プロパティの編集]** をクリックします。 ダイアログ ボックスで、**モデル要素** を選択します。

    ファイル ダイアログ フィルターを次のように設定します。

    `Provider File|*.provide`

    "&#124;" の後の部分文字列は、[ファイルの選択] ダイアログ ボックスのフィルターです。 *.\* を使用すると、すべてのファイルを許可するように設定できます。

    **[モデル要素の型]** 一覧で、プロバイダー DSL 内の 1 つ以上のドメイン クラスの名前を入力します (たとえば、「Company.MBProvider.Task」と入力します)。 抽象クラスにすることができます。 リストを空白のままにすると、ユーザーは任意の要素への参照を設定できます。

6. ダイアログを閉じて、 **[すべてのテンプレートの変換]** を実行します。

   別の DSL の要素への参照を含むことができる DSL を作成しました。

### <a name="create-a-modelbus-reference-to-another-file-in-the-solution"></a>ソリューション内の別のファイルへの ModelBus 参照を作成する

1. MBConsumer ソリューションで、Ctrl キーを押しながら F5 キーを押します。 **MBConsumer\Debugging** プロジェクトで Visual Studio の実験用インスタンスが開きます。

2. Sample.provide のコピーを **MBConsumer\Debugging** プロジェクトに追加します。 ModelBus 参照は同じソリューション内のファイルを参照する必要があるため、これが必要になります。

   1. Debugging プロジェクトを右クリックし、 **[追加]** をポイントして、 **[既存の項目]** をクリックします。

   2. **[項目の追加]** ダイアログで、フィルターを **[すべてのファイル (\*.\*)]** に設定します。

   3. `MBProvider\Debugging\Sample.provide` に移動して、 **[追加]** をクリックします。

3. `Sample.consume`を開きます。

4. 例のシェイプの 1 つをクリックし、[プロパティ] ウィンドウで、MBR プロパティの **[...]** をクリックします。 ダイアログ ボックスで、 **[参照]** をクリックして、`Sample.provide` を選択します。 要素ウィンドウで、タイプ タスクを展開し、いずれかの要素を選択します。

5. ファイルを保存します。 (まだ Visual Studio の実験用インスタンスを終了しないでください。)

   別のモデルの要素への ModelBus 参照を含むモデルを作成しました。

### <a name="resolve-a-modelbus-reference-in-a-text-template"></a>テキスト テンプレートで ModelBus 参照を解決する

1. Visual Studio の実験用インスタンスで、サンプル テキスト テンプレート ファイルを開きます。 その内容を次のように設定します。

    ```
    <#@ template debug="true" hostspecific="true" language="C#"
    inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>
    <#@ MBConsumer processor="MBConsumerDirectiveProcessor" requires="fileName='Sample.consume'" #>
    <#@ output extension=".txt" #>
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>
    <#@ assembly name = "Company.MBProvider.Dsl.dll" #>
    <#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>
    <#@ import namespace="Company.MBProvider" #>
    <#
      // Property provided by the Consumer directive processor:
      ExampleModel consumerModel = this.ExampleModel;
      // Iterate through Consumer model, listing the elements:
      foreach (ExampleElement element in consumerModel.Elements)
      {
    #>
       <#= element.Name #>
    <#
        if (element.MBR != null)
      using (ModelBusAdapter adapter = this.ModelBus.CreateAdapter(element.MBR))
      {
              // If we allowed multiple types or DSLs in the MBR, discover type here.
        Task task = adapter.ResolveElementReference<Task>(element.MBR);
    #>
            <#= element.Name #> is linked to Task: <#= task==null ? "(null)" : task.Name #>
    <#
          }
      }
    #>

    ```

     次の点にも注意します。

    - `template` ディレクティブの `hostSpecific` 属性と `inherits` 属性を設定する必要があります。

    - コンシューマー モデルは、その DSL で生成されたディレクティブ プロセッサを介して通常の方法でアクセスされます。

    - アセンブリ ディレクティブとインポート ディレクティブは、ModelBus とプロバイダー DSL の型にアクセスできる必要があります。

    - 多数の MBR が同じモデルにリンクされていることがわかっている場合は、CreateAdapter を 1 回だけ呼び出すことをお勧めします。

2. テンプレートを保存します。 生成されたテキスト ファイルが次のようになっていることを確認します。

    ```
    ExampleElement1
    ExampleElement2
         ExampleElement2 is linked to Task: Task2
    ```

### <a name="resolve-a-modelbus-reference-in-a-gesture-handler"></a>ジェスチャ ハンドラーで ModelBus 参照を解決する

1. Visual Studio の実験用インスタンスを実行している場合は終了します。

2. *MBConsumer\Dsl\Custom.cs* という名前のファイルを追加し、その内容を次のように設定します。

    ```csharp
    namespace Company.MB2Consume
    {
      using Microsoft.VisualStudio.Modeling.Integration;
      using Company.MB3Provider;

      public partial class ExampleShape
      {
        public override void OnDoubleClick(Microsoft.VisualStudio.Modeling.Diagrams.DiagramPointEventArgs e)
        {
          base.OnDoubleClick(e);
          ExampleElement element = this.ModelElement as ExampleElement;
          if (element.MBR != null)
          {
            IModelBus modelbus = this.Store.GetService(typeof(SModelBus)) as IModelBus;
            using (ModelBusAdapter adapter = modelbus.CreateAdapter(element.MBR))
            {
              Task task = adapter.ResolveElementReference<Task>(element.MBR);
              // Open a window on this model:
              ModelBusView view = adapter.GetDefaultView();
              view.Show();
              view.SetSelection(element.MBR);
            }
          }
        }
      }
    }
    ```

3. **Ctrl**+**F5** キーを押します。

4. Visual Studio の実験用インスタンスで `Debugging\Sample.consume` を開きます。

5. シェイプの 1 つをダブルクリックします。

    その要素に MBR を設定してある場合は、参照先のモデルが開き、参照されている要素が選択されます。

## <a name="see-also"></a>関連項目

- [Visual Studio Modelbus によるモデルの統合](../modeling/integrating-models-by-using-visual-studio-modelbus.md)
- [コード生成と T4 テキスト テンプレート](../modeling/code-generation-and-t4-text-templates.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
