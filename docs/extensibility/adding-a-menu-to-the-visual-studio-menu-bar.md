---
title: Visual Studio のメニュー バーへのメニューの追加 | Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) のメニュー バーにメニューを追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- menus, creating top level
- top-level menus
ms.assetid: 58fc1a31-2aeb-441c-8e48-c7d5cbcfe501
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 22ce9bc00f24278fd2c0533052d7bd5e944b1ebf
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078345"
---
# <a name="add-a-menu-to-the-visual-studio-menu-bar"></a>Visual Studio のメニュー バーへのメニューの追加

このチュートリアルでは、Visual Studio 統合開発環境 (IDE) のメニュー バーにメニューを追加する方法について説明します。 IDE のメニューバーには、 **[ファイル]** 、 **[編集]** 、 **[表示]** 、 **[ウィンドウ]** 、 **[ヘルプ]** などのメニュー カテゴリがあります。

新しいメニューを Visual Studio のメニュー バーに追加する前に、コマンドを既存のメニュー内に配置するかどうかを検討してください。 コマンドの配置の詳細については、「[Visual Studio のメニューとコマンド](../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)」を参照してください。

メニューは、プロジェクトの *.vsct* ファイルで宣言されます。 メニューおよび *.vsct* ファイルの詳細については、「[コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

このチュートリアルを終了すると、1 つのコマンドを含む "**Test Menu**" という名前のメニューを作成できます。

:::moniker range=">=vs-2019"
> [!NOTE]
> Visual Studio 2019 以降では、拡張機能によって提供される最上位のメニューは **[拡張機能]** メニューに配置されます。
:::moniker-end

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-vsix-project-that-has-a-custom-command-item-template"></a>カスタム コマンド項目テンプレートを含む VSIX プロジェクトを作成する

1. `TopLevelMenu` という名前の VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログで「vsix」と検索すると見つかります。  詳細については、「[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

::: moniker range="vs-2017"

2. プロジェクトが開いたら、**Testcommand** という名前のカスタム コマンド項目テンプレートを追加します。 **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >   **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Visual C#]、[拡張機能]** の順に移動し、 **[カスタム コマンド]** を選択します。 ウィンドウの下部にある **[名前]** フィールドで、コマンド ファイル名を *TestCommand.cs* に変更します。

::: moniker-end

::: moniker range=">=vs-2019"

2. プロジェクトが開いたら、**Testcommand** という名前のカスタム コマンド項目テンプレートを追加します。 **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >   **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Visual C#]、[拡張機能]** の順に移動し、 **[コマンド]** を選択します。 ウィンドウの下部にある **[名前]** フィールドで、コマンド ファイル名を *TestCommand.cs* に変更します。

::: moniker-end

## <a name="create-a-menu-on-the-ide-menu-bar"></a>IDE のメニュー バーのメニューを作成する

::: moniker range="vs-2017"

1. **ソリューション エクスプローラー** で、*TestCommandPackage.vsct* を開きます。

    ファイルの末尾には、複数の `<GuidSymbol>` ノードを含む `<Symbols>` ノードがあります。 `guidTestCommandPackageCmdSet` という名前のノードで、次のように新しいシンボルを追加します。

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. `<Commands>` ノードの `<Groups>` の直前に、空の `<Menus>` ノードを作成します。 `<Menus>` ノードで、次のように `<Menu>` ノードを追加します。

   ```xml
   <Menus>
         <Menu guid="guidTestCommandPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
           <Parent guid="guidSHLMainMenu"
                   id="IDG_VS_MM_TOOLSADDINS" />
           <Strings>
             <ButtonText>Test Menu</ButtonText>
           </Strings>
       </Menu>
   </Menus>
   ```

    メニューの `guid` および `id` の値で、コマンド セットとコマンド セット内の特定のメニューを指定します。

    親の `guid` および `id` の値により、Visual Studio のメニュー バーの、[ツール] と [アドイン] メニューを含むセクションにメニューが配置されます。

    `<ButtonText>` 要素で、テキストをメニュー項目に表示することを指定します。

3. `<Groups>` セクションで `<Group>` を探し、前の手順で追加したメニューをポイントするように `<Parent>` 要素を変更します。

   ```xml
   <Groups>
       <Group guid="guidTestCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTestCommandPackageCmdSet" id="TopLevelMenu"/>
       </Group>
   </Groups>
   ```

    これで、グループの部分が新しいメニューに追加されます。

::: moniker-end

::: moniker range=">=vs-2019"

1. **ソリューション エクスプローラー** で、*TopLevelMenuPackage.vsct* を開きます。

    ファイルの末尾には、複数の `<GuidSymbol>` ノードを含む `<Symbols>` ノードがあります。 `guidTopLevelMenuPackageCmdSet` という名前のノードで、次のように新しいシンボルを追加します。

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. `<Commands>` ノードの `<Groups>` の直前に、空の `<Menus>` ノードを作成します。 `<Menus>` ノードで、次のように `<Menu>` ノードを追加します。

   ```xml
   <Menus>
         <Menu guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
           <Parent guid="guidSHLMainMenu"
                   id="IDG_VS_MM_TOOLSADDINS" />
           <Strings>
             <ButtonText>Test Menu</ButtonText>
           </Strings>
       </Menu>
   </Menus>
   ```

    メニューの `guid` および `id` の値で、コマンド セットとコマンド セット内の特定のメニューを指定します。

    親の `guid` および `id` の値により、Visual Studio のメニュー バーの、[ツール] と [アドイン] メニューを含むセクションにメニューが配置されます。

    `<ButtonText>` 要素で、テキストをメニュー項目に表示することを指定します。

3. `<Groups>` セクションで `<Group>` を探し、前の手順で追加したメニューをポイントするように `<Parent>` 要素を変更します。

   ```xml
   <Groups>
       <Group guid="guidTopLevelMenuPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu"/>
       </Group>
   </Groups>
   ```

    これで、グループの部分が新しいメニューに追加されます。

::: moniker-end

4. `<Buttons>` セクションで、`<Button>` ノードを探します。 次に、`<Strings>` ノードで、`<ButtonText>` 要素を `Test Command` に変更します。

    [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] パッケージ テンプレートによって、親が `MyMenuGroup` に設定されている `Button` 要素が生成されたことに注意してください。 その結果、このコマンドがメニューに表示されます。

## <a name="build-and-test-the-extension"></a>拡張機能をビルドしてテストする

1. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスのインスタンスが表示されます。

::: moniker range="vs-2017"

2. 実験用インスタンスのメニュー バーには、 **[Test Menu]** メニューが含まれています。

::: moniker-end

::: moniker range=">=vs-2019"

2. 実験用インスタンスの **[拡張機能]** メニューには、 **[Test Menu]** メニューが含まれています。

::: moniker-end

3. **[Test Menu]** メニューで、 **[Test Command]** を選択します。

    メッセージ ボックスが表示され、"TestCommand Inside TopLevelMenu.TestCommand.MenuItemCallback()" というメッセージが表示されます。

## <a name="see-also"></a>関連項目

- [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
