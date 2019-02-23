---
title: ボタンの再利用可能なグループを作成する |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- button groups, creating in VSPackages
- VSPackages, creating reusable button groups
- buttons, creating reusable groups
ms.assetid: 0c561617-fb86-476d-8bd1-c6e5e7464c65
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 89b4f55e5e5de564db6cb7a1217b79a15283fb93
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56712321"
---
# <a name="create-reusable-groups-of-buttons"></a>ボタンの再利用可能なグループを作成します。
コマンド グループは、常に、メニューまたはツールバーにまとめて表示されるコマンドのコレクションです。 CommandPlacements セクションでは、別の親メニューに割り当てることで、任意のコマンド グループを再利用できる、 *.vsct*ファイル。

 コマンド グループには、ボタン、通常が含まれますが、他のメニューやコンボ ボックスを含めることできますも。

## <a name="to-create-a-reusable-group-of-buttons"></a>ボタンの再利用可能なグループを作成するには

1.  という名前の VSIX プロジェクトを作成する`ReusableButtons`します。 詳細については、次を参照してください。[メニュー コマンドを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-a-menu-command.md)します。

2.  という名前のカスタム コマンド項目テンプレートを追加、プロジェクトが開いたら、 **ReusableCommand**します。 **ソリューション エクスプ ローラー**でプロジェクト ノードを右クリックし、選択**追加** > **新しい項目の**します。 **新しい項目の追加**ダイアログ ボックスに移動して**Visual c#** > **機能拡張**選択と**カスタム コマンド**。 **名前**ウィンドウの下部にあるフィールドに、コマンド ファイル名を変更して*ReusableCommand.cs*します。

3.  *.Vsct*ファイル、シンボルのセクションに移動し、グループ、およびプロジェクトのコマンドを含む GuidSymbol 要素を検索します。 GuidReusableCommandPackageCmdSet、名前にする必要があります。

4.  次の例のように、グループに追加する各ボタン、IDSymbol を追加します。

    ```xml
    <GuidSymbol name="guidReusableCommandPackageCmdSet" value="{7f383b2a-c6b9-4c1d-b4b8-a26dc5b60ca1}">
        <IDSymbol name="MyMenuGroup" value="0x1020" />
        <IDSymbol name="ReusableCommandId" value="0x0100" />
        <IDSymbol name="SecondReusableCommandId" value="0x0200" />
    </GuidSymbol>
    ```

     既定では、コマンドの項目テンプレートがという名前のグループを作成します**MyMenuGroup**と各 IDSymbol エントリと共に、指定された名前を持つボタンをクリックします。

5.  Groups セクションでは、シンボルで示されているものと同じ GUID と ID の属性を持つグループ要素を作成します。 既存のグループを使用してもまたは次の例のように、コマンド テンプレートによって提供されるエントリを使用できます。 このグループが表示されます、**ツール**メニュー

    ```xml
    <Groups>
        <Group guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
              <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_TOOLS"/>
        </Group>
    </Groups>
    ```

## <a name="to-create-a-group-of-buttons-for-reuse"></a>再利用するためのボタンのグループを作成するには

1.  コマンドまたはメニューの定義内の親として、グループを使用するか、CommandPlacements セクションを使用して、コマンドまたはメニューをグループ内に配置することで、グループ内のコマンドまたはメニューに配置できます。

     ボタンのセクションでは、グループ、その親を持つボタンの定義またはのパッケージ テンプレートによって提供されるボタンを使用して、次の例に示すようにします。

    ```xml
    <Button guid="guidReusableCommandPackageCmdSet" id="ReusableCommandId" priority="0x0100" type="Button">
        <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ReusableCommand</ButtonText>
        </Strings>
    </Button>
    ```

2.  ボタンは、1 つ以上のグループに表示する必要があります、コマンド セクションの後に配置する必要があります CommandPlacements のセクションでそのエントリを作成します。 移動するボタンに合わせて CommandPlacement 要素の GUID と ID の属性を設定し、GUID とその親要素の ID がターゲット グループの次の例に示すようにします。

    ```xml
    <CommandPlacements>
        <CommandPlacement guid="guidReusableCommandPackageCmdSet" id="SecondReusableCommandId" priority="0x105">
          <Parent guid="guidReusableCommandPackageCmdSet" id="MyMenuGroup" />
        </CommandPlacement>
    </CommandPlacements>
    ```

    > [!NOTE]
    >  優先順位フィールドの値は、新しいコマンド グループで、コマンドの位置を決定します。 優先順位は、項目の定義で設定されている要素がオーバーライド CommandPlacement で設定します。 高い優先順位値がコマンドの前に、低い優先順位値がコマンドが表示されます。 重複する優先度の値は許可されていますが、ために、同じ優先順位値を持つコマンドの相対位置を保証できません、順序、 **devenv/setup**コマンドでは、レジストリから最終的なインターフェイスを作成します。一貫性のあるできない可能性があります。

## <a name="to-put-a-reusable-group-of-buttons-on-a-menu"></a>メニューのボタンの再利用可能なグループを配置するには

1. 内のエントリを作成、`CommandPlacements`セクション。 GUID と ID の設定、`CommandPlacement`グループの要素とターゲットの場所の親の GUID と ID を設定します。

    CommandPlacements セクションは、「コマンド」セクションの直後後に配置する必要があります。

   ```xml
   <CommandTable>
   ...
     <Commands>... </Commands>
     <CommandPlacements>... </CommandPlacements>
   ...
   </CommandTable>
   ```

    1 つ以上のメニューで、コマンド グループを含めることできます。 親メニュー使用できるいずれか、作成したによって指定された 1 つ[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)](」の説明に従って*ShellCmdDef.vsct*または*SharedCmdDef.vsct*)、または別の VSPackage で定義されている 1 つ。 親レイヤーの数は、親メニューが最終的に接続されている限り、制限[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]または VSPackage によって表示されるショートカット メニューにします。

    次の例では、配置グループ、**ソリューション エクスプ ローラー**ツールバーで、他のボタンの右側にします。

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
