---
title: Visual Studio modelbus によるモデルの統合 |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2ff722f3-21d6-44e2-9efd-f6694aee9987
caps.latest.revision: 28
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 2cbc89ae03e96a574e3d63a8448628d29ecf163f
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47548953"
---
# <a name="integrating-models-by-using-visual-studio-modelbus"></a>Visual Studio Modelbus によるモデルの統合
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[Visual Studio modelbus によるモデルの統合](https://docs.microsoft.com/visualstudio/modeling/integrating-models-by-using-visual-studio-modelbus)します。  
  
[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ModelBus はモデルにモデル間、およびその他のツールからリンクを作成するためのメソッドを提供します。 たとえば、ドメイン固有言語 (DSL) モデルと UML モデルをリンクする可能性があります。 DSL の統合セットを作成できます。  
  
 ModelBus により、モデルまたはモデル内の特定の要素への一意の参照を作成できます。 この参照は、たとえば、別のモデル内の要素など、モデルの外に保存できます。 後で何らかのツールにおいて要素へのアクセスを取得する必要が生じると、モデル バス インフラストラクチャは適切なモデルを読み込み、要素を返します。 必要があれば、モデルをユーザーに表示できます。 ファイルが以前の場所でアクセスできない場合、ModelBus はユーザーにファイルを見つけるように求めます。 ユーザーがファイルを見つけると、ModelBus はそのファイルへのすべての参照を解決します。  
  
> [!NOTE]
>  ModelBus の現在の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 実装では、リンクされたモデルは同じ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューション内の項目である必要があります。  
  
 追加情報とサンプル コードについては、以下を参照してください。  
  
-   [方法: ドラッグ アンド ドロップ ハンドラーを追加する](../modeling/how-to-add-a-drag-and-drop-handler.md)  
  
-   [Modeling SDK for Visual Studio](http://www.microsoft.com/download/details.aspx?id=40754)  
  
##  <a name="provide"></a> DSL へのアクセスを提供します。  
 モデルまたはその要素への ModelBus 参照を作成するには、DSL の ModelBusAdapter を定義しておく必要があります。 そのための最も簡単な方法は、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] モデル バス拡張機能を使用して、コマンドを DSL デザイナーに追加することです。  
  
###  <a name="expose"></a> DSL 定義をモデル バスを公開するには  
  
1.  Visual Studio モデル バス拡張機能をまだインストールしていない場合はダウンロードしてインストールします。 詳細については、次を参照してください。 [Visualization and Modeling SDK](http://go.microsoft.com/fwlink/?LinkID=185579)します。  
  
2.  DSL 定義ファイルを開きます。 デザイン サーフェイスを右クリックし、をクリックし、 **Modelbus の有効化**します。  
  
3.  ダイアログ ボックスで、次のように選択します。**この DSL を ModelBus に公開する**します。 この DSL のモデルを公開すると同時に他の DSL への参照を利用する場合は、両方のオプションを選択できます。  
  
4.  **[OK]** をクリックします。 新しいプロジェクト "ModelBusAdapter" が DSL ソリューションに追加されます。  
  
5.  テキスト テンプレートから DSL にアクセスする場合、新しいプロジェクトで AdapterManager.tt を変更する必要があります。 コマンドやイベント ハンドラーなどの他のコードから DSL にアクセスする場合はこの手順を省略します。 詳細については、次を参照してください。[テキスト テンプレートで Visual Studio ModelBus を使用して](../modeling/using-visual-studio-modelbus-in-a-text-template.md)します。  
  
    1.  AdapterManagerBase の基底クラスを <xref:Microsoft.VisualStudio.TextTemplating.Modeling.VsTextTemplatingModelingAdapterManager> に変更します。  
  
    2.  ファイルの終わり近くで、クラス AdapterManager の前に次の追加属性を挿入します。  
  
         `[Microsoft.VisualStudio.Modeling.Integration.HostSpecific(HostName)]`  
  
    3.  参照の ModelBusAdapter プロジェクトで追加**Microsoft.VisualStudio.TextTemplating.Modeling.11.0**します。  
  
     テキスト テンプレートと他のコードの両方から DSL にアクセスするには、変更したアダプターと変更していないアダプターの 2 つが必要です。  
  
6.  クリックして**すべてのテンプレートの変換**します。  
  
7.  ソリューションをリビルドします。  
  
 これで ModelBus がこの DSL のインスタンスを開くことができるようになります。  
  
 フォルダー `ModelBusAdapters\bin\*` には、`Dsl` プロジェクトと `ModelBusAdapters` プロジェクトによりビルドされるアセンブリが含まれます。 この DSL を別の DSL から参照するには、これらのアセンブリをインポートする必要があります。  
  
### <a name="making-sure-that-elements-can-be-referenced"></a>要素が参照可能であることの確認  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ModelBus アダプターは、既定では、要素を特定するためにその GUID を使用します。 したがって、これらの ID はモデル ファイル内に保持される必要があります。  
  
##### <a name="to-ensure-that-element-ids-are-persisted"></a>要素 ID が保持されることを確認するには  
  
1.  DslDefinition.dsl を開きます。  
  
2.  DSL エクスプ ローラーで、 **Xml シリアル化動作**、し**クラス データ**します。  
  
3.  モデル バス参照を作成する各クラスについて、次の操作を実行します。  
  
     クラス ノードをクリックし、[プロパティ] ウィンドウで**Id のシリアル化**に設定されている`true`します。  
  
 または、GUID ではなく要素名を使用して要素を特定する場合、生成されたアダプターの各部をオーバーライドできます。 アダプター クラス内の次のメソッドをオーバーライドします。  
  
-   `GetElementId` をオーバーライドし、使用する ID を返します。 このメソッドは参照を作成するときに呼び出されます。  
  
-   `ResolveElementReference` をオーバーライドし、モデル バス参照から正しい要素を特定します。  
  
##  <a name="editRef"></a> 別の DSL から DSL にアクセスします。  
 DSL のドメイン プロパティにモデル バス参照を保存し、それらを使用するカスタム コードを作成できます。 ユーザーがモデル ファイルとその中の要素を選択することにより、モデル バス参照を作成可能にすることもできます。  
  
 別の DSL への参照を使用する DSL を有効にする必要があります最初に、*コンシューマー*モデル バス参照の。  
  
#### <a name="to-enable-a-dsl-to-consume-references-to-an-exposed-dsl"></a>DSL が公開されている DSL への参照を利用可能にするには  
  
1.  DSL 定義図で図の主な部分を右クリックし、 **Modelbus の有効化**します。  
  
2.  ダイアログ ボックスで、次のように選択します。**モデル バス参照を使用するには、このモデルを有効にする**します。  
  
3.  利用する DSL の Dsl プロジェクトで、次のアセンブリをプロジェクト参照に追加します。 これらのアセンブリ (.dll ファイル) は、ModelBusAdapter\bin で見つかります\\*、公開される DSL のディレクトリ。  
  
    -   たとえば、公開されている DSL アセンブリ**Fabrikam.FamilyTree.Dsl.dll**  
  
    -   公開されているモデル バス アダプターのアセンブリがたとえば**Fabrikam.FamilyTree.ModelBusAdapter.dll**  
  
4.  次の .NET アセンブリを利用する DSL プロジェクトのプロジェクト参照に追加します。  
  
    1.  **Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0.dll**  
  
    2.  **Microsoft.VisualStudio.Modeling.Sdk.Integration.Shell.11.0.dll**  
  
#### <a name="to-store-a-model-bus-reference-in-a-domain-property"></a>モデル バス参照をドメイン プロパティに保存するには  
  
1.  利用する DSL の DSL 定義で、ドメイン クラスにドメイン プロパティを追加し、その名前を設定します。  
  
2.  プロパティ ウィンドウで、選択すると、ドメイン プロパティを使用して設定**型**に`ModelBusReference`します。  
  
 この段階で、プログラム コードはプロパティ値を設定できますが、[プロパティ] ウィンドウでは読み取り専用です。  
  
 ユーザーが特殊な ModelBus 参照エディターを使用してプロパティを設定可能にすることができます。 このエディターの 2 つのバージョンまたは*ピッカー:* いずれかにより、ユーザーがモデル ファイルを選択して、その他により、ユーザーがモデル ファイルと、モデル内の要素を選択します。  
  
#### <a name="to-allow-the-user-to-set-a-model-bus-reference-in-a-domain-property"></a>ユーザーがモデル バス参照をドメイン プロパティに設定可能にするには  
  
1.  ドメイン プロパティを右クリックし、をクリックし、**編集 ModelBusReference 固有プロパティ**します。 ダイアログ ボックスが開きます。 これは、*モデル バス ピッカー*します。  
  
2.  適切な選択**modelbusreference の種類**: モデルまたはモデル内の要素。  
  
3.  ファイル ダイアログ フィルター文字列に、`Family Tree files |*.ftree` のような文字列を入力します。 公開される DSL のファイル拡張子を置き換えます。  
  
4.  モデル内の要素を参照する場合、ユーザーが選択可能な型の一覧を追加します (たとえば、Company.FamilyTree.Person)。  
  
5.  をクリックして**OK**、順にクリックします**すべてのテンプレートの変換**ソリューション エクスプ ローラーのツールバー。  
  
    > [!WARNING]
    >  有効なモデルまたはエンティティを選択しなかった場合、[OK] ボタンが有効のように見えても効果はありません。  
  
6.  Company.FamilyTree.Person などのターゲット型の一覧を指定した場合、DSL プロジェクトにアセンブリ参照を追加して、ターゲット DSL の DLL (たとえば、Company.FamilyTree.Dsl.dll) を参照する必要があります。  
  
#### <a name="to-test-a-model-bus-reference"></a>モデル バス参照をテストするには  
  
1.  公開される DSL と利用する DSL の両方をビルドします。  
  
2.  F5 キーまたは CTRL+F5 キーを押して、DSL のいずれかを実験モードで実行します。  
  
3.  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験インスタンスのデバッグ プロジェクトで、各 DSL のインスタンスであるファイルを追加します。  
  
    > [!NOTE]
    >  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ModelBus は、同じ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューション内の項目である、モデルへの参照のみを解決できます。 たとえば、ファイル システムの別の部分にあるモデル ファイルへの参照は作成できません。  
  
4.  公開される DSL のインスタンス内に要素とリンクを作成し、インスタンスを保存します。  
  
5.  利用する DSL のインスタンスを開き、モデル バス参照プロパティを持つモデル要素を選択します。  
  
6.  [プロパティ] ウィンドウで、モデル バス参照プロパティをダブルクリックします。 ピッカー ダイアログが開きます。  
  
7.  クリックして**参照**公開されている DSL のインスタンスを選択します。  
  
     モデル バス参照の要素固有の種類を指定した場合、ピッカーではモデル内の項目を選択することもできます。  
  
## <a name="creating-references-in-program-code"></a>プログラム コード中の参照の作成  
 モデルまたは要素への参照をモデル内に保存する場合、`ModelBusReference` を作成します。 `ModelBusReference` にはモデル参照と要素参照の 2 種類があります。  
  
 モデル参照を作成するには、モデルがインスタンスになっている DSL の AdapterManager と、モデルのファイル名または [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクト項目が必要です。  
  
 要素参照を作成するには、モデル ファイルと参照する要素のアダプターが必要です。  
  
> [!NOTE]
>  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ModelBus を使用して、同じ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューション内の項目への参照のみを作成できます。  
  
### <a name="import-the-exposed-dsl-assemblies"></a>公開されている DSL アセンブリのインポート  
 利用するプロジェクトで、DSL へのプロジェクト参照と公開されている DSL の ModelBusAdapter アセンブリを追加します。  
  
 たとえば、ModelBus References を MusicLibrary DSL の要素に保存するとします。 ModelBus References は FamilyTree DSL の要素を参照します。 MusicLibrary ソリューションの `Dsl` プロジェクトで、References ノードに次のアセンブリへの参照を追加します。  
  
-   Fabrikam.FamilyTree.Dsl.dll - 公開されている DSL。  
  
-   Fabrikam.FamilyTree.ModelBusAdapters.dll - 公開されている DSL の ModelBus アダプター。  
  
-   Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0  
  
-   Microsoft.VisualStudio.Modeling.Sdk.Integration.Shell.11.0  
  
 これらのアセンブリは、公開されている DSL の `ModelBusAdapters` プロジェクトの `bin\*` の下にあります。  
  
 参照を作成するコード ファイルで、通常、次の名前空間をインポートする必要があります。  
  
```  
// The namespace of the DSL you want to reference:  
using Fabrikam.FamilyTree;  // Exposed DSL  
using Fabrikam.FamilyTree.ModelBusAdapters;  
using Microsoft.VisualStudio.Modeling.Integration;  
using System.Linq;  
...  
```  
  
### <a name="to-create-a-reference-to-a-model"></a>モデルへの参照を作成するには  
 モデル参照を作成するには、公開されている DSL の AdapterManager にアクセスし、それを使用してモデルへの参照を作成します。 ファイル パスまたは `EnvDTE.ProjectItem` のどちらかを指定できます。  
  
 AdapterManager から、Adapter を取得し、モデル内の個々の要素にアクセスできます。  
  
> [!NOTE]
>  操作を終了したら、Adapter を破棄する必要があります。 そのための最も便利な方法は、`using` ステートメントの使用です。 次に例を示します。  
  
```  
// The file path of a model instance of the FamilyTree DSL:  
string targetModelFile = "TudorFamilyTree.ftree";  
// Get the ModelBus service:  
IModelBus modelBus =   
    this.Store.GetService(typeof(SModelBus)) as IModelBus;  
// Get an adapterManager for the target DSL:  
FamilyTreeAdapterManager manager =   
    (modelbus.GetAdapterManager(FamilyTreeAdapter.AdapterId)   
     as FamilyTreeAdapterManager;  
// or: (modelBus.FindAdapterManagers(targetModelFile).First())  
// or could provide an EnvDTE.ProjectItem  
  
// Create a reference to the target model:  
// NOTE: the target model must be a file in this project.  
ModelBusReference modelReference =  
     manager.CreateReference(targetModelFile);  
// or can use an EnvDTE.ProjectItem instead of the filename  
  
// Get the root element of this model:  
using (FamilyTreeAdapter adapter =   
     modelBus.CreateAdapter(modelReference) as FamilyTreeAdapter)  
{  
  FamilyTree modelRoot = adapter.ModelRoot;  
  // Access elements under the root in the usual way:  
  foreach (Person p in modelRoot.Persons) {...}  
  // You can create adapters for individual elements:  
  ModelBusReference elementReference =  
     adapter.GetElementReference(person);  
  ...  
} // Dispose adapter  
  
```  
  
 後で `modelReference` を使用可能にする場合、外部型 `ModelBusReference` を持つドメイン プロパティに保存できます。  
  
```  
using Transaction t = this.Store.TransactionManager  
    .BeginTransaction("keep reference"))  
{  
  artist.FamilyTreeReference = modelReference;  
  t.Commit();  
}  
```  
  
 ユーザーがこのドメイン プロパティを編集可能にするには、Editor 属性のパラメーターとして `ModelReferenceEditor` を使用します。 詳細については、次を参照してください。[の参照を編集するユーザーを許可する](#editRef)します。  
  
### <a name="to-create-a-reference-to-an-element"></a>要素への参照を作成するには  
 モデル用に作成したアダプターは参照の作成と解決のために使用できます。  
  
```  
// person is an element in the FamilyTree model:  
ModelBusReference personReference =   
  adapter.GetElementReference(person);  
```  
  
 後で `elementReference` を使用可能にする場合、外部型 `ModelBusReference` を持つドメイン プロパティに保存できます。 ユーザーがそれを編集可能にするには、Editor 属性のパラメーターとして `ModelElementReferenceEditor` を使用します。 詳細については、次を参照してください。[の参照を編集するユーザーを許可する](#editRef)します。  
  
### <a name="resolving-references"></a>参照の解決  
 `ModelBusReference` (MBR) がある場合、モデルまたはモデルが参照するモデル要素を取得できます。 要素が図またはその他の表示に示されている場合、表示を開き、要素を選択できます。  
  
 MBR からアダプターを作成できます。 アダプターから、モデルのルートを取得できます。 モデル内の特定の要素を参照する MBR を解決することもできます。  
  
```  
using Microsoft.VisualStudio.Modeling.Integration; ...  
ModelBusReference elementReference = ...;  
  
// Get the ModelBus service:  
IModelBus modelBus =   
    this.Store.GetService(typeof(SModelBus)) as IModelBus;  
// Use a model reference or an element reference  
// to obtain an adapter for the target model:  
using (FamilyTreeAdapter adapter =   
   modelBus.CreateAdapter(elementReference) as FamilyTreeAdapter)  
   // or CreateAdapter(modelReference)  
{  
  // Get the root of the model:  
  FamilyTree tree = adapter.ModelRoot;  
  
  // Get a model element:  
  MyDomainClass mel =  
    adapter.ResolveElementReference<MyDomainClass>(elementReference);  
  if (mel != null) {...}  
  
  // Get the diagram or other view, if there is one:  
  ModelBusView view = adapter.GetDefaultView();  
  if (view != null)   
  {  
   view.Open();  
   // Display the diagram:  
   view.Show();   
   // Attempt to select the shape that presents the element:  
   view.SetSelection(elementReference);  
  }  
} // Dispose the adapter.  
```  
  
##### <a name="to-resolve-modelbus-references-in-a-text-template"></a>テキスト テンプレート内の ModelBus References を解決するには  
  
1.  アクセスする DSL には、テキスト テンプレートによるアクセスのために構成された ModelBus Adapter が含まれている必要があります。 詳細については、次を参照してください。 [DSL へのアクセスを提供する](#provide)します。  
  
2.  通常、ソース DSL 内に保存されたモデル バス参照 (MBR) を使用してターゲット DSL にアクセスします。 したがって、テンプレートにはソース DSL のディレクティブに加えて、MBR を解決するためのコードが含まれています。 テキスト テンプレートの詳細については、次を参照してください。[ドメイン固有言語からコードを生成する](../modeling/generating-code-from-a-domain-specific-language.md)します。  
  
    ```  
    <#@ template debug="true" hostspecific="true"   
    inherits="Microsoft.VisualStudio.TextTemplating.Modeling.ModelBusEnabledTextTransformation" #>   
    <#@ SourceDsl processor="SourceDslDirectiveProcessor" requires="fileName='Sample.source'" #>  
    <#@ output extension=".txt" #>  
    <#@ assembly name = "Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0" #>  
    <#@ assembly name = "System.Core" #>  
    <#@ assembly name = "Company.CompartmentDragDrop.Dsl.dll" #>  
    <#@ assembly name = "Company.CompartmentDragDrop.ModelBusAdapter.dll" #>  
    <#@ import namespace="Microsoft.VisualStudio.Modeling.Integration" #>  
    <#@ import namespace="System.Linq" #>  
    <#@ import namespace="Company.CompartmentDragDrop" #>  
    <#@ import namespace="Company.CompartmentDragDrop.ModelBusAdapters" #>  
    <# // Get source root from directive processor:  
      ExampleModel source = this.ExampleModel;   
      // This DSL has a MBR in its root:  
    using (ModelBusAdapter adapter = this.ModelBus.CreateAdapter(source.ModelReference) as ModelBusAdapter)   
      {  
      ModelBusAdapterManager manager = this.ModelBus.FindAdapterManagers(this.Host.ResolvePath("Sample.compDD1")).FirstOrDefault();  
      ModelBusReference modelReference =  
        manager.CreateReference(this.Host.ResolvePath("Sample.compDD1"));  
  
      // Get the root element of this model:  
      using (CompartmentDragDropAdapter adapter =   
         this.ModelBus.CreateAdapter(modelReference) as CompartmentDragDropAdapter)  
      {  
        ModelRoot root = adapter.ModelRoot;  
    #>  
    [[<#= root.Name #>]]  
    <#  
      }  
    #>  
  
    ```  
  
 詳細とチュートリアルは、次を参照してください[テキスト テンプレートでの Visual Studio ModelBus の使用。](../modeling/using-visual-studio-modelbus-in-a-text-template.md)  
  
## <a name="serializing-a-modelbusreference"></a>ModelBusReference のシリアル化  
 `ModelBusReference` (MBR) を文字列形式で保存する場合、次のようにシリアル化することができます。  
  
```  
string serialized = modelBus.SerializeReference(elementReference);  
// Store it anywhere, then get it back again:  
ModelBusReference elementReferenceRestored =  
    modelBus.DeserializeReference(serialized, null);  
```  
  
 この方法でシリアル化される MBR はコンテキストに依存しません。 単純なファイルベースのモデル バス アダプターを使用している場合、MBR には絶対ファイル パスが含まれます。 これはインスタンス モデル ファイルが絶対に移動しない場合は十分です。 ただし、モデル ファイルは通常、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクト内の項目です。 ユーザーはプロジェクト全体をファイル システムの異なる場所へ移動できると期待しています。 ユーザーはプロジェクトをソース管理の下に維持し、異なるコンピューターで開くこともできると期待しています。 したがって、パス名はファイルを含むプロジェクトの場所を基準とする相対値としてシリアル化する必要があります。  
  
### <a name="serializing-relative-to-a-specified-file-path"></a>指定されたファイル パスを基準とする相対シリアル化  
 `ModelBusReference` には、相対シリアル化の基準となるファイル パスなどの情報を含めることが可能なディクショナリである `ReferenceContext` が含まれています。  
  
 パス相対シリアル化を実行するには、次の操作を実行します。  
  
```  
elementReference.ReferenceContext.Add(  
   ModelBusReferencePropertySerializer.FilePathSaveContextKey,   
   currentProjectFilePath);  
string serialized = modelBus.SerializeReference(elementReference);  
```  
  
 次の文字列から参照を取得するには  
  
```  
ReferenceContext context = new ReferenceContext();  
context.Add(ModelBusReferencePropertySerializer.FilePathLoadContextKey,  
    currentProjectFilePath);  
ModelBusReference elementReferenceRestored =  
    modelBus.DeserializeReference(serialized, context);  
```  
  
### <a name="modelbusreferences-created-by-other-adapters"></a>他のアダプターにより作成された ModelBusReferences  
 独自のアダプターを作成する場合、次の情報が役立ちます。  
  
 `ModelBusReference` (MBR) は、モデル バスにより逆シリアル化される MBR ヘッダーと特定のアダプター マネージャーにより処理されるアダプター固有部分の 2 つの部分で構成されます。 これにより、独自のアダプター シリアル化形式を提供できます。 たとえば、ファイルではなくデータベースを参照したり、アダプター参照に追加情報を保存したりすることできます。 独自のアダプターは `ReferenceContext` に追加情報を配置することもできます。  
  
 MBR を逆シリアル化する場合、ReferenceContext を指定する必要があり、これは MBR オブジェクト内に保存されます。 MBR をシリアル化する場合、保存された ReferenceContext はアダプターが文字列の生成を助けるために使用されます。 逆シリアル化された文字列には ReferenceContext 内のすべての情報が含まるわけではありません。 たとえば、単純なファイルベースのアダプターで、ReferenceContext はルート ファイル パスを含みますが、これはシリアル化された MBR 文字列に保存されません。  
  
 MBR は次の 2 つの段階で逆シリアル化されます。  
  
-   `ModelBusReferencePropertySerializer` は MBR ヘッダーを処理する、標準のシリアライザーです。 これは標準の DSL `SerializationContext` プロパティ バッグを使用し、このプロパティ バッグは, キー `ReferenceContext` を使用する `ModelBusReferencePropertySerializer.ModelBusLoadContextKey` に保存されています。 特に、`SerializationContext` は `ModelBus` のインスタンスを含む必要があります。  
  
-   ModelBus Adapter は MBR のアダプター固有部分を処理します。 これは MBR の ReferenceContext に保存されている追加情報を使用できます。 単純なファイルベースのアダプターは、キーを使用してルート ファイル パスを保持`FilePathLoadContextKey`と`FilePathSaveContextKey`します。  
  
     モデル ファイル内のアダプター参照は使用されるときにのみ逆シリアル化されます。  
  
## <a name="to-create-a-model"></a>モデルを作成するには  
  
### <a name="creating-opening-and-editing-a-model"></a>モデルの作成、オープン、および編集  
 次のフラグメントは、VMSDK Web サイトの State Machine サンプルから取得したものです。 ここには、ModelBusReferences を使用した、モデルの作成とオープン、およびモデルに関連する図の取得が示されています。  
  
 このサンプルで、ターゲット DSL の名前は StateMachine です。 そこから、モデル クラスの名前や ModelBusAdapter の名前など、いくつかの名前が派生しています。  
  
```  
using Fabrikam.StateMachine.ModelBusAdapters;   
using Microsoft.VisualStudio.Modeling;  
using Microsoft.VisualStudio.Modeling.Diagrams;  
using Microsoft.VisualStudio.Modeling.Integration;  
using Microsoft.VisualStudio.Modeling.Integration.Shell;  
using Microsoft.VisualStudio.Modeling.Shell;  
...  
// Create a new model.  
ModelBusReference modelReference =   
   StateMachineAdapterManager    .CreateStateMachineModel(modelName, fileName);  
//Keep reference of new model in this model.  
using (Transaction t = ...)  
{  
  myModelElement.ReferenceProperty = modelReference;  
  t.Commit();  
}  
// Get the ModelBus service from Visual Studio.  
IModelBus modelBus = Microsoft.VisualStudio.Shell.Package.  
    GetGlobalService(typeof(SModelBus)) as IModelBus;  
// Get a modelbus adapter on the new model.  
ModelBusAdapter modelBusAdapter;  
modelBus.TryCreateAdapter(modelReference,   
    this.ServiceProvider, out modelBusAdapter);  
using (StateMachineAdapter adapter =   
      modelBusAdapter as StateMachineAdapter)  
{  
    if (adapter != null)  
    {  
        // Obtain a Diagram from the adapter.  
        Diagram targetDiagram =   
           ((StandardVsModelingDiagramView)  
                 adapter.GetDefaultView()  
            ).Diagram;  
  
        using (Transaction t =   
             targetDiagram.Store.TransactionManager  
                .BeginTransaction("Update diagram"))  
        {  
            DoUpdates(targetDiagram);  
            t.Commit();  
        }  
  
        // Display the new diagram.  
        adapter.GetDefaultView().Show();  
    }  
}  
```  
  
## <a name="validating-references"></a>参照の検証  
 BrokenReferenceDetector は ModelBusReferences を保持可能な、Store 内のすべてのドメイン プロパティをテストします。 これはアクションが見つかった場所で指定されるアクションを呼び出します。 これは特に検証メソッドに便利です。 次の検証メソッドは、モデルの保存を試行するときにストアをテストし、壊れている参照をエラー ウィンドウに報告します。  
  
```  
[ValidationMethod(ValidationCategories.Save)]  
public void ValidateModelBusReferences(ValidationContext context)  
{  
  BrokenReferenceDetector.DetectBrokenReferences(this.Store,  
    delegate(ModelElement element, // parent of property  
             DomainPropertyInfo property, // identifies property  
             ModelBusReference reference) // invalid reference  
    {   
      context.LogError(string.Format(INVALID_REF_FORMAT,   
             property.Name,   
             referenceState.Name,   
             new ModelBusReferenceTypeConverter().  
                 ConvertToInvariantString(reference)),   
         "Reference",   
         element);  
      });  
}}  
private const string INVALID_REF_FORMAT =   
    "The '{0}' domain property of ths ReferenceState instance "  
  + "named '{1}' contains reference value '{2}' which is invalid";  
```  
  
## <a name="actions-performed-by-the-modelbus-extension"></a>ModelBus 拡張機能により実行されるアクション  
 次の情報は必須ではありませんが、ModelBus を広く使用する場合に有用な場合があります。  
  
 ModelBus 拡張機能は DSL ソリューションで次の変更を加えます。  
  
 DSL 定義図を右クリックするとクリックして**Modelbus の有効化**、し、 **、ModelBus を使用するには、この DSL を有効にする**:  
  
-   参照が追加、DSL プロジェクトで**Microsoft.VisualStudio.Modeling.Sdk.Integration.11.0.dll**  
  
-   DSL 定義に、外部型参照 `Microsoft.VisualStudio.Modeling.Integration.ModelBusReference` が追加されます。  
  
     内の参照を確認できます**DSL エクスプ ローラー****ドメイン型**します。 外部型参照を手動で追加するには、ルート ノードを右クリックします。  
  
-   新しいテンプレート ファイルを追加すると、 **Dsl\GeneratedCode\ModelBusReferencesSerialization.tt**します。  
  
 Modelbusreference ドメイン プロパティの型を設定し、しプロパティを右クリックしてをクリックして**を有効にする ModelBusReference 固有プロパティ**:  
  
-   ドメイン プロパティにいくつかの CLR 属性が追加されます。 それらはプロパティ ウィンドウの Custom Attributes フィールドで確認できます。 **Dsl\GeneratedCode\DomainClasses.cs**、プロパティ宣言で属性を確認できます。  
  
    ```  
    [System.ComponentModel.TypeConverter(typeof(  
    Microsoft.VisualStudio.Modeling.Integration.ModelBusReferenceTypeConverter))]  
    [System.ComponentModel.Editor(typeof(  
      Microsoft.VisualStudio.Modeling.Integration.Picker  
      .ModelReferenceEditor // or ModelElementReferenceEditor  
      ), typeof(System.Drawing.Design.UITypeEditor))]  
    [Microsoft.VisualStudio.Modeling.Integration.Picker  
      .SupplyFileBasedBrowserConfiguration  
      ("Choose a model file", "Target model|*.target")]  
    ```  
  
 DSL 定義図では、右クリックしたときにをクリックして**ModelBus の有効化**、選び**この DSL を ModelBus に公開**:  
  
-   ソリューションに新しいプロジェクト `ModelBusAdapter` が追加されます。  
  
-   `ModelBusAdapter` プロジェクトに `DslPackage` への参照が追加されます。 `ModelBusAdapter` は `Dsl` プロジェクトへの参照を持ちます。  
  
-   **DslPackage\source.extention.tt**、 `|ModelBusAdapter|` MEF コンポーネントとして追加されます。  
  
## <a name="see-also"></a>関連項目  
 [方法: プログラム コード内のファイルからモデルを開く](../modeling/how-to-open-a-model-from-file-in-program-code.md)   
 [UML モデルを他のモデルおよびツールと統合します。](../modeling/integrate-uml-models-with-other-models-and-tools.md)   
 [方法: ドラッグ アンド ドロップ ハンドラーを追加](../modeling/how-to-add-a-drag-and-drop-handler.md)   
 [テキスト テンプレートでの Visual Studio ModelBus の使用](../modeling/using-visual-studio-modelbus-in-a-text-template.md)



