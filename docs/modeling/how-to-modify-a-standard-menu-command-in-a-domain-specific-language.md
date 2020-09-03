---
title: DSL で標準メニューコマンドを変更する
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- .vsct files, adding commands to a domain-specific language
- Domain-Specific Language, adding custom commands
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a7236c074bda17023c989c744042db2de4046558
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85532497"
---
# <a name="how-to-modify-a-standard-menu-command-in-a-domain-specific-language"></a>方法: ドメイン固有言語における標準のメニュー コマンドを修正する

DSL で自動的に定義される標準コマンドのいくつかの動作を変更できます。 たとえば、重要な情報を除外するように **切り取り** を変更することができます。 そのためには、コマンド セット クラス内でメソッドをオーバーライドします。 これらのクラスは DslPackage プロジェクト内の CommandSet.cs ファイルで定義され、<xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> から派生します。

> [!NOTE]
> 独自のメニューコマンドを作成する場合は、「 [方法: ショートカットメニューにコマンドを追加](../modeling/how-to-add-a-command-to-the-shortcut-menu.md)する」を参照してください。

## <a name="what-commands-can-you-modify"></a>変更可能なコマンド

### <a name="to-discover-what-commands-you-can-modify"></a>変更可能なコマンドを見つけるには

1. `DslPackage` プロジェクトで、`GeneratedCode\CommandSet.cs` ファイルを開きます。 この C# ファイルは、の子会社としてソリューションエクスプローラーにあり `CommandSet.tt` ます。

2. このファイル内の名前の末尾が "" であるクラスを検索 `CommandSet` します。たとえば、「」を参照して `Language1CommandSet` `Language1ClipboardCommandSet` ください。

3. 各コマンド セット クラスで、"`override`" とその後に続けて空白文字を 1 つ入力します。 IntelliSense ではオーバーライド可能なメソッドの一覧が表示されます。 各コマンドには名前が "`ProcessOnStatus`" および "`ProcessOnMenu`" で始まるメソッドのペアが含まれます。

4. 変更するコマンドを含むコマンド セット クラスをメモします。

5. 編集内容を保存せずにファイルを閉じます。

    > [!NOTE]
    > 通常、生成されたファイルを編集できません。 次回ファイルが生成されたときに編集内容は失われます。

## <a name="extend-the-appropriate-command-set-class"></a>適切なコマンド セット クラスを拡張します。

コマンド セット クラスの部分宣言を含む新しいファイルを作成します。

### <a name="to-extend-the-command-set-class"></a>コマンド セット クラスを拡張するには

1. ソリューション エクスプローラーで、DslPackage プロジェクト内の GeneratedCode フォルダーを開き、CommandSet.tt の下で、生成されたファイル CommandSet.cs を開きます。 名前空間と、名前空間で定義されている最初のクラスの名前を書きとめます。 たとえば、次のように表示されることがあります。

     `namespace Company.Language1`

     `{ ...  internal partial class Language1CommandSet : ...`

2. **Dslpackage**で、**カスタムコード**という名前のフォルダーを作成します。 このフォルダーに、という名前の新しいクラスファイルを作成 `CommandSet.cs` します。

