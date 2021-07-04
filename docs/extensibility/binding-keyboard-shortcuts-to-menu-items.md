---
title: キーボード ショートカットのメニュー項目へのバインド | Microsoft Docs
description: Visual Studio のキーボード ショートカットを、既定のエディターまたはカスタム エディターのいずれかの、カスタムのボタン、メニュー項目、またはツールバー コマンドにマップする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- keyboard command
- keyboards
- command key
- keyboard shortcuts
- menu items
ms.assetid: 19f483b6-4d3e-424e-9d68-dc129c788e47
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6a9591a7412b0bcaf506483a16a6660790df5f40
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900435"
---
# <a name="bind-keyboard-shortcuts-to-menu-items"></a>キーボード ショートカットをメニュー項目にバインドする
キーボード ショートカットをカスタム メニュー コマンドにバインドするには、パッケージの *.vsct* ファイルにただエントリを追加します。 このトピックでは、キーボード ショートカットをカスタムのボタン、メニュー項目、またはツールバー コマンドにマップする方法と、キーボード マップを、既定のエディターで適用したり、カスタム エディターに制限したりする方法について説明します。

 既存の Visual Studio メニュー項目にキーボード ショートカットを割り当てるには、[キーボード ショートカットの識別とカスタマイズ](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)に関するページを参照してください。

## <a name="choose-a-key-combination"></a>キーの組み合わせを選択する
 Visual Studio では既に、多くのキーボード ショートカットが使用されています。 バインドの重複は、検出するのが困難で、予期しない結果を引き起こす可能性もあるため、複数のコマンドに同じショートカットを割り当ててはいけません。 そのため、ショートカットを割り当てる前に、利用可能であることの確認をお勧めします。

### <a name="to-verify-the-availability-of-a-keyboard-shortcut"></a>キーボード ショートカットを利用可能であることを確認するには

1. **[ツール]**  >  **[オプション]**  >  **[環境]** ウィンドウで、 **[キーボード]** を選択します。

2. **[使用する場所]** が **[グローバル]** に設定されていることを確認します。

3. **[ショートカット キー]** ボックスに、使用するキーボード ショートカットを入力します。

    ショートカットが既に Visual Studio で使用されている場合は、そのショートカットによって現在呼び出されるコマンドが、 **[現在使用されているショートカット]** ボックスに表示されます。

4. マップされていないキーの組み合わせが見つかるまで、さまざまな組み合わせを試してください。

   > [!NOTE]
   > **Alt** キーを使用するキーボード ショートカットでは、メニューを開けますがコマンドを直接実行できません。 そのため、**Alt** キーを含むショートカットを入力すると、 **[現在使用されているショートカット]** ボックスが空白になることがあります。 **[オプション]** ダイアログ ボックスを閉じてキーを押せば、そのショートカットでメニューが開かないことを確認できます。

   次の手順は、1 つのメニュー コマンドがある既存の VSPackage を前提としています。 それを行うヘルプが必要な場合は、「[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

### <a name="to-assign-a-keyboard-shortcut-to-a-command"></a>コマンドにキーボード ショートカットを割り当てるには

1. パッケージの *.vsct* ファイルを開きます。

2. まだない場合は、`<Commands>` の後に空の `<KeyBindings>` セクションを作成します。

   > [!WARNING]
   > キー バインドの詳細については、[Keybinding](../extensibility/keybinding-element.md) に関するページを参照してください。

    `<KeyBindings>` セクション内に `<KeyBinding>` エントリを作成します。

    `guid` および `id` 属性を、呼び出そうとしているコマンドの属性に設定します。

    `mod1` 属性を **Control**、**Alt**、または **Shift** に設定します。

    KeyBindings セクションはこのようになるはずです。

   ```xml
   <KeyBindings>
       <KeyBinding guid="<name of command set>" id="<name of command id>"
           editor="guidVSStd97" key1="1" mod1="CONTROL"/>
   </KeyBindings>

   ```

   キーボード ショートカットに 3 つ以上のキーが必要な場合は、`mod2` および `key2` 属性を設定します。

   たいていの場合は、**Shift** キーを押すとほとんどの英数字キーで大文字または記号を入力することになるため、2 番目の修飾子なしでこのキーを使用しないでください。

   仮想キー コードを使用すると、関数キーや **Backspace** キーなど、文字が関連付けられていない特殊なキーにアクセスすることができます。 詳細については、「[仮想キー コード](/windows/desktop/inputdev/virtual-key-codes)」を参照してください。

   Visual Studio エディターでコマンドを使用できるようにするには、`editor` 属性を `guidVSStd97` に設定します。

   カスタム エディターでのみコマンドを使用できるようにするには、`editor` 属性を、カスタム エディターを含む VSPackage を作成したときに [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] パッケージ テンプレートによって生成されたカスタム エディターの名前に設定します。 名前の値を見つけるには、`name` 属性が "`editorfactory`" で終わる `<GuidSymbol>` ノードの `<Symbols>` セクションを調べます。これがカスタム エディターの名前です。

## <a name="example-1"></a>例 1
 この例では、キーボード ショートカットの **Ctrl**+**Alt**+**C** を、`MyPackage` という名前のパッケージの `cmdidMyCommand` という名前のコマンドにバインドしています。

```
<CommandTable>
. . .
<Commands>
. . .
</Commands>
<KeyBindings>
  <KeyBinding guid="guidMyPackageCmdSet" id="cmdidMyCommand"
      key1="C" mod1="CONTROL" mod2="ALT" editor="guidVSStd97" />
</KeyBindings>
. . .
</CommandTable>
```

## <a name="example-2"></a>例 2
 この例では、キーボード ショートカットの **Ctrl**+**B** を、`TestEditor` という名前のプロジェクトの `cmdidBold` という名前のコマンドにバインドしています。 このコマンドは、カスタム エディターでのみ使用でき、他のエディターでは使用できません。

```xml
<KeyBinding guid="guidVSStd97" id="cmdidBold" editor="guidTestEditorEditorFactory" key1="B" mod1="Control" />
```

## <a name="see-also"></a>関連項目
- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
