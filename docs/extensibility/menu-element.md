---
title: Menu 要素 | Microsoft Docs
description: Menu 要素では、1 つのメニュー項目を定義します。 メニューの種類は、Context、Menu、MenuController、MenuControllerLatched、Toolbar、ToolWindowToolbar です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Menus
- Menus element (VSCT XML schema)
ms.assetid: ce0560f3-b4c9-4ab2-a99c-d4e10f37b9e0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7427b826249bd29c73c928630eed0941c57b997d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064047"
---
# <a name="menu-element"></a>Menu 要素
1 つのメニュー項目を定義します。 これらは、Context、Menu、MenuController、MenuControllerLatched、Toolbar、ToolWindowToolbar の 6 種類のメニューです。

## <a name="syntax"></a>構文

```xml
<Menu guid="guidMyCommandSet" id="MyCommand" priority="0x100" type="button">
  <Parent>... </Parent>
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</Menu>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 GUID/ID コマンド識別子の GUID。|
|id|必須。 GUID/ID コマンド識別子の ID。|
|priority|省略可能。 メニューのグループ内のメニューの相対的な位置を指定する数値。|
|ToolbarPriorityInBand|省略可能。 ウィンドウがドッキングされているときのバンド内のツール バーの相対的な位置を指定する数値。|
|型|省略可能。 要素の種類を指定する列挙値。<br /><br /> 存在しない場合、既定の種類は Menu です。<br /><br /> Context<br /> ユーザーがウィンドウを右クリックしたときに表示されるショートカット メニュー。 ショートカット メニューには、次の特性があります。<br /><br /> -   メニューがショートカット メニューとして表示される場合は、**Parent** および **Priority** フィールドを使用しません。<br />-   サブメニューとして使用でき、ショートカット メニューとしても使用できます。 この場合は、**Group ID** フィールドと **Priority** フィールドの両方が考慮されます。<br />-   常に使用できるとは限りません。<br /><br /> ショートカット メニューは、次の条件に当てはまる場合にのみ表示されます。<br /><br /> -   それをホストするウィンドウが表示されている。<br />-   VSPackage のマウス ハンドラーがウィンドウの右クリックを検出した後、そのコマンドを処理するメソッドを呼び出す。<br />-   <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager.ShowContextMenu%2A> メソッド (推奨されるアプローチ) または <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A> メソッドを呼び出すことによってショートカット メニューが表示される。<br /><br /> メニュー<br /> ドロップダウン メニューを提供します。 ドロップダウン メニューには、次の特性があります。<br /><br /> -   その定義内の Parent を考慮します。<br />-   Parent グループ、またはグループへの CommandPlacement が存在する必要があります。<br />-   他の任意の種類のメニューのサブメニューにすることができます。<br />-   その親メニューが表示されるたびに自動的に表示されます。<br />-   これが表示されるようにするために VSPackage コードを実装する必要はありません。<br /><br /> MenuController<br /> ツール バーで一般に使用される分割ボタン ドロップダウン メニューを提供します。 MenuController メニューには、次の特性があります。<br /><br /> -   Parent または CommandPlacement 経由で別のメニューに含まれている必要があります。<br />-   その定義内の Parent を考慮します。<br />-   その親として任意の種類のメニューを持つことができます。<br />-   その親メニューが表示されるたびに自動的に使用可能になります。<br />-   このメニューを表示するためにプログラムによるサポートは必要ありません。<br /><br /> このメニュー ボタンには、分割ボタン メニューのコマンドが表示されます。 表示されるコマンドには、次のいずれかの特性があります。<br /><br /> -   これは、そのコマンドがまだ表示され、有効になっていた場合に使用された最後のコマンドです。<br />-   これは、最初に表示されるコマンドです。<br /><br /> MenuControllerLatched<br /> コマンドをラッチ済みとしてマークすることによってコマンドを既定の選択として指定できる分割ボタン ドロップダウン メニューを提供します。<br /><br /> ラッチされたコマンドは、通常はチェック マークを表示することにより、メニューで選択済みとしてマークされているコマンドです。 コマンドは、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスの `QueryStatus` メソッドの実装でそれに対して OLECMDF_LATCHED フラグが設定されている場合に、ラッチ済みとしてマークできます。 MenuControllerLatched メニューには、次の特性があります。<br /><br /> -   Parent グループまたは CommandPlacement 経由で別のメニューに含まれている必要があります。<br />-   その定義内の Parent を考慮します。<br />-   その親として任意の種類のメニューを持つことができます。<br />-   その親メニューが表示されるたびに使用可能になります。<br />-   このメニューを表示するためにプログラムによるサポートは必要ありません。<br /><br /> このメニュー ボタンには、分割ボタン メニューのコマンドが表示されます。 表示されるコマンドには、次のいずれかの特性があります。<br /><br /> -   これは、ラッチされた最初に表示されるコマンドです。<br />-   これは、最初に表示されるコマンドです。<br /><br /> ツール バー<br /> ツール バーを提供します。 ツール バーには、次の特性があります。<br /><br /> -   その定義内の Parent を無視します。<br />-   CommandPlacement を使用した場合でも、どのグループのサブメニューにすることもできません。<br />-   常に **[表示]** メニューの **[ツール バー]** をクリックして表示できます。<br />-   [VisibilityItem](../extensibility/visibilityitem-element.md) を使用して表示できます。<br />-   これを作成するためにコードは必要ありません。 ツール バーを作成する方法に関する例については、「[ツール バーの追加](../extensibility/adding-a-toolbar.md)」を参照してください。<br /><br /> ToolWindowToolbar<br /> ツール バーが開発環境にアタッチされているのと同様に、特定のツール ウィンドウにアタッチされているツール バーを提供します。<br /><br /> -   その定義内の Parent を無視します。<br />-   CommandPlacement を使用した場合でも、どのグループのサブメニューにすることもできません。<br />-   ツール バーをホストするツール ウィンドウが表示されていて、VSPackage がそのツール バーをそのツール ウィンドウに明示的に追加した場合にのみ表示されます。 これは通常、ツール ウィンドウが作成されるときに、ツール ウィンドウ フレームから (<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost> インターフェイスによって表される) ツール バーのホスト プロパティを取得し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost.AddToolbar%2A> メソッドを呼び出すことによって実行されます。|
|条件|省略可能。 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)に関するページを参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|Parent|省略可能。 メニュー項目の親要素。|
|CommandFlag|必須。 「[コマンド フラグ要素](../extensibility/command-flag-element.md)」を参照してください。 Menu の有効な CommandFlag 値は次のとおりです。<br /><br /> -   **AlwaysCreate**<br />-   **DefaultDocked**<br />-   **DefaultInvisible** - このフラグはツール バーの表示に影響を与えません。<br />-   **DontCache**<br />-   **DynamicVisibility** - このフラグはツール バーの表示に影響を与えません。<br />-   **IconAndText**<br />-   **NoCustomize**<br />-   **NotInTBList**<br />-   **NoToolbarClose**<br />-   **TextChanges**<br />-   **TextIsAnchorCommand**|
|文字列|必須。 「[Strings 要素](../extensibility/strings-element.md)」を参照してください。 子の `ButtonText` 要素を定義する必要があります。|
|注釈|省略可能なコメント。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Menus 要素](../extensibility/menus-element.md)|VSPackage で実装するすべてのメニューを定義します。|

## <a name="example"></a>例

```
<Menu guid="cmdGuidWidgetCommands" id="menuIDEditWidget"
  priority="0x0002" type="Menu">
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit"/>
  <CommandFlag>AlwaysCreate</CommandFlag>
  <Strings>
    <ButtonText>Edit Widget</ButtonText>
  </Strings>
</Menu>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
