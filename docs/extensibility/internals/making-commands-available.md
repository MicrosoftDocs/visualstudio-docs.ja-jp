---
title: コマンドを使用可能にする | Microsoft Docs
description: 遅延読み込み、コンテキスト、表示を使用して、VSPackage で Visual Studio IDE に追加されるコマンドの可用性を制御する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- best practices, menu and toolbar commands
- toolbars [Visual Studio], best practices
- menu commands, best practices
ms.assetid: 3ffc4312-c6db-4759-a946-a4bb85f4a17a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 29f5e5c634c1bf360409e35c87684282a26e8a07
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095213"
---
# <a name="making-commands-available"></a>コマンドを使用可能にする

複数の VSPackage が Visual Studio に追加されると、ユーザー インターフェイス (UI) がコマンドでいっぱいになることがあります。 この問題の軽減には、パッケージを次のようにプログラミングすると役立ちます。

- ユーザーが要求したときにのみ読み込まれるようにパッケージをプログラミングします。

- 統合開発環境 (IDE) の現在の状態のコンテキストで必要になったときにのみコマンドが表示されるようにパッケージをプログラミングします。

## <a name="delayed-loading"></a>遅延読み込み

遅延読み込みを有効にするには、一般に、UI にコマンドが表示されるが、ユーザーがいずれかのコマンドをクリックするまでパッケージ自体は読み込まれないように VSPackage を設計します。 これを行うには、.vsct ファイルで、コマンド フラグを持たないコマンドを作成します。

次の例は、.vsct ファイルからのメニュー コマンドの定義を示しています。 これは、テンプレートの **[メニュー コマンド]** オプションが選択されている場合に Visual Studio パッケージ テンプレートによって生成されるコマンドです。

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

この例では、親グループ (`MyMenuGroup`) が **[ツール]** メニューなどのトップレベル メニューの子である場合、コマンドはそのメニューに表示されますが、コマンドを実行するパッケージは、ユーザーがコマンドをクリックするまで読み込まれません。 ただし、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを実装するようにコマンドをプログラミングして、コマンドを含むメニューを最初に展開したときにパッケージが読み込まれるようにすることができます。

なお、遅延読み込みにより起動時のパフォーマンスが向上することもあります。

## <a name="current-context-and-the-visibility-of-commands"></a>コマンドの現在のコンテキストと表示

VSPackage データの現在の状態や、現在関連しているアクションに応じて表示と非表示が切り替わるように VSPackage コマンドをプログラミングできます。 VSPackage でそのコマンドの状態を設定できるようにするには、通常は <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスからの <xref:EnvDTE.IDTCommandTarget.QueryStatus%2A> メソッドの実装を使用しますが、この場合、コードの実行前に VSPackage を読み込んでおく必要があります。 代わりに、パッケージを読み込まずにコマンドの表示を IDE で管理できるようにすることをお勧めします。 これを行うには、.vsct ファイルで、コマンドを 1 つ以上の特別な UI コンテキストに関連付けます。 これらの UI コンテキストは、"*コマンド コンテキスト GUID*" と呼ばれる GUID で識別されます。

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、プロジェクトの読み込みや、編集からビルドへの移行などのユーザー アクションによって生じた変更を監視します。 変更が生じると、IDE の表示が自動的に変更されます。 次の表に、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で監視される IDE の変更の 4 つの主要コンテキストを示します。

| コンテキストの種類 | 説明 |
|-------------------------| - |
| アクティブなプロジェクトの種類 | ほとんどの種類のプロジェクトで、この `GUID` 値は、プロジェクトを実装する VSPackage の GUID と同じになります。 ただし、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] プロジェクトでは、`GUID` のプロジェクトの種類を値として使用します。 |
| アクティブ ウィンドウ | 通常、これは、キー バインド用に現在の UI コンテキストを確立する最後のアクティブなドキュメント ウィンドウです。 ただし、内部 Web ブラウザーに類似したキー バインド テーブルを持つツール ウィンドウになることもあります。 HTML エディターなどの複数タブのドキュメント ウィンドウでは、すべてのタブでコマンド コンテキスト `GUID` が異なっています。 |
| アクティブな言語サービス | テキスト エディターで現在表示されているファイルに関連付けられている言語サービス。 |
| アクティブなツール ウィンドウ | 開いており、フォーカスがあるツール ウィンドウ。 |

