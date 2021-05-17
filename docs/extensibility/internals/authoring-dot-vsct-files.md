---
title: .vsct ファイルを記述する |Microsoft Docs
description: メニュー項目、ツール バー、その他の UI 要素を Visual Studio 統合開発環境 (IDE) に追加する .vsct ファイルを記述する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, manual authoring
ms.assetid: e9f715dc-12b7-439b-bdf3-f3dc75e62f1c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 73d16337daefdfe25425982a7fc7249c42f0fa1a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086340"
---
# <a name="author-vsct-files"></a>.vsct ファイルを記述する
このドキュメントでは、メニュー項目、ツール バー、その他のユーザー インターフェイス (UI) 要素を Visual Studio 統合開発環境 (IDE) に追加するために、 *.vsct* ファイルを記述する方法について説明します。 これらの手順は、まだ *.vsct* ファイルがない Visual Studio パッケージ (VSPackage) に UI 要素を追加する場合に使用します。

 新しいプロジェクトの場合は、Visual Studio パッケージ テンプレートを使用することをお勧めします。このテンプレートでは、選択内容に応じて、メニュー コマンド、ツール ウィンドウ、またはカスタム エディターに必要な要素を既に持つ *.vsct* ファイルが生成されるためです。 この *.vsct* ファイルを変更して、VSPackage の要件を満たすことができます。 *.vsct* ファイルを変更する方法の詳細については、「[メニューとコマンドを拡張する](../../extensibility/extending-menus-and-commands.md)」の例を参照してください。

## <a name="author-the-file"></a>ファイルを記述する
 *.vsct* ファイルを記述するためのフェーズは次のとおりです。ファイルとリソースの構造を作成し、UI 要素を宣言して、UI 要素を IDE に配置し、特殊な動作を追加します。

### <a name="file-structure"></a>ファイル構造
 *.vsct* ファイルの基本構造は [CommandTable](../../extensibility/commandtable-element.md) ルート要素であり、[Commands](../../extensibility/commands-element.md) 要素と [Symbols](../../extensibility/symbols-element.md) 要素が含まれています。

#### <a name="to-create-the-file-structure"></a>ファイル構造を作成するには

1. [「方法: vsct ファイルを作成する](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)」の手順に従って、 *.vsct* ファイルをプロジェクトに追加します。

2. 次の例に示すように、必要な名前空間を `CommandTable` 要素に追加します。

    ```xml
    <CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable"
        xmlns:xs="http://www.w3.org/2001/XMLSchema">

    ```

3. `CommandTable` 要素に、すべてのカスタム メニュー、ツール バー、コマンド グループ、コマンドをホストする `Commands` 要素を追加します。 カスタム UI 要素を読み込むことができるようにするには、`Commands` 要素の `Package` 属性にパッケージの名前が設定されている必要があります。

     `Commands` 要素の後に `Symbols` 要素を追加して、パッケージの GUID、および UI 要素の名前とコマンド ID を定義します。

### <a name="include-visual-studio-resources"></a>Visual Studio リソースを含める
 Visual Studio のコマンドが定義されているファイルと、IDE に UI 要素を配置するために必要なメニューにアクセスするには、[Extern](../../extensibility/extern-element.md) 要素を使用します。 パッケージの外部で定義されているコマンドを使用する場合は、[UsedCommands](../../extensibility/usedcommands-element.md) 要素を使用して Visual Studio に通知します。

#### <a name="to-include-visual-studio-resources"></a>Visual Studio リソースを含めるには

1. `CommandTable` 要素の先頭に、参照する外部ファイルごとに 1 つの `Extern` 要素を追加し、`href` 属性をファイルの名前に設定します。 次のヘッダー ファイルを参照すると、Visual Studio リソースにアクセスできます。

   - *Stdidcmd.h*: Visual Studio によって公開されるすべてのコマンドの ID を定義します。

   - *Vsshlids. h*: Visual Studio メニューのコマンド ID が含まれています。

2. Visual Studio または他のパッケージで定義されているコマンドをパッケージで呼び出す場合は、`Commands` 要素の後に `UsedCommands` 要素を追加します。 パッケージの一部ではない、呼び出すコマンドごとに [UsedCommand](../../extensibility/usedcommand-element.md) 要素をこの要素に設定します。 `UsedCommand` 要素の `guid` および `id` 属性に、呼び出すコマンドの GUID と ID の値を設定します。

   Visual Studio コマンドの GUID と ID を検索する方法の詳細については、「[Visual studio コマンドの GUID と ID](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)」を参照してください。 他のパッケージからコマンドを呼び出すには、そのパッケージの *.vsct* ファイルで定義されているコマンドの GUID と ID を使用します。

### <a name="declare-ui-elements"></a>UI 要素を宣言する
 新しい UI 要素はすべて *.vsct* ファイルの `Symbols` セクションで宣言します。

