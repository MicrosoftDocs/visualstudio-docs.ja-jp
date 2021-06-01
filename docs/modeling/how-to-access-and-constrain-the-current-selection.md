---
title: '方法: 現在の選択項目を表示および制限する'
description: ドメイン固有言語用のコマンドまたはジェスチャ ハンドラーを記述するときに、ユーザーが右クリックした要素を特定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Domain-Specific Language, accessing the current selection
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 83903c8ff911fdd1d4900714137a7f6976513dad
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99890566"
---
# <a name="how-to-access-and-constrain-the-current-selection"></a>方法: 現在の選択項目を表示および制限する

ドメイン固有言語用のコマンドまたはジェスチャ ハンドラーを記述するときに、ユーザーが右クリックした要素を特定できます。 また、一部の図形またはフィールドが選択されないようにすることもできます。 たとえば、ユーザーがアイコン デコレーターをクリックしたときに、それが含まれる図形が代わりに選択されるようにすることができます。 この方法で選択を制限すると、記述する必要のあるハンドラーの数が減ります。 また、それによってユーザーも楽になり、デコレーターを避けることなく、図形内の任意の場所をクリックできるようになります。

## <a name="access-the-current-selection-from-a-command-handler"></a>コマンド ハンドラーから現在の選択項目にアクセスする

ドメイン固有言語のコマンド セット クラスには、カスタム コマンド用のコマンド ハンドラーが含まれています。 ドメイン固有言語のコマンド セット クラスの派生元である <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> クラスにより、現在の選択項目にアクセスするためのいくつかのメンバーが提供されています。

コマンド ハンドラーでは、コマンドに応じて、モデル デザイナー、モデル エクスプローラー、またはアクティブ ウィンドウに選択項目が含まれることが必要になる場合があります。

### <a name="to-access-selection-information"></a>選択情報にアクセスするには

1. <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> クラスで定義されている次のメンバーを使用して、現在の選択項目にアクセスできます。

    |メンバー|説明|
    |-|-|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsAnyDocumentSelectionCompartment%2A> メソッド|モデル デザイナーで選択されているいずれかの要素がコンパートメント シェイプである場合は、`true` を返します。それ以外の場合は `false` を返します。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsDiagramSelected%2A> メソッド|モデル デザイナーでダイアグラムが選択されている場合は、`true` を返します。それ以外の場合は `false` を返します。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleDocumentSelection%2A> メソッド|モデル デザイナーで厳密に 1 つの要素が選択されている場合は、`true` を返します。それ以外の場合は `false` を返します。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleSelection%2A> メソッド|アクティブ ウィンドウで厳密に 1 つの要素が選択されている場合は、`true` を返します。それ以外の場合は `false` を返します。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentDocumentSelection%2A> プロパティ|モデル デザイナーで選択されている要素の読み取り専用のコレクションを取得します。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentSelection%2A> プロパティ|アクティブ ウィンドウで選択されている要素の読み取り専用のコレクションを取得します。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleDocumentSelection%2A> プロパティ|モデル デザイナーでの選択のプライマリ要素を取得します。|
    |<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleSelection%2A> プロパティ|アクティブ ウィンドウでの選択のプライマリ要素を取得します。|

2. <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet.CurrentDocView%2A> クラスの <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> プロパティを使用すると、 モデル デザイナー ウィンドウを表す <xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView> オブジェクトにアクセスでき、さらにモデル デザイナーで選択されている要素にもアクセスできます。

3. さらに、生成されたコードでは、ドメイン固有言語用のコマンド セット クラスでエクスプローラー ツール ウィンドウ プロパティとエクスプローラー選択プロパティが定義されています。

    - エクスプローラー ツール ウィンドウ プロパティからは、ドメイン固有言語用のエクスプローラー ツール ウィンドウ クラスのインスタンスが返されます。 エクスプローラー ツール ウィンドウ クラスは <xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow> クラスから派生し、ドメイン固有言語用のモデル エクスプローラーを表します。

    - `ExplorerSelection` プロパティからは、ドメイン固有言語用のモデル エクスプローラー ウィンドウで選択されている要素が返されます。

## <a name="determine-which-window-is-active"></a>アクティブなウィンドウを特定する

<xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> インターフェイスには、シェルの現在の選択状態にアクセスできるメンバーが定義されています。 ドメイン固有言語用のパッケージ クラスまたはコマンド セット クラスの基底クラスで定義されている `MonitorSelection` プロパティを使用して、それぞれのクラスから <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> オブジェクトを取得できます。 パッケージ クラスは <xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage> クラスから派生し、コマンド セット クラスは <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> クラスから派生しています。

### <a name="to-determine-from-a-command-handler-what-type-of-window-is-active"></a>アクティブになっているウィンドウの種類をコマンド ハンドラーから特定するには

1. <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> クラスの <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.MonitorSelection%2A> プロパティからは、シェルの現在の選択状態にアクセスできる <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> オブジェクトが返されます。

2. <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> インターフェイスの <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService.CurrentSelectionContainer%2A> プロパティを使用すると、アクティブな選択コンテナーを取得できます。これは、アクティブなウィンドウとは異なる場合があります。