3. 新しいファイル内に、生成された部分クラスと同じ名前空間および名前を持つ部分宣言を記述します。 次に例を示します。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Design;
    namespace Company.Language1 /* Make sure this is correct */
    { internal partial class Language1CommandSet { ...
    ```

    > [!NOTE]
    > クラスファイルテンプレートを使用して新しいファイルを作成した場合は、名前空間とクラス名の両方を修正する必要があります。

## <a name="override-the-command-methods"></a>コマンド メソッドのオーバーライド

ほとんどのコマンドには、次のような2つのメソッドが関連付けられてい `ProcessOnStatus` ます。コマンドを表示して有効にする必要があるかどうかを判断します。 このメソッドはユーザーが図を右クリックするたびに呼び出され、すばやく実行し、何の変更も生じません。 `ProcessOnMenu`...は、ユーザーがコマンドをクリックしたときに呼び出され、コマンドの機能を実行する必要があります。 これらのメソッドの一方または両方をオーバーライドする場合があります。

### <a name="to-change-when-the-command-appears-on-a-menu"></a>メニュー上にコマンドが表示されるタイミングを変更するには

ProcessOnStatus をオーバーライドします...b. このメソッドは、パラメーター MenuCommand の Visible プロパティおよび Enabled プロパティを設定します。 通常、コマンドは this.CurrentSelection を見て、コマンドが選択された要素に適用されるかどうかを判断し、それらのプロパティを見て、コマンドが現在の状態で適用可能かどうかを判断します。

一般的なガイドとして、Visible プロパティは選択される要素により判断する必要があります。 Enabled プロパティは、コマンドがメニュー上に黒で表示されるかグレーで表示されるかを決め、現在の選択状態に依存します。

以下の例では、ユーザーが複数の図形を選択している場合、[削除] メニュー項目が無効になります。

> [!NOTE]
> このメソッドはコマンドがキーストロークにより使用可能かどうかに影響しません。 たとえば、[削除] メニュー項目を無効化しても、コマンドが Delete キーから呼び出されるのを妨げません。

```csharp
/// <summary>
/// Called when user right-clicks on the diagram or clicks the Edit menu.
/// </summary>
/// <param name="command">Set Visible and Enabled properties.</param>
protected override void ProcessOnStatusDeleteCommand (MenuCommand command)
{
  // Default settings from the base method.
  base.ProcessOnStatusDeleteCommand(command);
  if (this.CurrentSelection.Count > 1)
  {
    // If user has selected more than one item, Delete is greyed out.
    command.Enabled = false;
  }
}
```

最初に基本的なメソッドを呼び出し、関係のないケースおよび設定のすべてに対処することを推奨します。

ProcessOnStatus メソッドは、ストア内の要素の作成、削除、または更新を実行しません。

### <a name="to-change-the-behavior-of-the-command"></a>コマンドの動作を変更するには

ProcessOnMenu をオーバーライドします...b. 以下の例では、Delete キーを使用しても、ユーザーは一度に複数の要素を削除できません。

```csharp
/// <summary>
/// Called when user presses Delete key
/// or clicks the Delete command on a menu.
/// </summary>
protected override void ProcessOnMenuDeleteCommand()
{
  // Allow users to delete only one thing at a time.
  if (this.CurrentSelection.Count <= 1)
  {
    base.ProcessOnMenuDeleteCommand();
  }
}
```

要素またはリンクの作成、削除、または更新など、コードがストアに対して変更を加える場合、トランザクション内でそれを実行する必要があります。 詳細については、「 [モデル要素を作成および更新する方法](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)」を参照してください。

### <a name="write-the-code-of-the-methods"></a>メソッドのコードを記述する

次のコード片はこれらのメソッド内で頻繁に役立ちます。

- `this.CurrentSelection`. ユーザーが右クリックした図形は常にこの図形およびコネクタの一覧に含まれます。 ユーザーが図の空白部分をクリックした場合、このリストのメンバーは図のみになります。

- `this.IsDiagramSelected()` - `true` ユーザーが図の空白部分をクリックした場合。

- `this.IsCurrentDiagramEmpty()`

- `this.IsSingleSelection()` -ユーザーが複数の図形を選択しませんでした

- `this.SingleSelection` -ユーザーが右クリックした図形または図

- `shape.ModelElement as MyLanguageElement` -図形によって表されるモデル要素。

要素間の移動方法、およびオブジェクトとリンクの作成方法の詳細については、「 [プログラムコードでのモデルのナビゲーションと更新](../modeling/navigating-and-updating-a-model-in-program-code.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.ComponentModel.Design.MenuCommand>
- [ドメイン固有言語をカスタマイズするコードの記述](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [方法: ショートカット メニューにコマンドを追加する](../modeling/how-to-add-a-command-to-the-shortcut-menu.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML スキーマ リファレンス](../extensibility/vsct-xml-schema-reference.md)
- [VMSDK-回路図のサンプル。広範囲にわたる DSL のカスタマイズ](https://code.msdn.microsoft.com/Visualization-Modeling-SDK-763778e8)
