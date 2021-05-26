---
title: ソリューション エクスプローラーのフィルターの拡張 | Microsoft Docs
description: Visual Studio SDK で、ソリューション エクスプローラー フィルター機能を拡張して、さまざまなファイルを表示または非表示にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Solution Explorer, extending
- extensibility [Visual Studio], projects and solutions
ms.assetid: df976c76-27ec-4f00-ab6d-a26a745dc6c7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d1256b807d67f95aa8ca1e952a4dca7bd550e0fc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075017"
---
# <a name="extend-the-solution-explorer-filter"></a>ソリューション エクスプローラーのフィルターを拡張する
**ソリューション エクスプローラー** フィルター機能を拡張して、さまざまなファイルを表示または非表示にすることができます。 たとえば、このチュートリアルで示すように、**ソリューション エクスプローラー** に C# クラス ファクトリ ファイルのみを表示するフィルターを作成できます。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

### <a name="create-a-visual-studio-package-project"></a>Visual Studio パッケージ プロジェクトを作成する

1. `FileFilter` という名前の VSIX プロジェクトを作成します。 **FileFilter** という名前のカスタム コマンド項目テンプレートを追加します。 詳細については、「[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. `System.ComponentModel.Composition` および `Microsoft.VisualStudio.Utilities` への参照を追加します。

3. メニュー コマンドが **ソリューション エクスプローラー** ツールバーに表示されるようにします。 *FileFilterPackage.vsct* ファイルを開きます。

4. `<Button>` ブロックを次のように変更します。

    ```xml
    <Button guid="guidFileFilterPackageCmdSet" id="FileFilterId" priority="0x0400" type="Button">
        <Parent guid="guidSHLMainMenu" id="IDG_VS_TOOLBAR_PROJWIN_FILTERS" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>FileNameFilter</ButtonText>
        </Strings>
    </Button>
    ```

### <a name="update-the-manifest-file"></a>マニフェスト ファイルを更新する

1. *source.extension.vsixmanifest* ファイルで、MEF コンポーネントであるアセットを追加します。

2. **[アセット]** タブで **[新規作成]** をクリックします。

3. **[種類]** フィールドで **[Microsoft.VisualStudio.MefComponent]** を選択します。

4. **[ソース]** フィールドで、 **[現在のソリューション内のプロジェクト]** を選択します。

5. **[プロジェクト]** フィールドで **[FileFilter]** を選択し、 **[OK]** をクリックします。

### <a name="add-the-filter-code"></a>フィルター コードを追加する

1. いくつかの GUID を *FileFilterPackageGuids.cs* ファイルに追加します。

    ```csharp
    public const string guidFileFilterPackageCmdSetString = "00000000-0000-0000-0000-00000000"; // get your GUID from the .vsct file
    public const int FileFilterId = 0x100;
    ```

2. *FileNameFilter.cs* という名前の FileFilter プロジェクトにクラス ファイルを追加します。

3. 空の名前空間と空のクラスを次のコードに置き換えます。

     `Task<IReadOnlyObservableSet> GetIncludedItemsAsync(IEnumerable<IVsHierarchyItem rootItems)` メソッドは、ソリューションのルート (`rootItems`) を含むコレクションを受け取り、フィルターに含める項目のコレクションを返します。

     `ShouldIncludeInFilter` メソッドは、指定した条件に基づいて、**ソリューション エクスプローラー** 階層内の項目をフィルター処理します。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Composition;
    using System.Text.RegularExpressions;
    using System.Threading.Tasks;
    using Microsoft.Internal.VisualStudio.PlatformUI;
    using Microsoft.VisualStudio.Shell;

    namespace FileFilter
    {
        // Implements ISolutionTreeFilterProvider. The SolutionTreeFilterProvider attribute declares it as a MEF component
        [SolutionTreeFilterProvider(FileFilterPackageGuids.guidFileFilterPackageCmdSetString, (uint)(FileFilterPackageGuids.FileFilterId))]
        public sealed class FileNameFilterProvider : HierarchyTreeFilterProvider
        {
            SVsServiceProvider svcProvider;
            IVsHierarchyItemCollectionProvider hierarchyCollectionProvider;

            // Constructor required for MEF composition
            [ImportingConstructor]
            public FileNameFilterProvider(SVsServiceProvider serviceProvider, IVsHierarchyItemCollectionProvider hierarchyCollectionProvider)
            {
                this.svcProvider = serviceProvider;
                this.hierarchyCollectionProvider = hierarchyCollectionProvider;
            }

            // Returns an instance of Create filter class.
            protected override HierarchyTreeFilter CreateFilter()
            {
                return new FileNameFilter(this.svcProvider, this.hierarchyCollectionProvider, FileNamePattern);
            }

            // Regex pattern for CSharp factory classes
            private const string FileNamePattern = @"\w*factory\w*(.cs$)";

            // Implementation of file filtering
            private sealed class FileNameFilter : HierarchyTreeFilter
            {
                private readonly Regex regexp;
                private readonly IServiceProvider svcProvider;
                private readonly IVsHierarchyItemCollectionProvider hierarchyCollectionProvider;

                public FileNameFilter(
                    IServiceProvider serviceProvider,
                    IVsHierarchyItemCollectionProvider hierarchyCollectionProvider,
                    string fileNamePattern)
                {
                    this.svcProvider = serviceProvider;
                    this.hierarchyCollectionProvider = hierarchyCollectionProvider;
                    this.regexp = new Regex(fileNamePattern, RegexOptions.IgnoreCase);
                }

                // Gets the items to be included from this filter provider.
                // rootItems is a collection that contains the root of your solution
                // Returns a collection of items to be included as part of the filter
                protected override async Task<IReadOnlyObservableSet> GetIncludedItemsAsync(IEnumerable<IVsHierarchyItem> rootItems)
                {
                    IVsHierarchyItem root = HierarchyUtilities.FindCommonAncestor(rootItems);
                    IReadOnlyObservableSet<IVsHierarchyItem> sourceItems;
                    sourceItems = await hierarchyCollectionProvider.GetDescendantsAsync(
                                        root.HierarchyIdentity.NestedHierarchy,
                                        CancellationToken);

                    IFilteredHierarchyItemSet includedItems = await hierarchyCollectionProvider.GetFilteredHierarchyItemsAsync(
                        sourceItems,
                        ShouldIncludeInFilter,
                        CancellationToken);
                    return includedItems;
                }

                // Returns true if filters hierarchy item name for given filter; otherwise, false</returns>
                private bool ShouldIncludeInFilter(IVsHierarchyItem hierarchyItem)
                {
                    if (hierarchyItem == null)
                    {
                        return false;
                    }
                    return this.regexp.IsMatch(hierarchyItem.Text);
                }
            }
        }
    }

    ```

4. *FileFilter.cs* で、FileFilter コンストラクターからコマンド配置および処理コードを削除します。 結果は次のようになるはずです。

    ```csharp
    private FileFilter(Package package)
    {
        if (package == null)
        {
            throw new ArgumentNullException("package");
        }

        this.package = package;
    }
    ```

     `ShowMessageBox()` メソッドも削除します。

5. *FileFilterPackage.cs* で、`Initialize()` メソッド内のコードを次のコードに置き換えます。

    ```csharp
    protected override void Initialize()
    {
        Debug.WriteLine (string.Format(CultureInfo.CurrentCulture, "Entering Initialize() of: {0}", this.ToString()));
        base.Initialize();
    }
    ```

### <a name="test-your-code"></a>コードをテストする

1. プロジェクトをビルドして実行します。 Visual Studio の 2 番目のインスタンスが表示されます。 これは実験用インスタンスと呼ばれます。

2. Visual Studio の実験用インスタンスで、C# プロジェクトを開きます。

3. **ソリューション エクスプローラー** ツールバーで追加したボタンを探します。 左側から 4 番目のボタンになるはずです。

4. このボタンをクリックすると、すべてのファイルがフィルターで除外され、 **[すべての項目がビューからフィルターされました。]** と **ソリューション エクスプローラー** に表示されるはずです。
