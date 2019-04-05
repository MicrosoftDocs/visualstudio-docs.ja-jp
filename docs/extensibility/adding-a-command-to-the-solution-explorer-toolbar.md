---
title: ソリューション エクスプ ローラーのツールバーにコマンドの追加 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- toolbars [Visual Studio], adding buttons
- buttons [Visual Studio], adding to Solution Explorer
- Solution Explorer, adding buttons
ms.assetid: f6411557-2f4b-4e9f-b02e-fce12a6ac7e9
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fff1187793350b52484bcac99021be7fc2845607
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56717794"
---
# <a name="add-a-command-to-the-solution-explorer-toolbar"></a>ソリューション エクスプ ローラーのツールバーにコマンドを追加します。
このチュートリアルでは、ボタンを追加する方法、**ソリューション エクスプ ローラー**ツールバー。

 ツールバーまたはメニューのすべてのコマンドには、Visual Studio でのボタンは呼び出されます。 このボタンをクリックすると、コマンド ハンドラーのコードが実行されます。 通常、関連するコマンドは 1 つのグループ化されます。 メニューまたはツールバーは、グループのコンテナーとして機能します。 優先順位は、メニューまたはツールバーで、グループ内の個々 のコマンドを表示する順序を決定します。 ボタンを防ぐため、その可視性を制御することで、ツールバーまたはメニューに表示されることができます。 記載されているコマンド、`<VisibilityConstraints>`のセクション、 *.vsct*ファイルが関連付けられているコンテキストでのみが表示されます。 可視性は、グループに適用できません。

 メニュー、ツールバーのコマンドの詳細については、 *.vsct*ファイルを参照してください[コマンド、メニューのおよびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)します。

> [!NOTE]
>  XML コマンド テーブルの使用 (*.vsct*) コマンド テーブル構成ではなくファイル (*.ctc*) ファイルを Vspackage でのメニューとコマンドの表示方法を定義します。 詳細については、[Visual Studio Command Table (を参照してください。Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降、ダウンロード センターから Visual Studio SDK をインストールすることはできません。 これは Visual Studio のセットアップにオプション機能として含まれるようになりました。 また、後から VS SDK をインストールすることもできます。 より詳細な情報については 、[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md) に関する記事を参照してください。

## <a name="create-an-extension-with-a-menu-command"></a>メニュー コマンドを使用して拡張機能を作成します。
 という名前の VSIX プロジェクトを作成する`SolutionToolbar`します。 という名前のメニュー コマンド項目テンプレートを追加**ツールバー ・ ボタン**します。 これを行う方法については、[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)を参照してください。

## <a name="add-a-button-to-the-solution-explorer-toolbar"></a>ソリューション エクスプ ローラーのツールバーにボタンを追加します。
 このチュートリアルのこのセクションでは、ボタンを追加する方法を示しています。、**ソリューション エクスプ ローラー**ツールバー。 このボタンをクリックすると、コールバック メソッドでコードが実行されます。

1.  *ToolbarButtonPackage.vsct*に移動して、ファイル、`<Symbols>`セクション。 `<GuidSymbol>`ノードには、メニューのグループおよびパッケージ テンプレートによって生成されたコマンドが含まれています。 追加、`<IDSymbol>`要素は、コマンドを保持するグループを宣言するには、このノードにします。

    ```xml
    <IDSymbol name="SolutionToolbarGroup" value="0x0190"/>
    ```

2.  `<Groups>`セクションでは、の 既存のグループ エントリの後に前の手順で定義を宣言する新しいグループ。

    ```xml
    <Group guid="guidToolbarButtonPackageCmdSet"
           id="SolutionToolbarGroup" priority="0xF000">
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
          </Group>
    ```

     親 GUID:ID のペアを設定`guidSHLMainMenu`と`IDM_VS_TOOL_PROJWIN`にこのグループを設定、**ソリューション エクスプ ローラー**ツールバー、および優先度の高い値を設定するその他のコマンド グループの後に配置します。

3.  `<Buttons>`セクションで、生成された親 ID を変更、`<Button>`前の手順で定義されているグループを反映するように入力します。 変更された`<Button>`要素は、次のようになります。

    ```xml
    <Button guid="guidToolbarButtonPackageCmdSet" id="ToolbarButtonId" priority="0x0100" type="Button">
        <Parent guid="guidToolbarButtonPackageCmdSet" id="SolutionToolbarGroup" />
        <Icon guid="guidImages" id="bmpPicStrikethrough" />
        <Strings>
            <ButtonText>Invoke ToolbarButton</ButtonText>
        </Strings>
    </Button>
    ```

4.  プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

     **ソリューション エクスプ ローラー**既存のボタンの右側に新しいコマンド ボタンがツールバーに表示する必要があります。 ボタンのアイコンは、取り消し線です。

5.  新しいボタンをクリックします。

     ダイアログ ボックスに、メッセージ**ToolbarButtonPackage 内 SolutionToolbar.ToolbarButton.MenuItemCallback()** が表示されます。

## <a name="control-the-visibility-of-a-button"></a>ボタンの表示を制御します。
 このチュートリアルのこのセクションでは、ツールバーのボタンの表示を制御する方法を示します。 内の 1 つまたは複数のプロジェクトにコンテキストを設定して、`<VisibilityConstraints>`のセクション、 *SolutionToolbar.vsct*ファイルのみまたはプロジェクトを開いているときに表示するためのボタンを制限します。

### <a name="to-display-a-button-when-one-or-more-projects-are-open"></a>1 つまたは複数のプロジェクトが開いているときにボタンを表示するには

1. `<Buttons>`のセクション*ToolbarButtonPackage.vsct*、2 つのコマンド フラグを追加、既存`<Button>`要素間に、`<Strings>`と`<Icons>`タグ。

   ```xml
   <CommandFlag>DefaultInvisible</CommandFlag>
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

    `DefaultInvisible`と`DynamicVisibility`ためフラグを設定する必要がありますでそのエントリ、`<VisibilityConstraints>`セクションが有効になります。

2. 作成、 `<VisibilityConstraints>` 2 つ含まれるセクション`<VisibilityItem>`エントリ。 終了した直後の新しいセクションの配置`</Commands>`タグ。

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

    可視性の各項目は、指定したボタンを表示する条件を表します。 複数の条件を適用するには、同じボタンの複数のエントリを作成する必要があります。

3. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

    **ソリューション エクスプ ローラー**ツールバーに取り消し線 ボタンが含まれていません。

4. プロジェクトを含む任意のソリューションを開きます。

    取り消し線 ボタンは、既存のボタンの右側にツールバーが表示されます。

5. **ファイル** メニューのをクリックして**ソリューションを閉じる**します。 ツールバーのボタンが表示されなくなります。

   ボタンの可視性がによって制御される[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]VSPackage が読み込まれるまでです。 VSPackage が読み込まれた後、ボタンの可視性は、VSPackage によって制御されます。  詳細については、[Menucommand とを参照してください。OleMenuCommands](../extensibility/menucommands-vs-olemenucommands.md)します。

## <a name="see-also"></a>関連項目
- [コマンド、メニューのおよびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)