#### <a name="to-declare-ui-elements"></a>UI 要素を宣言するには

1. `Symbols` 要素に 3 つの [GuidSymbol](../../extensibility/guidsymbol-element.md) 要素を追加します。 各 `GuidSymbol` 要素には、`name` 属性と `value` 属性があります。 要素の目的が反映されるように `name` 属性を設定します。 `value` 属性は GUID を受け取ります。 (GUID を生成するには、 **[ツール]** メニューで **[GUID の作成]** を選択し、 **[登録形式]** を選択します。)

     最初の `GuidSymbol` 要素はパッケージを表し、通常は子を持ちません。 2 番目の `GuidSymbol` 要素はコマンド セットを表し、メニュー、グループ、コマンドを定義するすべてのシンボルが含まれています。 3 番目の `GuidSymbol` 要素はイメージ ストアを表し、コマンドのすべてのアイコンのシンボルが含まれています。 アイコンを使用するコマンドがない場合は、3 番目の `GuidSymbol` 要素を省略できます。

2. コマンド セットを表す `GuidSymbol` 要素に、1 つまたは複数の [IDSymbol](../../extensibility/idsymbol-element.md) 要素を追加します。 これらは UI に追加するメニュー、ツール バー、グループ、またはコマンドをそれぞれ表します。

     各 `IDSymbol` 要素で、対応するメニュー、グループ、またはコマンドを参照するために使用される名前を `name` 属性に設定し、そのコマンド ID を表す 16 進数を `value` 要素に設定します。 同じ親を持つ 2 つの `IDSymbol` 要素を同じ値にすることはできません。

3. UI 要素のいずれかにアイコンが必要な場合は、イメージ ストアを表す `GuidSymbol` 要素に各アイコンの `IDSymbol` 要素を追加します。

### <a name="put-ui-elements-in-the-ide"></a>UI 要素を IDE に配置する
 [Menus](../../extensibility/menus-element.md)、[Groups](../../extensibility/groups-element.md)、[Buttons](../../extensibility/buttons-element.md) の各要素には、パッケージで定義されているすべてのメニュー、グループ、コマンドの定義が含まれています。 これらのメニュー、グループ、コマンドを IDE に配置するには、UI 要素の定義の一部である [Parent](../../extensibility/parent-element.md) 要素を使用するか、別の場所で定義された [CommandPlacement](../../extensibility/commandplacement-element.md) 要素を使用します。

 `Menu`、`Group`、`Button` の各要素には、`guid` 属性と `id` 属性があります。 コマンド セットを表す `GuidSymbol` 要素の名前と一致するように常に `guid` 属性を設定し、`Symbols` セクション内のメニュー、グループ、またはコマンドを表す `IDSymbol` 要素の名前を `id` 属性に設定します。

#### <a name="to-define-ui-elements"></a>UI 要素を定義するには

1. 新しいメニュー、サブメニュー、ショートカット メニュー、またはツール バーを定義する場合は、`Commands` 要素に `Menus` 要素を追加します。 次に、作成するメニューごとに、[Menu](../../extensibility/menu-element.md) 要素を `Menus` 要素に追加します。

    `Menu` 要素の `guid` および `id` 属性を設定し、目的のメニューの種類を `type` 属性に設定します。 また、`priority` 属性を設定して、親グループ内のメニューの相対位置を設定することもできます。

   > [!NOTE]
   > `priority` 属性は、ツール バーとコンテキスト メニューには適用されません。

2. Visual Studio IDE のすべてのコマンドは、メニューとツール バーの直接の子であるコマンド グループでホストされている必要があります。 新しいメニューやツール バーを IDE に追加する場合は、新しいコマンド グループが含まれている必要があります。 コマンドを視覚的にグループ化できるように、既存のメニューやツール バーにコマンド グループを追加することもできます。

    新しいコマンド グループを追加する場合は、最初に `Groups` 要素を作成してから、各コマンド グループの [Group](../../extensibility/group-element.md) 要素を追加する必要があります。

    各 `Group` 要素の `guid` および `id` 属性を設定してから、`priority` 属性を設定して、親メニューのグループの相対位置を設定します。 詳細については、「[再利用可能なボタンのグループを作成する](../../extensibility/creating-reusable-groups-of-buttons.md)」を参照してください。