3. アクティブなウィンドウの種類を特定するには、次のプロパティをドメイン固有言語用のコマンド セット クラスに追加します。

    ```csharp
    // using Microsoft.VisualStudio.Modeling.Shell;

    // Returns true if the model designer is the active selection container;
    // otherwise, false.
    protected bool IsDesignerActive
    {
        get
        {
            return (this.MonitorSelection.CurrentSelectionContainer
                is DiagramDocView);
        }
    }

    // Returns true if the model explorer is the active selection container;
    // otherwise, false.
    protected bool IsExplorerActive
    {
        get
        {
            return (this.MonitorSelection.CurrentSelectionContainer
                is ModelExplorerToolWindow);
        }
    }
    ```

## <a name="constrain-the-selection"></a>選択を制約する

選択規則を追加することにより、ユーザーがモデル内の要素を選択したときに選択される要素を制御できます。 たとえば、ユーザーが複数の要素を 1 つの単位として扱うことができるようにするには、選択規則を使用します。

### <a name="to-create-a-selection-rule"></a>選択規則を作成するには

1. DSL プロジェクトでカスタム コード ファイルを作成します

2. <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules> クラスから派生する選択規則クラスを定義します。

3. 選択条件を適用するには、選択規則クラスの <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules.GetCompliantSelection%2A> メソッドをオーバーライドします。

4. ClassDiagram クラスの部分クラス定義を、カスタム コード ファイルに追加します。

     `ClassDiagram` クラスは、<xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram> クラスから派生し、DSL プロジェクトの生成されたコード ファイル (Diagram.cs) で定義されています。

5. カスタム選択規則を返すように、`ClassDiagram` クラスの <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A> プロパティをオーバーライドします。

     <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A> プロパティの既定の実装では、選択を変更しない選択規則オブジェクトが取得されます。

### <a name="example"></a>例

次のコード ファイルでは、最初に選択されていた各ドメイン シェイプのすべてのインスタンスが含まれるように選択範囲を拡張する選択規則が作成されます。

```csharp
using System;
using System.Collections.Generic;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;

namespace CompanyName.ProductName.GroupingDsl
{
    public class CustomSelectionRules : DiagramSelectionRules
    {
        protected Diagram diagram;
        protected IElementDirectory elementDirectory;

        public CustomSelectionRules(Diagram diagram)
        {
            if (diagram == null) throw new ArgumentNullException();

            this.diagram = diagram;
            this.elementDirectory = diagram.Store.ElementDirectory;
        }

        /// <summary>Called by the design surface to allow selection filtering.
        /// </summary>
        /// <param name="currentSelection">[in] The current selection before any
        /// ShapeElements are added or removed.</param>
        /// <param name="proposedItemsToAdd">[in/out] The proposed DiagramItems to
        /// be added to the selection.</param>
        /// <param name="proposedItemsToRemove">[in/out] The proposed DiagramItems
        /// to be removed from the selection.</param>
        /// <param name="primaryItem">[in/out] The proposed DiagramItem to become
        /// the primary DiagramItem of the selection. A null value signifies that
        /// the last DiagramItem in the resultant selection should be assumed as
        /// the primary DiagramItem.</param>
        /// <returns>true if some or all of the selection was accepted; false if
        /// the entire selection proposal was rejected. If false, appropriate
        /// feedback will be given to the user to indicate that the selection was
        /// rejected.</returns>
        public override bool GetCompliantSelection(
            SelectedShapesCollection currentSelection,
            DiagramItemCollection proposedItemsToAdd,
            DiagramItemCollection proposedItemsToRemove,
            DiagramItem primaryItem)
        {
            if (currentSelection.Count == 0 && proposedItemsToAdd.Count == 0) return true;

            HashSet<DomainClassInfo> itemsToAdd = new HashSet<DomainClassInfo>();

            foreach (DiagramItem item in proposedItemsToAdd)
            {
                if (item.Shape != null)
                    itemsToAdd.Add(item.Shape.GetDomainClass());
            }
            proposedItemsToAdd.Clear();
            foreach (DomainClassInfo classInfo in itemsToAdd)
            {
                foreach (ModelElement element
                    in this.elementDirectory.FindElements(classInfo, false))
                {
                    if (element is ShapeElement)
                    {
                        proposedItemsToAdd.Add(
                            new DiagramItem((ShapeElement)element));
                    }
                }
            }

            return true;
        }
    }

    public partial class ClassDiagram
    {
        protected CustomSelectionRules customSelectionRules = null;

        protected bool multipleSelectionMode = true;

        public override DiagramSelectionRules SelectionRules
        {
            get
            {
                if (multipleSelectionMode)
                {
                    if (customSelectionRules == null)
                    {
                        customSelectionRules = new CustomSelectionRules(this);
                    }
                    return customSelectionRules;
                }
                else
                {
                    return base.SelectionRules;
                }
            }
        }
    }
}
```

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>
- <xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage>
- <xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView>
- <xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow>
- <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>
- <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules>
- <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>