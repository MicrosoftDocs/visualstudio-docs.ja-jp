---
title: VSPackage でユーザー インターフェイス要素を追加する方法 | Microsoft Docs
description: VSPackage によって、メニュー、ツール バー、ツール ウィンドウなどのユーザー インターフェイス (UI) 要素が Visual Studio に追加される仕組みについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, adding elements
- UI element design [Visual Studio SDK], VSPackages
- VSPackages, contributing UI elements
ms.assetid: abc5d9d9-b267-48a1-92ad-75fbf2f4c1b9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f1d01c2ed91a5f4aad55c196dfb2e689aeea288a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086041"
---
# <a name="how-vspackages-add-user-interface-elements"></a>VSPackage でユーザー インターフェイス要素を追加する方法
VSPackage では、 *.vsct* ファイルを使用して、ユーザー インターフェイス (UI) 要素 (メニュー、ツール バー、ツール ウィンドウなど) を Visual Studio に追加できます。

UI 要素のデザイン ガイドラインについては、「[Visual Studio ユーザー エクスペリエンス ガイドライン](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)」を参照してください。

## <a name="the-visual-studio-command-table-architecture"></a>Visual Studio コマンド テーブルのアーキテクチャ
既に説明したように、コマンド テーブルのアーキテクチャでは、前述のアーキテクチャの原則がサポートされています。 コマンド テーブルのアーキテクチャの抽象化、データ構造、ツールの背後にある原則は次のとおりです。

- 3 つの基本的な項目の種類があります (メニュー、コマンド、グループ)。 メニューは、メニュー、サブメニュー、ツール バー、またはツール ウィンドウとして UI に表示できます。 コマンドは、ユーザーが IDE で実行できるプロシージャであり、メニュー項目、ボタン、リスト ボックス、またはその他のコントロールとして表示できます。 グループは、メニューとコマンドの両方のコンテナーです。

- 各項目は、項目、他の項目に対する相対的な優先度、およびその動作を変更するフラグが記述された定義によって指定されます。

- 各項目には、その項目の親について記述する配置があります。 項目は複数の親を持つことができるため、UI 内の複数の場所に表示できます。

すべてのコマンドは、そのグループ内の唯一の子であっても、親としてグループを持つ必要があります。 すべての標準メニューにも親グループが必要です。 ツール バーとツール ウィンドウは、それ自体の親として機能します。 グループは、Visual Studio のメインのメニュー バー、任意のメニュー、ツール バー、またはツール ウィンドウを親としてを持つことができます。

### <a name="how-items-are-defined"></a>項目の定義方法
*.vsct* ファイルは XML で書式設定されます。 パッケージの UI 要素を定義し、それらの要素が IDE に表示される場所を決定します。 パッケージ内のすべてのメニュー、グループ、またはコマンドには、最初に `Symbols` セクションで GUID と ID が割り当てられます。 *.vsct* ファイルの残りの部分では、各メニュー、コマンド、グループが GUID と ID の組み合わせによって識別されます。 次の例は、テンプレートで **メニュー コマンド** が選択されたときに Visual Studio パッケージ テンプレートによって生成される一般的な `Symbols` セクションを示しています。

```xml
<Symbols>
  <!-- This is the package guid. -->
  <GuidSymbol name="guidMenuTextPkg" value="{b1253bc6-d266-402b-89e7-5e3d3b22c746}" />

  <!-- This is the guid used to group the menu commands together -->
  <GuidSymbol name="guidMenuTextCmdSet" value="{a633d4e4-6c65-4436-a138-1abeba7c9a69}">
    <IDSymbol name="MyMenuGroup" value="0x1020" />
    <IDSymbol name="cmdidMyCommand" value="0x0100" />
  </GuidSymbol>

  <GuidSymbol name="guidImages" value="{53323d9a-972d-4671-bb5b-9e418480922f}">
    <IDSymbol name="bmpPic1" value="1" />
    <IDSymbol name="bmpPic2" value="2" />
    <IDSymbol name="bmpPicSearch" value="3" />
    <IDSymbol name="bmpPicX" value="4" />
    <IDSymbol name="bmpPicArrows" value="5" />
  </GuidSymbol>
</Symbols>
```

`Symbols` セクションの最上位レベルの要素は、[GuidSymbol 要素](../../extensibility/guidsymbol-element.md)です。 `GuidSymbol` 要素では、パッケージとそのコンポーネント パーツを識別するために IDE によって使用される GUID に名前がマップされます。