3. IDE に新しいコマンドを追加する場合は、`Commands` 要素に `Buttons` 要素を追加します。 次に、各コマンドについて、`Buttons` 要素に [Button](../../extensibility/button-element.md) 要素を追加します。

   1. 各 `Button` 要素の `guid` および `id` 属性を設定し、目的のボタンの種類を `type` 属性に設定します。 また、`priority` 属性を設定して、親グループ内のコマンドの相対位置を設定することもできます。

       > [!NOTE]
       > ツール バーの標準のメニュー コマンドとボタンには `type="button"` 使用します。

   2. `Button` 要素に、[ButtonText](../../extensibility/buttontext-element.md) 要素と [CommandName](../../extensibility/commandname-element.md) 要素を含む [Strings](../../extensibility/strings-element.md) 要素を追加します。 `ButtonText` 要素によって、メニュー項目のテキスト ラベル、またはツール バーのボタンのツール ヒントが提供されます。 `CommandName` 要素によって、コマンド ウェルで使用されるコマンドの名前が提供されます。

   3. コマンドにアイコンがある場合は、`Button` 要素に [Icon](../../extensibility/icon-element.md) 要素を作成し、その `guid` および `id` 属性にアイコンの `Bitmap` 要素を設定します。

       > [!NOTE]
       > ツール バーのボタンにはアイコンが必要です。

   詳細については、[MenuCommands と OleMenuCommands](/previous-versions/visualstudio/visual-studio-2015/misc/menucommands-vs-olemenucommands?preserve-view=true&view=vs-2015)に関するページを参照してください。

4. いずれかのコマンドでアイコンが必要な場合は、`Commands` 要素に [Bitmaps](../../extensibility/bitmaps-element.md) 要素を追加します。 次に、各アイコンについて、`Bitmaps` 要素に [Bitmap](../../extensibility/bitmap-element.md) 要素を追加します。 これはビットマップ リソースの場所を指定する場所です。 詳細については、「[メニュー コマンドにアイコンを追加する](../../extensibility/adding-icons-to-menu-commands.md)」を参照してください。

   ほとんどのメニュー、グループ、コマンドは、ペアレンティング構造体に依存して正しく配置することができます。 非常に大きなコマンド セットの場合、またはメニュー、グループ、またはコマンドを複数の場所に表示する必要がある場合は、コマンドの配置を指定することをお勧めします。

#### <a name="to-rely-on-parenting-to-place-ui-elements-in-the-ide"></a>ペアレンティングに依存して IDE に UI 要素を配置するには

1. 一般的なペアレンティングの場合は、パッケージで定義されている `Menu`、`Group`、`Command` の各要素に `Parent` 要素を作成します。

    `Parent` 要素のターゲットは、メニュー、グループ、またはコマンドを含むメニューまたはグループです。

   1. コマンド セットを定義する `GuidSymbol` 要素の名前を `guid` 属性に設定します。 ターゲット要素がパッケージに含まれていない場合は、対応する *.vsct* ファイルで定義されているそのコマンド セットの GUID を使用します。

   2. ターゲットのメニューまたはグループの `id` 属性と一致するように `id` 属性を設定します。 Visual Studio によって公開されているメニューとグループの一覧については、「[Visual Studio メニューの GUID と ID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)」または「[Visual Studio ツール バーの GUID と ID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)」を参照してください。

   IDE に配置する UI 要素が多数ある場合、または複数の場所に表示される要素がある場合は、次の手順に示すように、それらの配置を [CommandPlacements](../../extensibility/commandplacements-element.md) 要素に定義します。

#### <a name="to-use-command-placement-to-place-ui-elements-in-the-ide"></a>コマンドの配置を使用して IDE に UI 要素を配置するには

1. `Commands` 要素の後に、`CommandPlacements` 要素を追加します。

2. `CommandPlacements` 要素に、配置するメニュー、グループ、またはコマンドごとに `CommandPlacement` 要素を追加します。

    各 `CommandPlacement` 要素または `Parent` 要素では、1 つの IDE の場所に 1 つのメニュー、グループ、またはコマンドが配置されます。 UI 要素で持つことができる親は 1 つのみですが、複数のコマンドの配置を持つことができます。 UI 要素を複数の場所に配置するには、場所ごとに `CommandPlacement` 要素を追加します。

3. `Parent` 要素の場合と同様に、各 `CommandPlacement` 要素の `guid` および `id` 属性に、ホストするメニューまたはグループを設定します。 また、`priority` 属性を設定して、UI 要素の相対位置を設定することもできます。

   ペアレンティングによる配置とコマンドの配置は組み合わせることができます。 ただし、非常に大きなコマンド セットの場合は、コマンドの配置のみを使用することをお勧めします。

### <a name="add-specialized-behaviors"></a>特殊な動作を追加する
 メニューやコマンドの動作を変更する (外観や表示の変更など) には、[CommandFlag](../../extensibility/command-flag-element.md) 要素を使用します。 また、[VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) 要素を使用してコマンドがどのようなときに表示されるかに影響を与えたり、[KeyBindings](../../extensibility/keybindings-element.md) 要素を使用してキーボード ショートカットを追加したりすることもできます。 特定の種類のメニューとコマンドには、既に特殊な動作が組み込まれています。

