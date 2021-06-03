---
title: Windows フォームに基づくドメイン固有言語を作成する
description: Windows フォームを使用してドメイン固有言語モデルの状態を表示する方法について説明します。
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: 41c3ba299df1e6f9ce0e2848f7ffad59e5b3fbea
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99945410"
---
# <a name="create-a-windows-forms-based-domain-specific-language"></a>Windows フォームに基づくドメイン固有言語を作成する

DSL 図を使用する代わりに Windows フォームを使用して、ドメイン固有言語 (DSL) モデルの状態を表示できます。 このトピックでは、Visual Studio Visualization and Modeling SDK を使用して Windows フォームを DSL にバインドする手順について説明します。

次の図は、ある DSL インスタンスの Windows フォーム UI とモデル エクスプローラーを示しています。

![Visual Studio での DSL インスタンス](../modeling/media/dsl-wpf-2.png)

## <a name="create-a-windows-forms-dsl"></a>Windows フォームの DSL を作成する

**最小 WinForm デザイナー** DSL テンプレートでは、独自の要件に合わせて変更できる最小限の DSL を作成できます。

1. **最小 WinForm デザイナー** テンプレートから DSL を作成します。

    このチュートリアルでは、次の名前を想定しています。

    - ソリューションと DSL の名前: `FarmApp`
    - 名前空間: `Company.FarmApp`

2. テンプレートに用意されている最初の例を試します。

   1. [すべてのテンプレートの変換] を実行します。

   2. サンプルをビルドして実行します (**Ctrl**+**F5** キー)。

   3. Visual Studio の実験用インスタンスで、デバッグ プロジェクト内の `Sample` ファイルを開きます。

        これが Windows フォーム コントロールに表示されていることを確認してください。

        また、モデルの要素がエクスプローラーに表示されていることも確認できます。

        フォームまたはエクスプローラーのどちらか一方でいくつかの要素を追加し、それらが他方の表示画面に表示されていることを確認します。

   Visual Studio の主要なインスタンスでは、DSL ソリューションに関する次の点にご注意ください。

- `DslDefinition.dsl` にはダイアグラム要素が含まれていません。 この DSL のインスタンス モデルの表示には DSL 図を使用しないためです。 代わりに、Windows フォームをモデルにバインドすると、フォーム上の要素にモデルが表示されます。

- `Dsl` および `DslPackage` プロジェクトに加えて、このソリューションには `UI.` という名前の 3 つ目のプロジェクトも含まれています。**UI** プロジェクトには、Windows フォーム コントロールの定義が含まれています。 `DslPackage` は `UI` に依存しており、`UI` は `Dsl` に依存しています。

- `DslPackage` プロジェクトの `UI\DocView.cs` には、`UI` プロジェクトで定義されている Windows フォーム コントロールを表示するコードが含まれています。

- `UI` プロジェクトには、DSL にバインドされたフォーム コントロールの作業用サンプルが含まれています。 ただし、DSL 定義を変更した場合は機能しなくなります。 `UI` プロジェクト名には以下が含まれています。

  - `ModelViewControl` という名前の Windows フォーム クラス。

  - `ModelViewControl` の追加の部分定義を含む、`DataBinding.cs` という名前のファイル。 その内容を確認するには、**ソリューション エクスプローラー** で、そのファイルのショートカット メニューを開き、 **[コードの表示]** を選択します。

### <a name="about-the-ui-project"></a>UI プロジェクトについて

DSL 定義ファイルを更新して独自の DSL を定義する場合は、その DSL を表示するように `UI` プロジェクト内のコントロールを更新する必要があります。 `Dsl` や `DslPackage` のプロジェクトとは異なり、`DslDefinitionl.dsl` から `UI` のサンプル プロジェクトは生成されません。 必要に応じて、.tt ファイルを追加してコードを生成できます (ただし、これについては、このチュートリアルでは説明しません)。

## <a name="update-the-dsl-definition"></a>DSL 定義を更新する