> [!NOTE]
> GUID は、Visual Studio パッケージ テンプレートによって自動的に生成されます。 **[ツール]** メニューで **[GUID の作成]** をクリックして、一意の GUID を生成することもできます。

最初の `GuidSymbol` 要素 (`guid<PackageName>Pkg`) は、パッケージ自体の GUID です。 これは、パッケージを読み込むために Visual Studio によって使用される GUID です。 通常、子要素はありません。

慣例により、メニューとコマンドは 2 番目の `GuidSymbol` 要素 (`guid<PackageName>CmdSet`) の下にグループ化され、ビットマップは 3 番目の `GuidSymbol` 要素 (`guidImages`) の下にグループ化されます。 この慣例に従う必要はありませんが、各メニュー、グループ、コマンド、ビットマップは、`GuidSymbol` 要素の子である必要があります。

パッケージ コマンド セットを表す 2 番目の `GuidSymbol` 要素には、複数の `IDSymbol` 要素があります。 各 [IDSymbol 要素](../../extensibility/idsymbol-element.md) では、名前が数値にマップされ、コマンド セットの一部であるメニュー、グループ、またはコマンドを表すことができます。 3 番目の `GuidSymbol` 要素の `IDSymbol` 要素は、コマンドのアイコンとして使用できるビットマップを表します。 GUID と ID のペアはアプリケーション内で一意である必要があるため、同じ `GuidSymbol` 要素の 2 つの子が同じ値を持つことはできません。

### <a name="menus-groups-and-commands"></a>メニュー、グループ、コマンド
メニュー、グループ、またはコマンドに GUID と ID がある場合は、IDE に追加できます。 すべての UI 要素には、次のものが必要です。

- UI 要素が定義されている `GuidSymbol` 要素の名前と一致する `guid` 属性。

- 関連付けられている `IDSymbol` 要素の名前と一致する `id` 属性。

`guid` および `id` 属性の組み合わせによって、UI 要素の "*シグネチャ*" が構成されます。

- 親メニューまたはグループ内の UI 要素の配置を決定する `priority` 属性。

- 親メニューまたはグループのシグネチャを指定する `guid` および `id` 属性を持つ[親要素](../../extensibility/parent-element.md)。

#### <a name="menus"></a>メニュー
各メニューは、`Menus` セクションに [Menu 要素](../../extensibility/menu-element.md) として定義されます。 メニューには `guid`、`id`、`priority` の各属性、`Parent` 要素、および次の追加の属性と子が必要です。

- メニューの一種としてメニューを IDE に表示するか、ツール バーとして表示するかを指定する `type` 属性。

- IDE のメニューのタイトルを指定する [ButtonText 要素](../../extensibility/buttontext-element.md)を含む [Strings 要素](../../extensibility/strings-element.md)と、 **[コマンド]** ウィンドウでメニューにアクセスするために使用される名前を指定する [CommandName 要素](../../extensibility/commandname-element.md)。

- オプションのフラグ。 IDE での外観や動作を変更するために、[CommandFlag 要素](../../extensibility/command-flag-element.md)がメニュー定義に指定されることがあります。

すべての `Menu` 要素は、ツール バーなどのドッキング可能な要素でない限り、親としてグループを持つ必要があります。 ドッキング可能なメニューは、それ自体の親です。 メニューと `type` 属性の値の詳細については、「[Menu 要素](../../extensibility/menu-element.md)」のドキュメントを参照してください。

次の例は、Visual Studio のメニュー バーの **[ツール]** メニューの横に表示されるメニューを示しています。

```xml
<Menu guid="guidTopLevelMenuCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
  <Parent guid="guidSHLMainMenu" id="IDG_VS_MM_TOOLSADDINS" />
  <Strings>
    <ButtonText>TestMenu</ButtonText>
    <CommandName>TestMenu</CommandName>
  </Strings>
</Menu>
```

#### <a name="groups"></a>グループ
グループは、 *.vsct* ファイルの `Groups` セクションで定義される項目です。 グループはただのコンテナーです。 IDE でメニュー上の分割線としてのみ表示されます。 このため、[Group 要素](../../extensibility/group-element.md) は、そのシグネチャ、優先度、親によってのみ定義されます。

グループは、メニュー、別のグループ、またはそれ自体を親として持つことができます。 ただし、通常、親はメニューまたはツール バーです。 前の例のメニューは `IDG_VS_MM_TOOLSADDINS` グループの子であり、そのグループは Visual Studio のメニュー バーの子です。 次の例のグループは、前の例のメニューの子です。

```xml
<Group guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" priority="0x0600">
  <Parent guid="guidTopLevelMenuCmdSet" id="TopLevelMenu"/>
</Group>
```

