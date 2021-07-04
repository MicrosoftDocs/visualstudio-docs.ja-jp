---
title: ソリューション エクスプローラーのツールバーへのコマンドの追加 | Microsoft Docs
description: Visual Studio のソリューション エクスプローラーのツールバーにコマンドを実行するボタンを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- toolbars [Visual Studio], adding buttons
- buttons [Visual Studio], adding to Solution Explorer
- Solution Explorer, adding buttons
ms.assetid: f6411557-2f4b-4e9f-b02e-fce12a6ac7e9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0aa75bd1a229be147e3462845a61266a650e072e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900240"
---
# <a name="add-a-command-to-the-solution-explorer-toolbar"></a>ソリューション エクスプローラー ツールバーにコマンドを追加する
このチュートリアルでは、**ソリューション エクスプローラー** のツールバーにボタンを追加する方法について説明します。

 ツールバーまたはメニューのすべてのコマンドは、Visual Studio ではボタンと呼ばれます。 このボタンをクリックすると、コマンド ハンドラーのコードが実行されます。 通常、関連するコマンドは、1 つのグループを形成するためにグループ化されます。 メニューまたはツールバーは、グループのコンテナーとして機能します。 優先順位によって、グループ内の個々のコマンドがメニューまたはツールバーに表示される順序が決定されます。 ツールバーまたはメニューの表示を制御することによって、ボタンが表示されないようにすることができます。 *.vsct* ファイルの `<VisibilityConstraints>` セクションに示されているコマンドは、関連付けられたコンテキストにのみ表示されます。 表示をグループに適用することはできません。

 メニュー、ツールバー コマンド、 *.vsct* ファイルの詳細については、「[コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

> [!NOTE]
> コマンド テーブル構成 ( *.ctc*) ファイルではなく、XML コマンド テーブル ( *.vsct*) ファイルを使用して、VSPackage にメニューとコマンドを表示する方法を定義します。 詳細については、「[Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールすることはしません。 これは、Visual Studio のセットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension-with-a-menu-command"></a>メニュー コマンドを使用した拡張機能の作成
 `SolutionToolbar` という名前の VSIX プロジェクトを作成します。 **ToolbarButton** という名前のメニュー コマンド項目テンプレートを追加します。 この方法の詳細については、[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)に関するページをご覧ください。

## <a name="add-a-button-to-the-solution-explorer-toolbar"></a>ソリューション エクスプローラー ツールバーにボタンを追加する
 このチュートリアルのセクションでは、**ソリューション エクスプローラー** のツールバーにボタンを追加する方法について説明します。 ボタンがクリックされると、コールバック メソッドのコードが実行されます。

1. *ToolbarButtonPackage.vsct* ファイルで、`<Symbols>` セクションに移動します。 `<GuidSymbol>` ノードには、パッケージ テンプレートによって生成されたメニュー グループおよびコマンドが含まれています。 このノードに `<IDSymbol>` 要素を追加して、コマンドを保持するグループを宣言します。

    ```xml
    <IDSymbol name="SolutionToolbarGroup" value="0x0190"/>
    ```

2. `<Groups>` セクションで、既存のグループ エントリの後に、前の手順で宣言した新しいグループを定義します。

    ```xml
    <Group guid="guidToolbarButtonPackageCmdSet"
           id="SolutionToolbarGroup" priority="0xF000">
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
          </Group>
    ```

     親 GUID:ID ペアを `guidSHLMainMenu` と `IDM_VS_TOOL_PROJWIN` に設定することにより、このグループが **ソリューション エクスプローラー** のツールバーに配置され、優先度の高い値を設定すると、他のコマンド グループの後に配置されます。

3. `<Buttons>` セクションで、生成された `<Button>` エントリの親 ID を、前の手順で定義したグループが反映されるように変更します。 変更された `<Button>` 要素は次のようになります。

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

     **ソリューション エクスプローラー** のツールバーに、既存のボタンの右側に新しいコマンド ボタンが表示されるはずです。 ボタン アイコンは取り消し線です。

5. 新しいボタンをクリックします。

     **ToolbarButtonPackage Inside SolutionToolbar.ToolbarButton.MenuItemCallback()** というメッセージを含むダイアログ ボックスが表示されるはずです。

## <a name="control-the-visibility-of-a-button"></a>ボタンの表示を制御する
 チュートリアルのこのセクションでは、ツールバーのボタンの表示を制御する方法について説明します。 *SolutionToolbar.vsct* ファイルの `<VisibilityConstraints>` セクションで 1 つ以上のプロジェクトにコンテキストを設定することにより、プロジェクトまたはプロジェクトが開いている場合にのみ、ボタンが表示されるように制限します。

### <a name="to-display-a-button-when-one-or-more-projects-are-open"></a>1 つ以上のプロジェクトが開いているときにボタンを表示する方法

1. *ToolbarButtonPackage.vsct* の `<Buttons>` セクションで、`<Strings>` と `<Icons>` タグの間の既存の `<Button>` 要素に 2 つのコマンド フラグを追加します。

   ```xml
   <CommandFlag>DefaultInvisible</CommandFlag>
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

    `<VisibilityConstraints>` セクションのエントリが有効になるように、`DefaultInvisible` と `DynamicVisibility` フラグを設定する必要があります。

2. 2 つの `<VisibilityItem>` エントリを持つ `<VisibilityConstraints>` セクションを作成します。 新しいセクションを `</Commands>` 終了タグの直後に配置します。

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

    **ソリューション エクスプローラー** のツールバーに取り消し線ボタンが含まれていません。

4. プロジェクトを含むソリューションを開きます。

    取り消し線ボタンが、ツールバーの既存のボタンの右側に表示されます。

5. **[ファイル]** メニューの **[ソリューションを閉じる]** をクリックします。 ツールバーからボタンが消えます。

   ボタンの表示は、VSPackage が読み込まれるまで [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって制御されます。 VSPackage が読み込まれた後、ボタンの可視性は VSPackage によって制御されます。  詳細については、「[MenuCommands と OleMenuCommands の比較](/previous-versions/visualstudio/visual-studio-2015/misc/menucommands-vs-olemenucommands?preserve-view=true&view=vs-2015)」を参照してください。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)