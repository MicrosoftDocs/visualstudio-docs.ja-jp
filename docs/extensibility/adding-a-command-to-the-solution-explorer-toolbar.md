---
title: ソリューションエクスプローラーツールバーにコマンドを追加する |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- toolbars [Visual Studio], adding buttons
- buttons [Visual Studio], adding to Solution Explorer
- Solution Explorer, adding buttons
ms.assetid: f6411557-2f4b-4e9f-b02e-fce12a6ac7e9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 99a21a4dd4c39a4cefdf6be30171c503fc2ce005
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73187111"
---
# <a name="add-a-command-to-the-solution-explorer-toolbar"></a>ソリューションエクスプローラーツールバーにコマンドを追加する
このチュートリアルでは、 **[ソリューションエクスプローラー]** ツールバーにボタンを追加する方法について説明します。

 ツールバーまたはメニューのすべてのコマンドは、Visual Studio のボタンと呼ばれます。 このボタンをクリックすると、コマンドハンドラーのコードが実行されます。 通常、関連するコマンドは、1つのグループを形成するためにグループ化されます。 メニューまたはツールバーは、グループのコンテナーとして機能します。 優先順位によって、グループ内の個々のコマンドがメニューまたはツールバーに表示される順序が決まります。 ツールバーまたはメニューの表示を制御することによって、ボタンが表示されないようにすることができます。 *Vsct*ファイルの `<VisibilityConstraints>` セクションに示されているコマンドは、関連付けられたコンテキストにのみ表示されます。 表示をグループに適用することはできません。

 メニュー、ツールバーコマンド、および*vsct*ファイルの詳細については、「[コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

> [!NOTE]
> コマンドテーブル構成 (*ctc*) ファイルではなく、XML コマンドテーブル (*vsct*) ファイルを使用して、vspackage にメニューとコマンドを表示する方法を定義します。 詳細については、「 [Visual Studio コマンドテーブル ()」を参照してください。Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

## <a name="prerequisites"></a>必要条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension-with-a-menu-command"></a>メニューコマンドを使用して拡張機能を作成する
 `SolutionToolbar`という名前の VSIX プロジェクトを作成します。 **ToolbarButton**という名前のメニューコマンド項目テンプレートを追加します。 これを行う方法については、「[メニューコマンドを使用して拡張機能を作成](../extensibility/creating-an-extension-with-a-menu-command.md)する」を参照してください。

## <a name="add-a-button-to-the-solution-explorer-toolbar"></a>ソリューションエクスプローラーツールバーにボタンを追加する
 チュートリアルのこのセクションでは、**ソリューションエクスプローラー**ツールバーにボタンを追加する方法について説明します。 ボタンがクリックされると、コールバックメソッドのコードが実行されます。

1. *Toolbarbuttonpackage. vsct*ファイルで、[`<Symbols>`] セクションにアクセスします。 [`<GuidSymbol>`] ノードには、パッケージテンプレートによって生成されたメニューグループおよびコマンドが含まれています。 このノードに `<IDSymbol>` 要素を追加して、コマンドを保持するグループを宣言します。

    ```xml
    <IDSymbol name="SolutionToolbarGroup" value="0x0190"/>
    ```

2. [`<Groups>`] セクションで、既存のグループエントリの後に、前の手順で宣言した新しいグループを定義します。

    ```xml
    <Group guid="guidToolbarButtonPackageCmdSet"
           id="SolutionToolbarGroup" priority="0xF000">
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
          </Group>
    ```

     親 GUID: ID のペアを `guidSHLMainMenu` に設定すると `IDM_VS_TOOL_PROJWIN` このグループが**ソリューションエクスプローラー**ツールバーに配置され、高優先度の値を設定すると他のコマンドグループの後に配置されます。

3. [`<Buttons>`] セクションで、生成された `<Button>` エントリの親 ID を、前の手順で定義したグループを反映するように変更します。 変更された `<Button>` 要素は次のようになります。

    ```xml
    <Button guid="guidToolbarButtonPackageCmdSet" id="ToolbarButtonId" priority="0x0100" type="Button">
        <Parent guid="guidToolbarButtonPackageCmdSet" id="SolutionToolbarGroup" />
        <Icon guid="guidImages" id="bmpPicStrikethrough" />
        <Strings>
            <ButtonText>Invoke ToolbarButton</ButtonText>
        </Strings>
    </Button>
    ```

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

     **ソリューションエクスプローラー**ツールバーに、既存のボタンの右側に [新しいコマンド] ボタンが表示されます。 ボタンアイコンは取り消し線です。

5. [新規] ボタンをクリックします。

     ダイアログボックスが表示されます。このダイアログボックスには、 **ToolbarButton. MenuItemCallback ()** というメッセージが表示されます。

## <a name="control-the-visibility-of-a-button"></a>ボタンの表示を制御する
 チュートリアルのこのセクションでは、ツールバーのボタンの表示を制御する方法について説明します。 Solutiontoolbar の `<VisibilityConstraints>` セクションで1つ以上のプロジェクトにコンテキストを設定することにより、プロジェクトまたはプロジェクトが開いている場合にのみ、ボタンを表示するように制限し*ます。*

### <a name="to-display-a-button-when-one-or-more-projects-are-open"></a>1つ以上のプロジェクトが開いているときにボタンを表示するには

1. *Toolbarbuttonpackage. vsct*の `<Buttons>` セクションで、`<Strings>` と `<Icons>` タグの間にある既存の `<Button>` 要素に2つのコマンドフラグを追加します。

   ```xml
   <CommandFlag>DefaultInvisible</CommandFlag>
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

    `<VisibilityConstraints>` セクションのエントリが有効になるように、`DefaultInvisible` フラグと `DynamicVisibility` フラグを設定する必要があります。

2. 2つの `<VisibilityItem>` エントリを持つ `<VisibilityConstraints>` セクションを作成します。 新しいセクションを、終了 `</Commands>` タグの直後に配置します。

   ```xml
   <VisibilityConstraints>
       <VisibilityItem guid="guidToolbarButtonPackageCmdSet"
             id="ToolbarButtonId"
             context="UICONTEXT_SolutionHasSingleProject" />
       <VisibilityItem guid="guidToolbarButtonPackageCmdSet"
             id="ToolbarButtonId"
             context="UICONTEXT_SolutionHasMultipleProjects" />
   </VisibilityConstraints>
   ```

    各可視性項目は、指定されたボタンが表示される条件を表します。 複数の条件を適用するには、同じボタンに対して複数のエントリを作成する必要があります。

3. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

    **ソリューションエクスプローラー**ツールバーに取り消し線ボタンが含まれていません。

4. プロジェクトを含むソリューションを開きます。

    ツールバーの [取り消し線] ボタンが、既存のボタンの右側に表示されます。

5. **[ファイル]** メニューの **[ソリューションを閉じる]** をクリックします。 ツールバーのボタンが消えます。

   ボタンの表示は、VSPackage が読み込まれるまで [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって制御されます。 VSPackage が読み込まれた後、ボタンの可視性は VSPackage によって制御されます。  詳細については、「 [Menucommands と OleMenuCommands](/visualstudio/extensibility/menucommands-vs-olemenucommands?view=vs-2015)」を参照してください。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)