次の図は、このチュートリアルで使用する DSL 定義を示しています。

![DSL 定義](../modeling/media/dsl-wpf-1.png)

1. DSL デザイナーで DslDefinition.dsl を開きます。

2. **ExampleElement** を削除します

3. **ExampleModel** ドメイン クラスの名前を `Farm` に変更します。

     これに、`Size` という名前の **Int32** 型と、`IsOrganic` という名前の **Boolean** 型の追加のドメイン プロパティを指定します。

    > [!NOTE]
    > ルート ドメイン クラスを削除してから新しいルートを作成する場合は、[エディターのルート クラス] プロパティをリセットする必要があります。 **DSL エクスプローラー** で、 **[エディター]** を選択します。 次に、プロパティ ウィンドウで、 **[ルート クラス]** を `Farm` に設定します。

4. **[名前付きドメイン クラス]** ツールを使用して、次のドメイン クラスを作成します。

    - `Field` - これに `Size` という名前の追加のドメイン プロパティを指定します。

    - `Animal` - プロパティ ウィンドウで、 **[継承修飾子]** を **[抽象]** に設定します。

5. **[ドメイン クラス]** ツールを使用して、次のクラスを作成します。

    - `Sheep`

    - `Goat`

6. **[継承]** ツールを使用して、`Goat` と `Sheep` を `Animal` から継承させます。

7. **[埋め込み]** ツールを使用して、`Field` と `Animal` を `Farm` の下に埋め込みます。

8. 図を整理することをお勧めします。 重複する要素の数を減らすには、リーフ要素のショートカット メニュー上の **[ここにサブツリーを表示]** を使用します。

9. ソリューション エクスプローラーのツールバーで **[すべてのテンプレートの変換]** を実行します。

10. **Dsl** プロジェクトをビルドします。

    > [!NOTE]
    > この段階では、他のプロジェクトはエラーのない状態でビルドされません。 ただし、Dsl プロジェクトは、データ ソース ウィザードでそのアセンブリを使用できるようにビルドする必要があります。

## <a name="update-the-ui-project"></a>UI プロジェクトを更新する

DSL モデルに格納されている情報を表示する新しいユーザー コントロールを作成できるようになりました。 ユーザー コントロールをモデルに接続する最も簡単な方法は、データ バインディングを使用することです。 **ModelingBindingSource** という名前のデータ バインディング アダプター タイプは、DSL を VMSDK 以外のインターフェイスに接続するように特別に設計されています。

### <a name="define-your-dsl-model-as-a-data-source"></a>DSL モデルをデータ ソースとして定義する

1. **[データ]** メニューの **[データ ソースの表示]** をクリックします。

     **[データ ソース]** ウィンドウが開きます。

     **[新しいデータ ソースの追加]** を選択します。 **データ ソース構成ウィザード** が開きます。

2. **[オブジェクト]** 、 **[次へ]** の順に選択します。

     **[Dsl]** 、 **[Company.FarmApp]** の順に展開し、モデルのルート クラスである **[Farm]** を選択します。 **[完了]** を選択します。

     ソリューション エクスプローラーでは、**UI** プロジェクトに **Properties\DataSources\Farm.datasource** が含まれるようになりました

     モデル クラスのプロパティとリレーションシップが [データ ソース] ウィンドウに表示されます。

     ![[データ ソース] ウィンドウ](../modeling/media/dslwpf-3.png)

### <a name="connect-your-model-to-a-form"></a>モデルをフォームに接続する

1. **UI** プロジェクトで、既存の .cs ファイルをすべて削除します。

2. `FarmControl` という名前の新しい **ユーザー コントロール** ファイルを **UI** プロジェクトに追加します。

3. **[データ ソース]** ウィンドウの **[Farm]** のドロップダウン メニューで、 **[詳細]** を選択します。

    他のプロパティの既定の設定はそのままにします。

