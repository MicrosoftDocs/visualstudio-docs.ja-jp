---
title: コマンド フラグ要素 |Microsoft Docs
description: コマンド フラグ要素によって、その親要素が変更されます。 親要素と子要素を確認します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CommandFlag element (VSCT XML schema)
- VSCT XML schema elements, CommandFlag
ms.assetid: 5ef63399-d2db-4dc1-97ce-be1bd4ef4e39
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1f9f9db3d7a8146bd7b44cf779fd62fd75803d86
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089642"
---
# <a name="command-flag-eelement"></a>コマンド フラグ要素
親要素を変更します。

## <a name="syntax"></a>構文

```
<CommandFlag>DynamicVisibility</CommandFlag>
```

## <a name="attributes-and-elements"></a>属性と要素
 次のセクションでは、有効な要素値について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素

|値|説明|
|-----------|-----------------|
|AllowParams|ユーザーがコマンドの正規名を入力するときに、 **[コマンド]** ウィンドウにコマンド パラメーターを入力できることを示します。<br /><br /> 有効な対象: `Button`|
|AlwaysCreate|グループとボタンのどちらもない場合でもメニューが作成されます。<br /><br /> 有効な対象: `Menu`|
|[CaseSensitive]|ユーザーの入力では、大文字と小文字が区別されます。<br /><br /> 有効な対象: `Combo`|
|CommandWellOnly|コマンドが最上位レベルのメニューに表示されず、追加のシェル カスタマイズ (キーボード ショートカットへのバインディングなど) できるようにする場合は、このフラグを適用します。 VSPackage のインストール後に、 **[オプション]** ダイアログ ボックスを開き、 **[キーボード環境]** カテゴリの下にあるコマンドの配置を編集することで、これらのコマンドをカスタマイズできます。 このフラグは、ショートカット メニュー、ツール バー、メニュー コントローラー、またはサブメニューの配置には影響しません。<br /><br /> 有効な対象: `Button`、`Combo`|
|DefaultDisabled|既定では、コマンドを実装する VSPackage が読み込まれていない場合、または `QueryStatus` メソッドが呼び出されていない場合は、コマンドが無効になります。<br /><br /> 有効な対象: `Button`、`Combo`|
|DefaultDocked|既定ではドッキングされます。 この設定は、常にドッキングされているため、ツール バーには適用されなくなりました。|
|DefaultInvisible|既定では、コマンドを実装する VSPackage が読み込まれていない場合、または `QueryStatus` メソッドが呼び出されていない場合は、コマンドが表示されません。<br /><br /> これは、`DynamicVisibility` フラグと組み合わせて使用することをお勧めします。<br /><br /> 有効な対象: `Button`、`Combo`、`Menu`|
|DontCache|開発環境で、このコマンドの `QueryStatus` メソッドの結果がキャッシュされません。<br /><br /> メニューに対しては、メニュー項目のテキストをキャッシュしないようにメニュー コントローラーに指示します。 このフラグは、動的な項目がメニューに含まれるか、動的なテキストが項目に含まれるときに使用します。<br /><br /> 有効な対象: `Button`、`Menu`|
|DynamicItemStart|動的リストの先頭を示します。 これにより、OLECMDERR_E_UNSUPPORTED フラグが返されるまで、リスト項目に対して `QueryStatus` メソッドを連続して呼び出すことで、環境を構築できます。 これは、最近使用した (MRU) リストやウィンドウ リストなどの項目に適しています。<br /><br /> 有効な対象: `Button`|
|DynamicVisibility|コマンドの可視性は、`QueryStatus` メソッドを使用して、または `VisibilityConstraints` セクションに含まれるコンテキスト GUID を使用して変更できます。<br /><br /> メニューおよびツール ウィンドウのツール バーに表示されるコマンドに適用されますが、メイン ウィンドウに表示される最上位レベルのツール バーには適用されません。 `QueryStatus` メソッドから OLECMDF_INVISIBLE フラグが返されると、最上位レベルのツール バー項目を無効にすることはできますが、非表示にすることはできません。 ツール ウィンドウのツール バーに表示されるツール バー コマンドは非表示にすることができます。<br /><br /> メニューについては、このフラグが、すべてのメンバーが非表示のときに自動的にメニューを非表示にする必要があることも示します。 最上位レベルのメニューには既にこの動作があるため、通常、このフラグはサブメニューに割り当てられます。<br /><br /> このフラグは、`DefaultInvisible` フラグと組み合わせる必要があります。<br /><br /> 有効な対象: `Button`、`Combo`、`Menu`|
|FilterKeys|「[Combo 要素](../extensibility/combo-element.md)」のフィルター処理キーのトピックを参照してください。<br /><br /> 有効な対象: `Combo`|
|FixMenuController|このコマンドがメニュー コントローラーに配置されている場合は、このコマンドが常に既定になります。つまり、メニュー コントローラー ボタン自体が選択されると常に、このコマンドが選択されます。 メニュー コントローラーに `TextIsAnchorCommand` フラグが設定されている場合、メニューコントローラーは、`FixMenuController` フラグが設定されたコマンドからテキストも受け取ります。<br /><br /> `FixMenuController` フラグは、メニュー コントローラーの 1 つのコマンドにのみ設定する必要があります。 複数のコマンドにフラグが設定されている場合は、メニューの最後のコマンドが、既定のコマンドになります。<br /><br /> 有効な対象: `Button`|
|IconAndText|メニューとツール バーにアイコンとテキストを表示します。<br /><br /> 有効な対象: `Button`、`Combo`、`Menu`|
|NoAutoComplete|オートコンプリート機能が無効になります。<br /><br /> 有効な対象: `Combo`|
|NoButtonCustomize|ユーザーがこのボタンをカスタマイズできないようにします。<br /><br /> 有効な対象: `Button`、`Combo`|
|NoKeyCustomize|キーボードのカスタマイズを有効にしません。<br /><br /> 有効な対象: `Button`、`Combo`|
|NoShowOnMenuController|このコマンドがメニュー コントローラーに配置されている場合は、そのコマンドがドロップダウン リストに表示されません。<br /><br /> 有効な対象: `Button`|
|NotInTBList|使用可能なツール バーのリストに表示されません。 これは、Toolbar 型のメニューに対してのみ有効です。<br /><br /> 有効な対象: `Menu`|
|NoToolbarClose|ユーザーはツール バーを閉じることができません。 これは、Toolbar 型のメニューに対してのみ有効です。<br /><br /> 有効な対象: `Menu`|
|Pict|ツール バーにアイコンのみを表示し、メニューにはテキストのみを表示します。 アイコンが指定されていない場合は、クリック可能な空白領域をツール バーに表示します。<br /><br /> 有効な対象: `Button`|
|PostExec|コマンドを非ブロッキングにします。 開発環境により、すべての前処理クエリが完了するまで実行が延期されます。<br /><br /> 有効な対象: `Button`|
|RouteToDocs|コマンドが、アクティブなドキュメントにルーティングされます。<br /><br /> 有効な対象: `Button`|
|StretchHorizontally|このフラグが設定されていると、幅が、コンボ ボックスの最小幅になります。そして、ツール バーに空き領域がある場合は、使用可能なスペースを埋めるようにコンボ ボックスが拡大されます。 これは、ツール バーが水平方向にドッキングされており、ツール バー上の 1 つのコンボ ボックスのみがフラグを使用できる場合にのみ発生します (フラグは、最初のコンボ ボックスを除くすべてで無視されます)。<br /><br /> 有効な対象: `Combo`|
|TextChanges|コマンドまたはメニュー テキストは実行時に、通常は `QueryStatus` メソッドを使用して変更できます。<br /><br /> 有効な対象: `Button`、`Menu`|
|TextChangesButton|有効な対象: `Button`|
|TextIsAnchorCommand|メニュー コントローラーの場合は、メニューのテキストが既定の (アンカー) コマンドから取得されます。 アンカー コマンドとは、最後に選択またはラッチされたコマンドです。 このフラグが設定されていない場合、メニュー コントローラーは、それ自体の `MenuText` フィールドを使用します。 ただし、メニュー コントローラーのクリックによっても、そのコントローラーから最後に選択されたコマンドが有効になります。<br /><br /> このフラグは、`TextChanges` フラグと組み合わせて使用することをお勧めします。<br /><br /> このフラグは、MenuController 型または MenucontrollerLatched 型のメニューにのみ適用されます。<br /><br /> 有効な対象: `Menu`|
|TextMenuCtrlUseMenu|メニュー コントローラー上の `MenuText` フィールドを使用します。 既定のフィールドは `ButtonText` です。<br /><br /> 有効な対象: `Button`|
|TextMenuUseButton|メニューの `ButtonText` フィールドを使用します。 既定のフィールドは `MenuText` です (指定されている場合)。<br /><br /> 有効な対象: `Button`|
|TextOnly|ツール バーまたはメニューにテキストのみを表示します。アイコンが指定されている場合でもアイコンは表示しません。<br /><br /> 有効な対象: `Button`|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Buttons 要素](../extensibility/buttons-element.md)|[Button 要素](../extensibility/button-element.md)の要素のグループを提供します。|
|[Menus 要素](../extensibility/menus-element.md)|VSPackage が実装するすべてのメニューを定義します。|

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