このグループはメニューの一部であるため、通常はコマンドを含んでいます。 ただし、他のメニューを含めることもできます。 次の例は、サブメニューを定義する方法を示しています。

```xml
<Menu guid="guidTopLevelMenuCmdSet" id="SubMenu" priority="0x0100" type="Menu">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup"/>
  <Strings>
    <ButtonText>Sub Menu</ButtonText>
    <CommandName>Sub Menu</CommandName>
  </Strings>
</Menu>
```

#### <a name="commands"></a>コマンド
IDE に提供されるコマンドは、[Button 要素](../../extensibility/button-element.md)または [Combo 要素](../../extensibility/combo-element.md)のいずれかとして定義されます。 メニューまたはツール バーに表示するには、コマンドの親がグループである必要があります。

##### <a name="buttons"></a>ボタン
ボタンは `Buttons` セクションに定義します。 ユーザーが 1 つのコマンドを実行するためにクリックするメニュー項目、ボタン、またはその他の要素は、ボタンと見なされます。 一部のボタンの種類には、リスト機能を含めることもできます。 ボタンには、メニューと同じ必須属性とオプション属性があります。また、IDE でボタンを表すビットマップの GUID と ID を指定する [Icon 要素](../../extensibility/icon-element.md) を持つこともできます。 ボタンとその属性の詳細については、「[Buttons 要素](../../extensibility/buttons-element.md)」のドキュメントを参照してください。

次の例のボタンは、前の例のグループの子であり、そのグループの親メニューのメニュー項目として IDE に表示されます。

```xml
<Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <Strings>
    <CommandName>cmdidTestCommand</CommandName>
    <ButtonText>Test Command</ButtonText>
  </Strings>
</Button>
```

##### <a name="combos"></a>コンボ
コンボは `Combos` セクションに定義します。 各 `Combo` 要素は、IDE のドロップダウン リスト ボックスを表します。 リスト ボックスは、コンボの `type` 属性の値に応じて、ユーザーが書き込みできるようにするか、書き込み不可にすることができます。 コンボは、ボタンと同じ要素と動作を持ち、次の追加の属性を持つこともできます。

- ピクセル幅を指定する `defaultWidth` 属性。

- リスト ボックスに表示される項目を含むリストを指定する `idCommandList` 属性。 コマンド リストは、コンボが含まれているのと同じ `GuidSymbol` ノードで宣言される必要があります。

次の例では、コンボ要素を定義しています。

```xml
<Combos>
  <Combo guid="guidFirstToolWinCmdSet"
         id="cmdidWindowsMediaFilename"
         priority="0x0100" type="DynamicCombo"
         idCommandList="cmdidWindowsMediaFilenameGetList"
         defaultWidth="130">
    <Parent guid="guidFirstToolWinCmdSet"
            id="ToolbarGroupID" />
    <CommandFlag>IconAndText</CommandFlag>
    <CommandFlag>CommandWellOnly</CommandFlag>
    <CommandFlag>StretchHorizontally</CommandFlag>
    <Strings>
      <CommandName>Filename</CommandName>
      <ButtonText>Enter a Filename</ButtonText>
    </Strings>
  </Combo>
</Combos>
```

##### <a name="bitmaps"></a>ビットマップ
アイコンと共に表示されるコマンドには、その GUID と ID を使用してビットマップを参照する `Icon` 要素が含まれている必要があります。 各ビットマップは、`Bitmaps` セクションに [Bitmap 要素](../../extensibility/bitmap-element.md)として定義します。 `Bitmap` の定義に必要な属性は、ソース ファイルを指す `guid` と `href` のみです。 ソース ファイルがリソース ストリップの場合は、ストリップの使用可能なイメージをリストするために **usedList** 属性も必要です。 詳細については、「[Bitmap 要素](../../extensibility/bitmap-element.md)」のドキュメントを参照してください。

### <a name="parenting"></a>ペアレンティング
次の規則によって、ある項目が別の項目の親となる仕組みが制御されます。

