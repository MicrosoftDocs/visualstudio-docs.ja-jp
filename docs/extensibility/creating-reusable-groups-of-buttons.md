---
title: 再利用可能なボタンのグループの作成 | Microsoft Docs
description: メニューまたはツールバーに一緒に表示されるコマンドのコレクションであるコマンド グループを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- button groups, creating in VSPackages
- VSPackages, creating reusable button groups
- buttons, creating reusable groups
ms.assetid: 0c561617-fb86-476d-8bd1-c6e5e7464c65
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6b9c0bd759083a0d0d053133cc9f2d4d03a52389
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055740"
---
# <a name="create-reusable-groups-of-buttons"></a>再利用可能なボタンのグループを作成する
コマンド グループは、メニューまたはツールバーに常に一緒に表示されるコマンドのコレクションです。 すべてのコマンド グループは、 *.vsct* ファイルの CommandPlacements セクションで別の親メニューに割り当てることで再利用できます。

 通常、コマンド グループにはボタンが含まれますが、他のメニューやコンボ ボックスを含めることもできます。

## <a name="to-create-a-reusable-group-of-buttons"></a>再利用可能なボタンのグループを作成するには

1. `ReusableButtons` という名前の VSIX プロジェクトを作成します。 詳細については、「[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください。

2. プロジェクトが開いたら、**ReusableCommand** という名前のカスタム コマンド項目テンプレートを追加します。 **ソリューション エクスプローラー** で、プロジェクト ノードを右クリックして、 **[追加]**  >  **[新しい項目]** の順に選択します。 **[新しい項目の追加]** ダイアログで、 **[Visual C#]**  >  **[機能拡張]** の順にアクセスし、 **[カスタム コマンド]** を選択します。 ウィンドウの下部にある **[名前]** フィールドで、コマンド ファイル名を *ReusableCommand.cs* に変更します。

3. *.vsct* ファイルの Symbols セクションに移動し、プロジェクトのグループとコマンドを含む GuidSymbol 要素を見つけます。 名前は guidReusableCommandPackageCmdSet です。

4. 次の例に示すように、グループに追加する各ボタンの IDSymbol を追加します。

    ```xml
    <GuidSymbol name="guidReusableCommandPackageCmdSet" value="{7f383b2a-c6b9-4c1d-b4b8-a26dc5b60ca1}">
        <IDSymbol name="MyMenuGroup" value="0x1020" />
        <IDSymbol name="ReusableCommandId" value="0x0100" />
        <IDSymbol name="SecondReusableCommandId" value="0x0200" />
    </GuidSymbol>
    ```

     既定では、コマンド項目テンプレートによって、**MyMenuGroup** という名前のグループと指定した名前のボタンが、それぞれ IDSymbol エントリを使用して一緒に作成されます。

5. Groups セクションで、Symbols セクションで指定したのと同じ GUID および ID 属性を含む Group 要素を作成します。 また、既存のグループを使用したり、次の例に示すように、コマンド テンプレートによって提供されるエントリを使用したりすることもできます。 このグループは、 **[ツール]** メニューに表示されます。

    ```xml
    <Groups>
        <Group guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
              <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS"/>
        </Group>
    </Groups>
    ```

## <a name="to-create-a-group-of-buttons-for-reuse"></a>再利用するためにボタンのグループを作成するには

1. コマンドまたはメニューをグループに含めるには、コマンドまたはメニューの定義でそのグループを親として使用するか、CommandPlacements セクションを使用してコマンドまたはメニューをグループに配置します。

     Buttons セクションで、グループが親になるようにボタンを定義するか、次の例に示すように、パッケージ テンプレートによって提供されるボタンを使用します。

    ```xml
    <Button guid="guidReusableCommandPackageCmdSet" id="ReusableCommandId" priority="0x0100" type="Button">
        <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ReusableCommand</ButtonText>
        </Strings>
    </Button>
    ```

2. 1 つのボタンを複数のグループに表示する必要がある場合は、そのためのエントリを CommandPlacements セクション (Commands セクションの後に配置する必要がある) に作成します。 次の例に示すように、CommandPlacement 要素の GUID および ID 属性を配置するボタンに合わせて設定し、Parent 要素の GUID および ID をターゲット グループに合わせて設定します。

    ```xml
    <CommandPlacements>
        <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="SecondReusableCommandId" priority="0x105">
          <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        </CommandPlacement>
    </CommandPlacements>
    ```

    > [!NOTE]
    > Priority フィールドの値によって、新しいコマンド グループ内でのコマンドの位置が決まります。 CommandPlacement 要素で設定された優先順位は、項目定義での設定をオーバーライドします。 優先順位の値が低いコマンドは、優先順位の値が高いコマンドよりも前に表示されます。 重複する値を優先順位に指定できますが、優先順位の値が同じコマンドの相対的な位置は保証されません。**devenv /setup** コマンドによって最終的なインターフェイスがレジストリから作成される順序に一貫性がないためです。

## <a name="to-put-a-reusable-group-of-buttons-on-a-menu"></a>再利用可能なボタンのグループをメニューに配置するには

1. `CommandPlacements` セクションにエントリを作成します。 `CommandPlacement` 要素の GUID と ID をグループのものに設定し、親の GUID と ID をターゲットの場所のものに設定します。

    CommandPlacements セクションは、Commands セクションの直後に配置する必要があります。

   ```xml
   <CommandTable>
   ...
     <Commands>... </Commands>
     <CommandPlacements>... </CommandPlacements>
   ...
   </CommandTable>
   ```

    コマンド グループは、複数のメニューに含めることができます。 親メニューとして使用できるのは、自分で作成したもの、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] (*ShellCmdDef.vsct* または *SharedCmdDef.vsct* に記述されている) で提供されるもの、または別の VSPackage で定義されるものです。 親メニューが最終的に [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] または VSPackage によって表示されるショートカット メニューに結び付けられる限り、親の階層数に制限はありません。

    次の例では、**ソリューション エクスプローラー** のツールバーの他のボタンの右側に、グループを配置しています。

   ```xml
   <CommandPlacements>
       <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0xF00">
         <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
       </CommandPlacement>
   </CommandPlacements>
   ```

   ```xml
   <CommandPlacements>
     <CommandPlacement guid="guidButtonGroupCmdSet" id="MyMenuGroup"
         priority="0x605">
       <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS" />
     </CommandPlacement>
   </CommandPlacements>

   ```