#### <a name="to-add-specialized-behaviors"></a>特殊な動作を追加するには

1. 特定の UI コンテキスト (ソリューションが読み込まれたときなど) でのみ UI 要素が表示されるようにするには、可視性の制約を使用します。

   1. `Commands` 要素の後に、`VisibilityConstraints` 要素を追加します。

   2. 制約する各 UI 項目に、[VisibilityItem](../../extensibility/visibilityitem-element.md) 要素を追加します。

   3. 各 `VisibilityItem` 要素で、メニュー、グループ、またはコマンドに `guid` および `id` 属性を設定し、<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> クラスで定義されているように、目的の UI コンテキストを `context` 属性に設定します。

2. コード内の UI 項目の可視性または可用性を設定するには、次のコマンド フラグのいずれか (または複数のフラグ) を使用します。

   - `DefaultDisabled`

   - `DefaultInvisible`

   - `DynamicItemStart`

   - `DynamicVisibility`

   - `NoShowOnMenuController`

   - `NotInTBList`

   詳細については、「[CommandFlag](../../extensibility/command-flag-element.md) 要素」を参照してください。

3. 要素の表示方法を変更したり、要素の外観を動的に変更したりするには、次のコマンド フラグのいずれか (または複数のフラグ) を使用します。

   - `AlwaysCreate`

   - `CommandWellOnly`

   - `DefaultDocked`

   - `DontCache`

   - `DynamicItemStart`

   - `FixMenuController`

   - `IconAndText`

   - `Pict`

   - `StretchHorizontally`

   - `TextMenuUseButton`

   - `TextChanges`

   - `TextOnly`

   詳細については、「[CommandFlag](../../extensibility/command-flag-element.md) 要素」を参照してください。

4. コマンドを受け取ったときの要素の反応を変更するには、次のコマンド フラグのいずれか (または複数のフラグ) を使用します。

   - `AllowParams`

   - `CaseSensitive`

   - `CommandWellOnly`

   - `FilterKeys`

   - `NoAutoComplete`

   - `NoButtonCustomize`

   - `NoKeyCustomize`

   - `NoToolbarClose`

   - `PostExec`

   - `RouteToDocs`

   - `TextIsAnchorCommand`

   詳細については、「[CommandFlag](../../extensibility/command-flag-element.md) 要素」を参照してください。

5. メニュー依存のキーボード ショートカットをメニューまたはメニュー項目にアタッチするには、メニューまたはメニュー項目の `ButtonText` 要素にアンパサンド文字 (&) を追加します。 アンパサンドの後に続く文字は、親メニューが開いているときにアクティブなキーボード ショートカットです。

6. メニューに依存しないキーボード ショートカットをコマンドにアタッチするには、[KeyBindings](../../extensibility/keybindings-element.md) 要素を使用します。 詳細については、「[KeyBinding](../../extensibility/keybinding-element.md) 要素」を参照してください。

7. メニュー テキストをローカライズするには、`LocCanonicalName` 要素を使用します。 詳細については、「[Strings](../../extensibility/strings-element.md) 要素」を参照してください。

   いくつかのメニューとボタンの種類には、特殊な動作が含まれています。 次の一覧では、いくつかの特殊なメニューとボタンの種類について説明しています。 その他の種類については、[Menu](../../extensibility/menu-element.md)、[Button](../../extensibility/button-element.md)、[Combo](../../extensibility/combo-element.md) 要素の `types` 属性の説明を参照してください。

   - コンボ ボックス: コンボ ボックスは、ツール バーで使用できるドロップダウン リストです。 コンボ ボックスを UI に追加するには、`Commands` 要素に [Combos](../../extensibility/combos-element.md) 要素を作成します。 次に、追加する各コンボ ボックスの `Combo` 要素を `Combos` 要素に追加します。 `Combo` 要素には、`Button` 要素と同じ属性と子があり、`DefaultWidth` および `idCommandList` 属性もあります。 `DefaultWidth` 属性にはピクセル単位で幅を設定し、`idCommandList` 属性ではコンボ ボックスの事前設定に使用されるコマンド ID を指します。

   - メニュー コントローラー: メニュー コントローラーは、その横に矢印があるボタンです。 矢印をクリックすると、一覧が表示されます。 メニュー コントローラーを UI に追加するには、必要な動作に応じて、`Menu` 要素を作成し、その `type` 属性に `MenuController` または `MenuControllerLatched` を設定します。 メニュー コントローラーを事前設定するには、`Group` 要素の親として設定します。 メニュー コントローラーでは、そのグループのすべての子がドロップダウン リストに表示されます。

## <a name="see-also"></a>関連項目
- [メニューとコマンドを拡張する](../../extensibility/extending-menus-and-commands.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML スキーマ リファレンス](../../extensibility/vsct-xml-schema-reference.md)