4. デザイン ビューで FarmControl.cs を開きます。

    [データ ソース] ウィンドウから FarmControl に **[Farm]** をドラッグします。

    一連のコントロールが、各プロパティに 1 つずつ表示されます。 リレーションシップのプロパティでは、コントロールは生成されません。

5. **[farmBindingNavigator]** を削除します。 これは `FarmControl` デザイナーでも自動的に生成されますが、このアプリケーションには役立ちません。

6. ツールボックスを使用して、 **[DataGridView]** のインスタンスを 2 つ作成し、「`AnimalGridView`」および「`FieldGridView`」という名前を付けます。

   > [!NOTE]
   > 代替手順として、[データ ソース] ウィンドウからそのコントロールに [Animals] と [Fields] の各項目をドラッグすることもできます。 このアクションにより、グリッド ビューとデータ ソースの間にデータ グリッドおよびバインディングが自動的に作成されます。 ただし、このバインディングは DSL では正しく機能しません。 そのため、データ グリッドおよびバインディングは手動で作成することをお勧めします。

7. ツールボックスに **[ModelingBindingSource]** ツールが含まれていない場合は、それを追加します。 **[データ]** タブのショートカット メニューで、 **[項目の選択]** を選択します。 **[ツールボックス項目の選択]** ダイアログで、 **[.NET Framework]** タブの **[ModelingBindingSource]** を選択します。

8. ツールボックスを使用して、 **[ModelingBindingSource]** のインスタンスを 2 つ作成し、「`AnimalBinding`」および「`FieldBinding`」という名前を付けます。

9. 各 **[ModelingBindingSource]** の **[データ ソース]** プロパティを **[farmBindingSource]** に設定します。

     **[データ メンバー]** プロパティを **[Animals]** または **[Fields]** に設定します。

10. `AnimalGridView` と `FieldGridView` の **[データ ソース]** プロパティをそれぞれ `AnimalBinding` と `FieldBinding` に設定します。

11. Farm コントロールのレイアウトをご自分の好みに合わせて調整します。

    **ModelingBindingSource** は、DSL に固有のいくつかの機能を実行するアダプターです。

- VMSDK ストア トランザクション内の更新をラップします。

   たとえば、ユーザーがデータ ビュー グリッドから行を削除すると、通常のバインディングではトランザクション例外が発生します。

- ユーザーが行を選択するときに、データ グリッド行ではなく、対応するモデル要素のプロパティがプロパティ ウィンドウに表示されるようにします。

  ![DSL バインディングのスキーマ](../modeling/media/dslwpf4.png)
  
  データ ソースとビューの間のリンクのスキーマ。

### <a name="complete-the-bindings-to-the-dsl"></a>DSL へのバインドを完了する

1. **UI** プロジェクト内の別のコード ファイルに次のコードを追加します。

    ```csharp
    using System.ComponentModel;
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Design;

    namespace Company.FarmApp
    {
      partial class FarmControl
      {
        public IContainer Components { get { return components; } }

        /// <summary>Binds the WinForms data source to the DSL model.
        /// </summary>
        /// <param name="nodelRoot">The root element of the model.</param>
        public void DataBind(ModelElement modelRoot)
        {
          WinFormsDataBindingHelper.PreInitializeDataSources(this);
          this.farmBindingSource.DataSource = modelRoot;
          WinFormsDataBindingHelper.InitializeDataSources(this);
        }
      }
    }
    ```

2. **DslPackage** プロジェクトで、次の変数定義を更新するように **DslPackage\DocView.tt** を編集します。

    ```csharp
    string viewControlTypeName = "FarmControl";
    ```

## <a name="test-the-dsl"></a>DSL をテストする

DSL ソリューションをビルドして実行できるようになりましたが、後でさらに改善を加えることもできます。

1. ソリューションをビルドして実行します。

2. Visual Studio の実験用インスタンスで、**Sample** ファイルを開きます。