5 番目の主要コンテキスト領域は、IDE の UI 状態です。 UI コンテキストは、次のように、アクティブなコマンド コンテキスト `GUID` で識別されます。

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Dragging_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.FullScreenMode_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.DesignMode_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.NoSolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.CodeWindow_guid>

これらの GUID は、IDE の現在の状態に応じて、アクティブまたは非アクティブとしてマークされます。 複数の UI コンテキストを同時にアクティブにすることができます。

### <a name="hide-and-display-commands-based-on-context"></a>コンテキストに基づいてコマンドの表示と非表示を切り替える

パッケージ自体を読み込まずに、IDE でのパッケージ コマンドの表示と非表示を切り替えることができます。 これを行うには、`DefaultDisabled`、`DefaultInvisible`、`DynamicVisibility` コマンド フラグを使用し、1 つ以上の [VisibilityItem](../../extensibility/visibilityitem-element.md) 要素を [VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) セクションに追加して、パッケージの .vsct ファイルでコマンドを定義します。 指定されたコマンド コンテキスト `GUID` がアクティブになると、パッケージを読み込まずにコマンドが表示されます。

### <a name="custom-context-guids"></a>カスタム コンテキスト GUID

適切なコマンド コンテキスト GUID がまだ定義されていない場合は、VSPackage でコマンド コンテキスト GUID を定義してから、必要に応じてアクティブまたは非アクティブになるようにプログラミングしてコマンドの表示を制御できます。 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> サービスを使用して、次の操作を行います。

- (<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A> メソッドを呼び出して) コンテキスト GUID を登録します。

- (<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> メソッドを呼び出して) コンテキスト `GUID` の状態を取得します。

- (<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A> メソッドを呼び出して) コンテキスト `GUID` をオンまたはオフにします。

    > [!CAUTION]
    > VSPackage が既存のコンテキスト GUID の状態に影響しないことを確認してください。これは、他の Vspackage が依存している可能性があるためです。

## <a name="example"></a>例

次の VSPackage コマンドの例は、VSPackage を読み込まずにコマンド コンテキストで管理されるコマンドの動的な表示を示しています。

このコマンドは、ソリューションが存在するときはいつでも、つまり次のコマンド コンテキスト GUID のいずれかがアクティブなときはいつでも、有効になり、表示されるように設定されています。

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

この例では、すべてのコマンド フラグが個別の[コマンド フラグ](../../extensibility/command-flag-element.md)要素であることに注意してください。

```xml
<Button guid="guidDynamicVisibilityCmdSet" id="cmdidMyCommand"
        priority="0x0100" type="Button">
  <Parent guid="guidDynamicVisibilityCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <CommandFlag>DefaultDisabled</CommandFlag>
  <CommandFlag>DefaultInvisible</CommandFlag>
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <CommandName>cmdidMyCommand</CommandName>
    <ButtonText>My Command name</ButtonText>
  </Strings>
</Button>
```

また、次のように、すべての UI コンテキストを個別の `VisibilityItem` 要素で指定する必要があることにも注意してください。

```xml
<VisibilityConstraints>
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                  id="cmdidMyCommand" context="UICONTEXT_EmptySolution" />
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                      id="cmdidMyCommand" context="UICONTEXT_SolutionHasSingleProject" />
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                  id="cmdidMyCommand" context="UICONTEXT_SolutionHasMultipleProjects" />
</VisibilityConstraints>
```

## <a name="see-also"></a>関連項目

- [ソリューション エクスプローラー ツールバーにコマンドを追加する](../../extensibility/adding-a-command-to-the-solution-explorer-toolbar.md)
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Vspackage のコマンド ルーティング](../../extensibility/internals/command-routing-in-vspackages.md)
- [メニュー項目の動的な追加](../../extensibility/dynamically-adding-menu-items.md)
