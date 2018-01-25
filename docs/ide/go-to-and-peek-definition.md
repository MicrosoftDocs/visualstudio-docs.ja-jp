---
title: "Visual Studio での型の定義の表示 | Microsoft Docs"
ms.custom: 
ms.date: 01/10/2018
ms.reviewer: 
ms.suite: 
ms.technology: vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- code editor, view definition
- go to definition
- peek definition
- type definition [Visual Studio]
- member definition [Visual Studio]
author: gewarren
ms.author: gewarren
manager: ghogen
ms.workload: multiple
ms.openlocfilehash: 945eb6e905613d3d068321e2d5993f4506036963
ms.sourcegitcommit: f89ed5fc2e5078213e30a6ade4604e34df48181f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2018
---
# <a name="view-type-and-member-definitions"></a>型とメンバーの定義の表示

多くの場合、開発者はコード内で使う型やクラス メンバーのソース コードの定義を確認する必要があります。 Visual Studio では、[定義へ移動] や [定義をここに表示] 機能を使用すると、型またはメンバーの定義を簡単に表示することができます。 ソース コードを使用できない場合は、代わりにメタデータが表示されます。

## <a name="go-to-definition"></a>[定義へ移動]

[定義へ移動] 機能では、型またはメンバーのソースに移動し、新しいタブで結果を開きます。キーボードを使用する場合は、シンボル名内の任意の場所にテキスト カーソルを置いて、**F12** キーを押します。 マウスを使用する場合は、コンテキスト メニューから **[定義へ移動]** を選択するか、以下のセクションで説明する **Ctrl-クリック**機能を使用します。

### <a name="ctrl-click-go-to-definition"></a>Ctrl-クリックの [定義へ移動]

Visual Studio 2017 バージョン 15.4 の場合、マウスを使用すると、より簡単に [定義へ移動] へすばやくアクセスできます。 **Ctrl** キーを押して、型またはメンバーにカーソルを置くと、シンボルがクリック可能になります。 シンボルの定義にすばやく移動するには、**Ctrl** キーを押してからクリックします。 とても簡単ですね。

![マウス クリックの [定義へ移動] のアニメーション](../ide/media/click_gotodef.gif)

マウス クリックの **[定義へ移動]** の修飾キーを変更するには、**[ツール]**、**[オプション]**、**[テキスト エディター]**、**[全般]** の順に移動し、**[修飾子キーを使用する]** ドロップダウンから **[Alt]** または **[Ctrl+Alt]** を選択します。 **[マウス クリックを有効にして [定義へ移動] を実行する]** チェック ボックスをオフにして、マウス クリックの **[定義へ移動]** を無効にすることもできます。

![マウス クリックの [定義へ移動] の無効化](../ide/media/editor_options_mouse_click_gotodef.png)

## <a name="peek-definition"></a>定義をここに表示

[定義をここに表示] 機能を使用すれば、エディターで現在の場所を離れずに型の定義をプレビューすることができます。 キーボードを使用する場合は、型またはメンバー名内の任意の場所にテキスト カーソルを置いて、**Alt + F12** キーを押します。 マウスを使用する場合は、コンテキスト メニューから **[定義をここに表示]** を選択できます。 Visual Studio 2017 バージョン 15.4 以降では、マウスを使用して定義をピーク表示するという新しい方法があります。 まず、**[ツール]**、**[オプション]**、**[テキスト エディター]**、**[全般]** の順に移動します。 オプションの **[定義をピーク ビューで開く]** を選択し、**[OK]** をクリックして **[オプション]** ダイアログ ボックスを閉じます。

![マウス クリックの [定義をここに表示] オプションの設定](../ide/media/editor_options_peek_view.png)

次に、**Ctrl** キー (または **[オプション]** で選択されている修飾キーのいずれか) を押して、型またはメンバーをクリックします。

![[定義をここに表示] のアニメーション](../ide/media/peek_definition.gif)

ポップアップ ウィンドウから別の定義を表示する場合は、ポップアップの上に表示される円と矢印を使ってナビゲートできる階層リンク パスを開始します。

詳細については、「[方法: [定義をここに表示] を使用してコードを表示および編集する (Alt + F12)](how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)」を参照してください。

## <a name="view-metadata-as-source-code-c"></a>ソース コードとしてのメタデータの表示 (C#)

ソース コードを使用できない C# の型またはメンバーの定義を表示すると、代わりにそのメタデータが表示されます。 型とメンバーの宣言は確認できますが、実装は確認できません。

ソースコードを使用できない項目に対して **[定義へ移動]** または **[定義をここに表示]** コマンドを実行すると、その項目のメタデータのビューを含むタブ付きドキュメントが、ソース コードとしてコード エディターに表示されます。 末尾に **[メタデータから]**が続く型の名前がドキュメントのタブに表示されます。

たとえば、<xref:System.Console> に対して **[定義へ移動]** コマンドを実行すると、<xref:System.Console> のメタデータが C# のソース コードとしてコード エディターに表示されます。 このコードはその宣言に似ていますが、実装は表示されません。

![ソースとしてのメタデータ](../ide/media/metadatasource.png "MetadataSource")

> [!NOTE]
> 内部としてマークされた型やメンバーに対して **[定義へ移動]** または **[定義をここに移動]** コマンドを実行しても、参照元のアセンブリがフレンドかどうかに関係なく、Visual Studio はメタデータをソース コードとして表示しません。

### <a name="view-decompiled-source-definitions-instead-of-metadata-c"></a>メタデータ (C#) に代わる逆コンパイルされたソース定義の表示

**Visual Studio 2017 バージョン 15.6 preview 2** の新機能では、ソース コードが使用できない C# の型やメンバーの定義を表示するときに、逆コンパイルされたソース コードを表示するオプションを設定できます。 この機能を有効にするには、メニュー バーから **[ツール]** > **[オプション]** の順に選択します。 次に、**[テキスト エディター]** > **[C#]** > **[詳細]** の順に展開して、**[Enable navigation to decompiled sources]\(逆コンパイルされたソースへのナビゲーションを有効にする\)** を選択します。

![逆コンパイルされた定義の表示](media/go-to-definition-decompiled-sources.png)

> [!NOTE]
> Visual Studio では、メソッド本体は ILSpy 逆コンパイルを使用して再構築されます。 初めてこの機能にアクセスするときは、ソフトウェア ライセンス、著作権、商標の法律に関する法的な免責事項に同意していただく必要があります。

## <a name="see-also"></a>関連項目

[コード間の移動](../ide/navigating-code.md)  
[方法: [定義をここに表示] を使用してコードを表示および編集する (Alt + F12)](how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)