3. **FarmApp エクスプローラー** で、 **[Farm]** ルート ノードのショートカット メニューを開き、 **[Add New Goat]** を選択します。

     `Goat1` が **[Animals]** ビューに表示されます。

    > [!WARNING]
    > **[Animals]** ノードではなく、 **[Farm]** ノードのショートカット メニューを使用する必要があります。

4. **[Farm]** ルート ノードを選択し、そのプロパティを表示します。

     フォーム ビューで、Farm の **[Name]** または **[Size]** を変更します。

     フォームの各フィールドから移動すると、対応するプロパティがプロパティ ウィンドウ内で変更されます。

## <a name="enhance-the-dsl"></a>DSL を拡張する

### <a name="make-the-properties-update-immediately"></a>プロパティを直ちに更新する

1. FarmControl.cs のデザイン ビューで、[Name]、[Size]、[IsOrganic] などの単純なフィールドを選択します。

2. プロパティ ウィンドウで、 **[DataBindings]** を展開して **[(詳細)]** を開きます。

     **[フォーマットと詳細バインド]** ダイアログの **[データ ソース更新モード]** で、 **[OnPropertyChanged]** を選択します。

3. ソリューションをビルドして実行します。

     フィールドの内容を変更すると、Farm モデルの対応するプロパティがすぐに変更されることを確認します。

### <a name="provide-add-buttons"></a>ボタンの追加機能を提供する

1. FarmControl.cs のデザイン ビューで、ツールボックスを使用してフォーム上にボタンを作成します。

    そのボタンの名前やテキストを (`New Sheep` などに) 編集します。

2. (ボタンをダブルクリックするなどして) ボタンの背後にあるコードを開きます。

    次のように編集します。

   ```csharp
   private void NewSheepButton_Click(object sender, EventArgs e)
   {
     using (Transaction t = farm.Store.TransactionManager.BeginTransaction("Add sheep"))
     {
       elementOperations.MergeElementGroup(farm,
         new ElementGroup(new Sheep(farm.Partition)));
       t.Commit();
     }
   }

   // The following code is shared with other add buttons:
   private ElementOperations operationsCache = null;
   private ElementOperations elementOperations
   {
     get
     {
       if (operationsCache == null)
       {
         operationsCache = new ElementOperations(farm.Store, farm.Partition);
       }
       return operationsCache;
     }
   }
   private Farm farm
   {
     get { return this.farmBindingSource.DataSource as Farm; }
   }
   ```

    次のディレクティブを挿入する必要もあります。

   ```csharp

   using Microsoft.VisualStudio.Modeling;
   ```

3. Goats と Fields についても同様のボタンを 追加します。

4. ソリューションをビルドして実行します。

5. 新規作成のボタンによって項目が追加されることを確認します。 FarmApp エクスプローラーと適切なデータ グリッド ビューの両方に新しい項目が表示されます。

    データ グリッド ビューでその要素の名前を編集できます。 そこから削除することもできます。

   ![データ グリッド ビューのサンプル](../modeling/media/dsl-wpf-2.png)

### <a name="about-the-code-to-add-an-element"></a>要素を追加するコードについて

新しい要素のボタンについては、次の代替コードの方がややシンプルです。

```csharp
private void NewSheepButton_Click(object sender, EventArgs e)
{
  using (Transaction t = farm.Store.TransactionManager.BeginTransaction("Add sheep"))
  {
    farm.Animals.Add(new Sheep(farm.Partition)); ;
    t.Commit();
  }
}
```

ただし、このコードでは、新しい項目の既定の名前は設定されません。 DSL の **要素マージ ディレクティブ** で定義した可能性のあるカスタマイズされたマージは実行されず、定義されている可能性のあるカスタム マージ コードも実行されません。

そのため、<xref:Microsoft.VisualStudio.Modeling.ElementOperations> を使用して新しい要素を作成することをお勧めします。 詳細については、「[要素作成処理および要素移動処理のカスタマイズ](../modeling/customizing-element-creation-and-movement.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)
- [ドメイン固有言語をカスタマイズするコードを記述する](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [Modeling SDK for Visual Studio - ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)
