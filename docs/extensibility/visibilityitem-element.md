---
title: VisibilityItem 要素 | Microsoft Docs
description: VisibilityItem 要素では、コマンドとツールバーを静的に表示するかどうかを決定します。 エントリによって、コマンドまたはメニュー、および関連付けられているコマンド UI コンテキストを識別します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VisibilityItem element (VSCT XML schema)
- VSCT XML schema elements, VisibilityItem
ms.assetid: 0932f551-972d-4194-84bb-426e3e4375e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1229c5e63838a8192c7622cdddd9881799a2da11
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062513"
---
# <a name="visibilityitem-element"></a>VisibilityItem 要素
`VisibilityItem` 要素では、コマンドとツールバーを静的に表示するかどうかを決定します。 各エントリによって、コマンドまたはメニュー、および関連付けられているコマンド UI コンテキストを識別します。 Visual Studio では、コマンド、メニュー、ツールバー、およびそれらの表示/非表示を、これらを定義する VSPackage を読み込まずに検出します。 IDE では、<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> メソッドを使用して、コマンド UI コンテキストがアクティブかどうかを判定します。

 Visual Studio では、VSPackage が読み込まれた後、`VisibilityItem` ではなく VSPackage によってコマンドの表示/非表示が決定されることを想定しています。 コマンドの表示/非表示を決定するには、コマンドの実装方法に応じて、<xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> イベント ハンドラーまたは <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> メソッドのいずれかを実装します。

 `VisibilityItem` 要素を含むコマンドまたはメニューは、関連付けられたコンテキストがアクティブな場合にのみ表示されます。 1 つのコマンド、メニュー、またはツールバーを 1 つ以上のコマンド UI コンテキストと関連付けるには、コマンド コンテキストの組み合わせごとに 1 つのエントリを追加します。 コマンドまたはメニューが複数のコマンド UI コンテキストに関連付けられている場合は、関連付けられているコマンド UI コンテキストのいずれかがアクティブになっているときに、そのコマンドまたはメニューが表示されます。

 `VisibilityItem` 要素は、グループではなく、コマンド、メニュー、ツールバーにのみ適用されます。 関連する `VisibilityItem` 要素を持たない要素は、その親メニューがアクティブになるたびに表示されます。

## <a name="syntax"></a>構文

```xml
<VisibilityItem
  guid="cmdGuidMyProductCommands"
  id="cmdidAddWidget"
  context="guidNotViewSourceMode"/>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 GUID/ID コマンド識別子の GUID。|
|id|必須。 GUID/ID コマンド識別子の ID。|
|context|必須。 コマンドが表示される UI コンテキスト。|
|条件|省略可能。 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)に関するページを参照してください。|

### <a name="child-elements"></a>子要素
 なし

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[VisibilityConstraints 要素](../extensibility/visibilityconstraints-element.md)|`VisibilityConstraints` 要素では、コマンドとツールバーのグループを静的に表示するかどうかを決定します。|

## <a name="remarks"></a>解説
 標準の Visual Studio UI コンテキストは、<*Visual Studio SDK のインストール パス*>\VisualStudioIntegration\Common\Inc\vsshlids.h ファイルと共に、<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids> クラスおよび <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> クラスでも定義されています。 UI コンテキストの完全なセットは、<xref:Microsoft.VisualStudio.VSConstants> クラスで定義されています。

## <a name="example"></a>例

```xml
<VisibilityConstraints>
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"
    context="guidNotViewSourceMode"/>
</VisibilityConstraints>
```

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>
- <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>
- <xref:Microsoft.VisualStudio.VSConstants>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>
- [VisibilityConstraints 要素](../extensibility/visibilityconstraints-element.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
