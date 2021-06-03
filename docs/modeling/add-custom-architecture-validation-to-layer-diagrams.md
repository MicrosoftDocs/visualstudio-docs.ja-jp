---
title: カスタム アーキテクチャ検証を依存関係図に追加する
description: カスタム アーキテクチャ検証を依存関係図に追加する方法について説明します。
ms.date: 11/04/2016
ms.topic: how-to
titleSuffix: ''
helpviewer_keywords:
- dependency diagrams, adding custom validation
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: SEO-VS-2020
ms.workload:
- multiple
ms.openlocfilehash: bd5f17e7e8c12da1d4e01738c26650a3df4760fa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99919320"
---
# <a name="add-custom-architecture-validation-to-dependency-diagrams"></a>カスタム アーキテクチャ検証を依存関係図に追加する

Visual Studio では、ユーザーはプロジェクトのソース コードをレイヤー モデルと対比して検証し、ソース コードが依存関係図の依存関係に準拠していることを確認できます。 標準の検証アルゴリズムがありますが、独自の検証拡張機能を定義できます。

ユーザーが依存関係図で **[アーキテクチャの検証]** を選択すると、標準の検証メソッドが呼び出された後、インストールされている検証拡張機能が呼び出されます。

> [!NOTE]
> 依存関係図での検証の主要な目的は、図と、ソリューションの他の部分のプログラム コードを比較することです。

レイヤー検証拡張機能を Visual Studio Integration Extension (VSIX) にパッケージ化し、他の Visual Studio ユーザーに配布できます。 検証機能は、単独で VSIX に配置することも、他の拡張機能と組み合わせて同じ VSIX に含めることもできます。 検証コントロールのコードは、他の拡張機能と同じプロジェクトではなく、専用の Visual Studio プロジェクトで作成する必要があります。