|要素|コマンド テーブルのこのセクションで定義されるもの|含まれているもの (親として、または `CommandPlacements` セクション内の配置によって、またはその両方)|含めることができるもの (親として参照されます)|
|-------------| - | - | - |
|Group|[Groups 要素](../../extensibility/groups-element.md)、IDE、他の VSPackage|メニュー、グループ、項目自体|メニュー、グループ、コマンド|
|メニュー|[Menus 要素](../../extensibility/menus-element.md)、IDE、他の VSPackage|1 から *n* 個のグループ|0 から *n* 個のグループ|
|ツール バー|[Menus 要素](../../extensibility/menus-element.md)、IDE、他の VSPackage|項目自体|0 から *n* 個のグループ|
|メニュー項目|[Buttons 要素](../../extensibility/buttons-element.md)、IDE、他の VSPackage|1 から *n* 個のグループ、項目自体|0 から *n* 個のグループ|
|ボタン|[Buttons 要素](../../extensibility/buttons-element.md)、IDE、他の VSPackage|1 から *n* 個のグループ、項目自体||
|複合|[Combos 要素](../../extensibility/combos-element.md)、IDE、他の VSPackage|1 から *n* 個のグループ、項目自体||

### <a name="menu-command-and-group-placement"></a>メニュー、コマンド、グループの配置
メニュー、グループ、またはコマンドは、IDE 内の複数の場所に表示できます。 複数の場所に項目を表示するには、その項目を [CommandPlacement 要素](../../extensibility/commandplacement-element.md)として `CommandPlacements` セクションに追加する必要があります。 任意のメニュー、グループ、またはコマンドをコマンドの配置として追加できます。 ただし、ツール バーは複数の状況依存の場所に表示できないため、この方法で配置することはできません。

コマンドの配置には、`guid`、`id`、`priority` 属性があります。 GUID と ID は、配置される項目の GUID と ID と一致している必要があります。 `priority` 属性では、他の項目に関連した項目の配置が制御されます。 IDE で同じ優先度を持つ複数の項目がマージされた場合、パッケージがビルドされるたびにパッケージ リソースが同じ順序で読み込まれることは保証されないため、配置が未定義になります。

メニューまたはグループが複数の場所に表示される場合は、そのメニューまたはグループのすべての子が各インスタンスに表示されます。

## <a name="command-visibility-and-context"></a>コマンドの可視性とコンテキスト
複数の VSPackages がインストールされている場合、メニュー、メニュー項目、ツール バーが多数あると、IDE が煩雑になることがあります。 この問題を回避するには、"*可視性の制約*" とコマンド フラグを使用して、個々の UI 要素の可視性を制御できます。

### <a name="visibility-constraints"></a>可視性の制約
可視性の制約は、`VisibilityConstraints` セクションに [VisibilityItem 要素](../../extensibility/visibilityitem-element.md) として設定します。 可視性の制約では、ターゲット項目が表示される特定の UI コンテキストを定義します。 このセクションに含まれているメニューまたはコマンドは、定義されているコンテキストのいずれかがアクティブな場合にのみ表示されます。 メニューまたはコマンドがこのセクションで参照されていない場合は、常に既定で表示されます。 このセクションはグループには適用されません。

`VisibilityItem` 要素には、ターゲットの UI 要素の `guid` および `id` と `context` の 3 つの属性がある必要があります。 `context` 属性では、ターゲット項目がどのようなときに表示されるかを指定し、有効な UI コンテキストをその値として受け取ります。 Visual Studio の UI コンテキスト定数は、<xref:Microsoft.VisualStudio.VSConstants> クラスのメンバーです。 すべての `VisibilityItem` 要素は、1 つのコンテキスト値のみを受け取ることができます。 2 つ目のコンテキストを適用するには、次の例に示すように、同じ項目を指す 2 番目の `VisibilityItem` 要素を作成します。

```xml
<VisibilityConstraints>
  <VisibilityItem guid="guidSolutionToolbarCmdSet"
        id="cmdidTestCmd"
        context="UICONTEXT_SolutionHasSingleProject" />
  <VisibilityItem guid="guidSolutionToolbarCmdSet"
        id="cmdidTestCmd"
        context="UICONTEXT_SolutionHasMultipleProjects" />
</VisibilityConstraints>
```

### <a name="command-flags"></a>コマンド フラグ
次のコマンド フラグを使用すると、それらが適用されるメニューとコマンドの可視性に影響を与えることができます。

`AlwaysCreate` グループまたはボタンがない場合でもメニューが作成されます。

有効な対象: `Menu`

`CommandWellOnly` コマンドが最上位レベルのメニューに表示されず、追加のシェル カスタマイズ (キーにバインドする場合など) に使用できるようにする場合は、このフラグを適用します。 VSPackage のインストール後、ユーザーは **[オプション]** ダイアログ ボックスを開き、 **[キーボード環境]** カテゴリの下にあるコマンドの配置を編集することで、これらのコマンドをカスタマイズできます。 ショートカット メニュー、ツール バー、メニュー コントローラー、またはサブメニューの配置には影響しません。

有効な対象: `Button`、`Combo`

