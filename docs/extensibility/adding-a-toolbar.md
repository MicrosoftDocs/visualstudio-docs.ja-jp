---
title: ツールバーの追加 | Microsoft Docs
description: コマンドにバインドされているボタンを含んだツールバーを、Visual Studio 統合開発環境 (IDE) に追加する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- toolbars [Visual Studio], adding to IDE
- IDE, adding toolbars
ms.assetid: 17302c25-6f59-4e97-8c85-54f95336a07f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e1b478041492bfb857c5497b6df5e2c4af9ad355
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094940"
---
# <a name="add-a-toolbar"></a>ツールバーを追加する
このチュートリアルでは、Visual Studio IDE にツールバーを追加する方法について説明します。

 ツールバーとは、コマンドにバインドされたボタンを含む、水平または垂直のストリップです。 IDE のツールバーは、実装に応じて、再配置したり、メイン IDE ウィンドウの任意の辺にドッキングしたり、常に他のウィンドウより前面に表示させたりすることができます。

 さらに、ユーザーは **[カスタマイズ]** ダイアログ ボックスを使用して、ツールバーでのコマンドの追加や削除を行えます。 通常、VSPackage のツールバーはユーザーがカスタイズできます。 カスタマイズはすべて IDE で処理され、コマンドへの応答は VSPackage で行われます。 コマンドの物理的な配置場所が VSPackage で把握されている必要はありません。

 メニューに関する詳細については、「[コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターからの Visual Studio SDK のインストールは行いません。 これは、Visual Studio セットアップにオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-an-extension-with-a-toolbar"></a>ツールバーを使用して拡張機能を作成する
 `IDEToolbar` という名前の VSIX プロジェクトを作成します。 **ToolbarTestCommand** という名前のメニュー コマンド項目テンプレートを追加します。 この方法の詳細については、[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)に関するページを参照してください。

## <a name="create-a-toolbar-for-the-ide"></a>IDE のツール バーを作成する

1. *ToolbarTestCommandPackage.vsct* で、[Symbols] セクションを探します。 guidToolbarTestCommandPackageCmdSet という名前の GuidSymbol 要素で、次のようにツール バーとツールバー グループの宣言を追加します。

    ```xml
    <IDSymbol name="Toolbar" value="0x1000" />
    <IDSymbol name="ToolbarGroup" value="0x1050" />

    ```

2. [Commands] セクションの最上部で [Menus] セクションを作成します。 [Menus] セクションに [Menu] 要素を追加して、ツール バーを定義します。

    ```xml
    <Menus>
        <Menu guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"
            type="Toolbar" >
            <CommandFlag>DefaultDocked</CommandFlag>
            <Strings>
                <ButtonText>Test Toolbar</ButtonText>
                <CommandName>Test Toolbar</CommandName>
            </Strings>
          </Menu>
    </Menus>
    ```

     ツール バーをサブメニューのように入れ子にすることはできません。 したがって、親グループを割り当てる必要はありません。 また、ユーザーがツール バーを移動できるので、優先度を設定する必要もありません。 通常、ツール バーの最初の配置はプログラムによって定義されますが、ユーザーによるその後の変更は保持されます。

3. [[Groups]](../extensibility/groups-element.md) セクションの既存のグループ エントリの後に、ツール バーのコマンドを含むように [[Group]](../extensibility/group-element.md) 要素を定義します。

    ```xml
    <Group guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup"
          priority="0x0000">
      <Parent guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"/>
    </Group>
    ```

4. ボタンをツール バーに表示させます。 [Buttons] セクションで、[Button] の [Parent] ブロックをツール バーに置き換えます。 結果の [Button] ブロックは次のようになります。

    ```xml
    <Button guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarTestCommandId" priority="0x0100" type="Button">
        <Parent guid= "guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup" />
                <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ToolbarTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     既定では、ツール バーにコマンドがない場合、ツール バーは表示されません。

5. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

6. Visual Studio のメニュー バーを右クリックして、ツール バーの一覧を表示します。 **[ツール バーのテスト]** を選択します。

7. これでツール バーは、[フォルダーを指定して検索] アイコンの右側にアイコンとして表示されているはずです。 アイコンをクリックすると、「**ToolbarTestCommandPackage. Inside IDEToolbar.ToolbarTestCommand.MenuItemCallback()** 」というメッセージ ボックスが表示されます。

## <a name="see-also"></a>関連項目
- [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