> [!WARNING]
> 検証プロジェクトを作成したら、このトピックの最後にある [コード例](#example) をコピーし、各自のニーズに合わせて編集してください。

## <a name="requirements"></a>必要条件

「 [要件](../modeling/extend-layer-diagrams.md#requirements)」を参照してください。

## <a name="defining-a-layer-validator-in-a-new-vsix"></a>新しい VSIX でレイヤー検証コントロールを定義する

最も簡単に検証コントロールを作成するには、プロジェクト テンプレートを使用します。 この方法では、コードと VSIX マニフェストが同じプロジェクトに配置されます。

### <a name="to-define-an-extension-by-using-a-project-template"></a>プロジェクト テンプレートを使用して拡張機能を定義するには

1. 新しい **レイヤー デザイナー検証拡張機能** プロジェクトを作成します。

    このテンプレートでは、小さい例を含むプロジェクトが作成されます。

   > [!WARNING]
   > テンプレートを正常に機能させるには:
   >
   > - `LogValidationError` の呼び出しを編集し、省略可能な引数 `errorSourceNodes` と `errorTargetNodes`を削除します。
   > - カスタム プロパティを使用する場合は、「[依存関係図へのカスタム プロパティの追加](../modeling/add-custom-properties-to-layer-diagrams.md)」で説明されている更新プログラムを適用します。

2. コードを編集して検証を定義します。 詳細については、「 [検証のプログラミング](#programming)」を参照してください。

3. 拡張機能をテストするには、「 [レイヤー検証のデバッグ](#debugging)」を参照してください。

   > [!NOTE]
   > メソッドは特定の状況においてのみ呼び出され、ブレークポイントは自動的には動作しません。 詳細については、「 [レイヤー検証のデバッグ](#debugging)」を参照してください。

::: moniker range="vs-2017"

4. Visual Studio のメイン インスタンスまたは別のコンピューターに拡張機能をインストールするには、*bin* ディレクトリで *.vsix* ファイルを探します。 このファイルをインストール先のコンピューターにコピーして、ダブルクリックします。 拡張機能をアンインストールするには、 **[ツール]** メニューの **[拡張機能と更新プログラム]** を選択します。

::: moniker-end

::: moniker range=">=vs-2019"

4. Visual Studio のメイン インスタンスまたは別のコンピューターに拡張機能をインストールするには、*bin* ディレクトリで *.vsix* ファイルを探します。 このファイルをインストール先のコンピューターにコピーして、ダブルクリックします。 アンインストールするには、 **[拡張機能]** メニューの **[拡張機能の管理]** を選択します。

::: moniker-end

## <a name="adding-a-layer-validator-to-a-separate-vsix"></a>レイヤー検証コントロールを別の VSIX に追加する

レイヤー検証コントロール、コマンド、および他の拡張機能を含む 1 つの VSIX を作成する場合は、VSIX を定義するプロジェクトとハンドラー用のプロジェクトを別にすることをお勧めします。

### <a name="to-add-layer-validation-to-a-separate-vsix"></a>レイヤー検証を別の VSIX に追加するには

1. 新しい **クラス ライブラリ** プロジェクトを作成します。 このプロジェクトには、レイヤー検証クラスが含められます。

2. ソリューションで **VSIX プロジェクト** を検索または作成します。 VSIX プロジェクトには、 **source.extension.vsixmanifest** という名前のファイルが含まれます。

3. **ソリューション エクスプローラー** の VSIX プロジェクトの右クリック メニューで、 **[スタートアップ プロジェクトに設定]** を選択します。

4. **source.extension.vsixmanifest** の **[アセット]** で、レイヤー検証プロジェクトを MEF コンポーネントとして追加します。

    1. **[新規]** を選択します。

    2. **[Add New Asset]** (新しいアセットの追加) ダイアログ ボックスで、次のように設定します。

         **[種類]**  = **Microsoft.VisualStudio.MefComponent**

         **[ソース]**  = **現在のソリューション内のプロジェクト**

         **[プロジェクト]**  = *検証プロジェクト*

5. また、このプロジェクトをレイヤー検証として追加する必要があります。

    1. **[新規]** を選択します。

    2. **[Add New Asset]** (新しいアセットの追加) ダイアログ ボックスで、次のように設定します。

         **[種類]**  = **Microsoft.VisualStudio.ArchitectureTools.Layer.Validator**」を参照してください。 これは、ドロップダウン リストのオプションの 1 つではありません。 キーボードで入力する必要があります。

         **[ソース]**  = **現在のソリューション内のプロジェクト**

         **[プロジェクト]**  = *検証プロジェクト*

6. レイヤー検証プロジェクトに戻り、次のプロジェクト参照を追加します。

    |**参照**|**実行できる操作**|
    |-|-|
    |Microsoft.VisualStudio.GraphModel.dll|アーキテクチャ グラフを読み取る|
    |Microsoft.VisualStudio.ArchitectureTools.Extensibility.CodeSchema.dll|レイヤーと関連付けられているコード DOM を読み取る|
    |Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer.dll|レイヤー モデルを読み取る|
    |Microsoft.VisualStudio.ArchitectureTools.Extensibility|図形と図を読み取って更新する|
    |System.ComponentModel.Composition|MEF (Managed Extensibility Framework) を使用して検証コンポーネントを定義する|
    |Microsoft.VisualStudio.Modeling.Sdk.[バージョン]|モデリング拡張機能を定義する|

7. このトピックの最後にあるコード例を、検証ライブラリ プロジェクトのクラス ファイルにコピーして、検証のコードが含まれるようにします。 詳細については、「 [検証のプログラミング](#programming)」を参照してください。

8. 拡張機能をテストするには、「 [レイヤー検証のデバッグ](#debugging)」を参照してください。

    > [!NOTE]
    > メソッドは特定の状況においてのみ呼び出され、ブレークポイントは自動的には動作しません。 詳細については、「 [レイヤー検証のデバッグ](#debugging)」を参照してください。

9. Visual Studio のメイン インスタンスまたは別のコンピューターに拡張機能をインストールするには、VSIX プロジェクトの **bin** ディレクトリで **.vsix** ファイルを探します。 このファイルを、VSIX をインストールするコンピューターにコピーします。 Windows エクスプローラーで、VSIX ファイルをダブルクリックします。

## <a name="programming-validation"></a><a name="programming"></a> 検証のプログラミング

レイヤー検証拡張機能を定義するには、以下の特性を備えたクラスを定義します。

- 宣言の全体的な形式を次に示します。

  ```csharp
  using System.ComponentModel.Composition;
  using Microsoft.VisualStudio.ArchitectureTools.Extensibility.CodeSchema;
  using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
  using Microsoft.VisualStudio.GraphModel;
  ...
   [Export(typeof(IValidateArchitectureExtension))]
    public partial class Validator1Extension :
                    IValidateArchitectureExtension
    {
      public void ValidateArchitecture(Graph graph)
      {
         GraphSchema schema = graph.DocumentSchema;
        ...
    } }
  ```

- エラーを検出したときは、 `LogValidationError()`を使用して報告できます。

  > [!WARNING]
  > `LogValidationError`の省略可能なパラメーターを使用しないでください。

ユーザーが **[アーキテクチャの検証]** を実行すると、レイヤーのランタイム システムがレイヤーとその成果物を分析して、グラフを生成します。 グラフは 4 つの部分で構成されます。

- Visual Studio ソリューションのレイヤー モデルは、グラフではノードとリンクとして表されます。

- ソリューションで定義されているコード、プロジェクト アイテム、および他の成果物は、ノードおよび分析システムによって検出された依存関係を示すリンクとして表されます。

- レイヤー ノードからコード成果物ノードへのリンク。

- 検証コントロールによって検出されたエラーを表すノード。

グラフが作成されると、標準の検証メソッドが呼び出されます。 これが完了すると、インストールされているすべての拡張検証メソッドが、不定の順序で呼び出されます。 グラフを渡された各 `ValidateArchitecture` メソッドは、グラフをスキャンし、検出したエラーを報告します。

> [!NOTE]
> これは、ドメイン固有言語で使用できる検証プロセスと同じではありません。

検証メソッドでは、レイヤー モデルまたは検証対象のコードを変更することはできません。

グラフ モデルは、 <xref:Microsoft.VisualStudio.GraphModel>で定義されています。 そのプリンシパル クラスは、 <xref:Microsoft.VisualStudio.GraphModel.GraphNode> および <xref:Microsoft.VisualStudio.GraphModel.GraphLink>です。

各ノードおよび各リンクには 1 つ以上のカテゴリがあり、それぞれが表す要素または関係の種類が指定されています。 標準的なグラフのノードには以下のカテゴリがあります。

- Dsl.LayerModel

- Dsl.Layer

- Dsl.Reference

- CodeSchema_Type

- CodeSchema_Namespace

- CodeSchema_Type

- CodeSchema_Method

- CodeSchema_Field

- CodeSchema_Property

レイヤーからコード内の要素へのリンクのカテゴリは "Represents" です。

## <a name="debugging-validation"></a><a name="debugging"></a> 検証のデバッグ

レイヤー検証拡張機能をデバッグするには、Ctrl キーを押しながら F5 キーを押します。 Visual Studio の実験用インスタンスが開きます。 このインスタンスで、レイヤー モデルを開くか作成します。 このモデルは、コードと関連付けられている必要があり、少なくとも 1 つの依存関係を含む必要があります。

### <a name="test-with-a-solution-that-contains-dependencies"></a>依存関係を含むソリューションでのテスト

以下の特性が存在していない限り、検証は実行されません。

- 依存関係図に、少なくとも 1 つの依存関係リンクが存在する。

- コード要素と関連付けられたレイヤーがモデルに存在する。

初めて Visual Studio の実験用インスタンスを起動して検証拡張機能をテストするときは、これらの特性を備えたソリューションを開くか作成します。

### <a name="run-clean-solution-before-validate-architecture"></a>アーキテクチャを検証する前に [ソリューションのクリーン] を実行する

検証コードを更新したときは常に、検証コマンドをテストする前に、実験用ソリューションで **[ビルド]** メニューの **[ソリューションのクリーン]** を使用します。 これは、検証の結果がキャッシュされているために必要です。 テスト依存関係図またはそのコードが更新されていない場合は、検証メソッドは実行されません。

### <a name="launch-the-debugger-explicitly"></a>デバッガーを明示的に起動する

検証は別のプロセスで実行されます。 したがって、検証メソッド内のブレークポイントはトリガーされません。 検証が開始したら、デバッガーをプロセスに明示的にアタッチする必要があります。

デバッガーを検証プロセスにアタッチするには、検証メソッドの先頭に `System.Diagnostics.Debugger.Launch()` の呼び出しを挿入します。 デバッグ ダイアログ ボックスが表示されたら、Visual Studio のメイン インスタンスを選択します。

または、 `System.Windows.Forms.MessageBox.Show()`の呼び出しを挿入してもかまいません。 メッセージ ボックスが表示されたら、Visual Studio のメイン インスタンスに移動し、 **[デバッグ]** メニューの **[プロセスにアタッチ]** をクリックします。 **Graphcmd.exe** という名前のプロセスを選択します。

常に、Ctrl キーを押しながら F5 キーを押して (**[デバッグなしで開始]**) 実験用インスタンスを起動します。

### <a name="deploying-a-validation-extension"></a>検証拡張機能を配置する

適切なバージョンの Visual Studio がインストールされているコンピューターに検証拡張機能をインストールするには、ターゲット コンピューターで VSIX ファイルを開きます。

## <a name="example-code"></a><a name="example"></a> Example code

```csharp
using System;
using System.ComponentModel.Composition;
using System.Globalization;
using System.Linq;
using System.Text.RegularExpressions;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.CodeSchema;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Layer;
using Microsoft.VisualStudio.GraphModel;

namespace Validator3
{
    [Export(typeof(IValidateArchitectureExtension))]
    public partial class Validator3Extension : IValidateArchitectureExtension
    {
        /// <summary>
        /// Validate the architecture
        /// </summary>
        /// <param name="graph">The graph</param>
        public void ValidateArchitecture(Graph graph)
        {
            if (graph == null) throw new ArgumentNullException("graph");

            // Uncomment the line below to debug this extension during validation
            // System.Windows.Forms.MessageBox.Show("Attach 2 to GraphCmd.exe with process id " + System.Diagnostics.Process.GetCurrentProcess().Id);

            // Get all layers on the diagram
            foreach (GraphNode layer in graph.Nodes.GetByCategory("Dsl.Layer"))
            {
                System.Threading.Thread.Sleep(100);
                // Get the required regex property from the layer node
                string regexPattern = "^[a-zA-Z]+$"; //layer[customPropertyCategory] as string;
                if (!string.IsNullOrEmpty(regexPattern))
                {
                    Regex regEx = new Regex(regexPattern);

                    // Get all referenced types in this layer including those from nested layers so each
                    // type is validated against all containing layer constraints.
                    foreach (GraphNode containedType in layer.FindDescendants().Where(node => node.HasCategory("CodeSchema_Type")))
                    {
                        // Check the type name against the required regex
                        CodeGraphNodeIdBuilder builder = new CodeGraphNodeIdBuilder(containedType.Id, graph);
                        string typeName = builder.Type.Name;
                        if (!regEx.IsMatch(typeName))
                        {
                            // Log an error
                            string message = string.Format(CultureInfo.CurrentCulture, Resources.InvalidTypeNameMessage, typeName);
                            this.LogValidationError(graph, typeName + "TypeNameError", message, GraphErrorLevel.Error, layer);
                        }
                    }
                }

            }

        }
    }
}
```

## <a name="see-also"></a>関連項目

- [依存関係図の拡張](../modeling/extend-layer-diagrams.md)