`DefaultDisabled` 既定では、コマンドを実装する VSPackage が読み込まれていない場合、または QueryStatus メソッドが呼び出されていない場合、コマンドは無効になります。

有効な対象: `Button`、`Combo`

`DefaultInvisible` 既定では、コマンドを実装する VSPackage が読み込まれていない場合、または QueryStatus メソッドが呼び出されていない場合、コマンドは非表示になります。

`DynamicVisibility` フラグと組み合わせる必要があります。

有効な対象: `Button`、`Combo`、`Menu`

`DynamicVisibility` コマンドの可視性は、`VisibilityConstraints` メソッド、または `QueryStatus` セクションに含まれているコンテキスト GUID を使用して変更できます。

ツール バーではなく、メニューに表示されるコマンドに適用されます。 `QueryStatus` メソッドから `OLECMDF_INVISIBLE` フラグが返された場合、最上位レベルのツール バー項目は無効にすることができますが、非表示にすることはできません。

メニューでは、このフラグは、メンバーが非表示のときに自動的に非表示にする必要があることも示します。 最上位レベルのメニューには既にこの動作があるため、通常、このフラグはサブメニューに割り当てられます。

`DefaultInvisible` フラグと組み合わせる必要があります。

有効な対象: `Button`、`Combo`、`Menu`

`NoShowOnMenuController` このフラグを持つコマンドがメニュー コントローラーに配置されている場合、そのコマンドはドロップダウン リストに表示されません。

有効な対象: `Button`

コマンド フラグの詳細については、「[CommandFlag 要素](../../extensibility/command-flag-element.md)」のドキュメントを参照してください。

#### <a name="general-requirements"></a>一般的な要件
コマンドは、表示して有効にする前に、次の一連のテストに合格する必要があります。

- コマンドが正しく配置されている。

- `DefaultInvisible` フラグが設定されていない。

- 親メニューまたはツール バーが表示されている。

- [VisibilityConstraints 要素](../../extensibility/visibilityconstraints-element.md)セクションのコンテキスト エントリにより、コマンドは非表示ではない。

- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを実装する VSPackage コードによって、コマンドが表示されて有効になる。 インターフェイス コードによって、インターセプトされておらず、影響されていない。

- ユーザーがコマンドをクリックすると、[ルーティング アルゴリズム](../../extensibility/internals/command-routing-algorithm.md)に関する記事に記載されている手順に従う。

## <a name="call-pre-defined-commands"></a>事前定義済みコマンドの呼び出し
[UsedCommands 要素](../../extensibility/usedcommands-element.md)を使用すると、VSPackages で他の VSPackages または IDE によって提供されるコマンドにアクセスできるようになります。 これを行うには、使用するコマンドの GUID と ID を持つ [UsedCommand 要素](../../extensibility/usedcommand-element.md)を作成します。 これにより、現在の Visual Studio の構成に含まれていない場合でも、コマンドが Visual Studio によって読み込まれるようになります。 詳細については、「[UsedCommand 要素](../../extensibility/usedcommand-element.md)」を参照してください。

## <a name="interface-element-appearance"></a>インターフェイス要素の外観
コマンド要素の選択と配置に関する考慮事項を次に示します。

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] には、配置に応じて表示が異なる多くの UI 要素が用意されています。

- `DefaultInvisible` フラグを使用して定義された UI 要素は、<xref:EnvDTE.IDTCommandTarget.QueryStatus%2A> メソッドの VSPackage 実装によって表示されない場合、または `VisibilityConstraints` セクション内の特定の UI コンテキストに関連付けられていない場合は、IDE に表示されません。

- コマンドが正常に配置されていても、表示されない場合があります。 これは、VSPackage によって実装された (または実装されていない) インターフェイスに応じて、IDE で一部のコマンドが自動的に非表示にされたり表示されたりするためです。 たとえば、VSPackage の一部のビルド インターフェイスを実装すると、ビルド関連のメニュー項目が自動的に表示されます。

- UI 要素の定義に `CommandWellOnly` フラグを適用することは、コマンドを追加できるのはカスタマイズする場合のみであることを意味します。

- コマンドは、特定の UI コンテキストでのみ使用できます。たとえば、IDE がデザイン ビューのときにダイアログボックスが表示される場合にのみ使用できます。

- IDE に特定の UI 要素が表示されるようにするには、1 つまたは複数のインターフェイスを実装するか、コードを記述する必要があります。

## <a name="see-also"></a>関連項目
- [メニューとコマンドを拡張する](../../extensibility/extending-menus-and-commands.md)
