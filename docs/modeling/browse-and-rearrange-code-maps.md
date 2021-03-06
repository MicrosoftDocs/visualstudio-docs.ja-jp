---
title: コード マップの参照および再配置
description: コード マップ上の項目を再配置して、読みやすさとパフォーマンスを向上させる方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.progression.dgmlgraph.layouthelp
- vs.progression.graphdocument
- vs.progression.dgmlgraph.message.notUlt.noexpandgroup
- vs.progression.colorsetpicker
- vs.progression.iconsetpicker
helpviewer_keywords:
- Visual Studio Ultimate, dependency graphs
- code visualization [Visual Studio ALM]
- graph documents, browsing
- Visual Studio ALM, dependency graphs
- code visualization
- Visual Studio ALM, graph documents
- Visual Studio Ultimate, graph documents
- dependency graphs, browsing
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 83132cfccd0af7244cf31f502669144eb3388bd8
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385553"
---
# <a name="browse-and-rearrange-code-maps"></a>コード マップの参照および再配置

コード マップ上のアイテムを再配置して、読みやすさとパフォーマンスを向上させます。

ソリューション内の基本コードに影響を与えずに、コード マップをカスタマイズすることができます。 この機能は、重要なコード要素に重点を置きたいときや、コードに関するアイデアをやりとりするときに便利です。 たとえば、興味のある領域を強調表示するために、マップ上のコード要素を選択してフィルター処理すること、コード要素とリンクのスタイルを変更すること、コード要素を非表示または削除すること、プロパティ、カテゴリ、またはグループを使用してコード要素を整理することができます。

 **必要条件**

- コード マップを作成するには、Visual Studio Enterprise が必要です。

- Visual Studio Professional でコード マップを表示して、制限付きでコード マップを編集することができます。

## <a name="get-started-working-with-code-maps"></a><a name="ManageLargeGraphs"></a> コード マップの作業開始

コード マップを作成します (詳細については、「[ソリューション間の依存関係をマッピングする](../modeling/map-dependencies-across-your-solutions.md)」を参照してください)。 マップの生成の終了まで待ちたくない場合は、いつでも **[キャンセル]** リンクをクリックして、生成プロセスを停止します。 ただし、この操作を実行した場合、従属関係とリンクの詳細をすべて確認することはできません。

マップを生成した後、コードの確認に関する以下のヒントを実行します。

- コード内の自然な依存関係クラスターを確認します。 マップのツールバーで、 **[レイアウト]** 、 **[クイック クラスター]** ![グラフ ツールバーの [クイック クラスター] ボタン](../modeling/media/quickclustersicon.gif) の順に選択します。 「[マップ レイアウトの変更](#Selecting)」を参照してください。

     ![依存関係グラフ &#45; クイック クラスター レイアウト](../modeling/media/dependencygraph_quickclusters.png)

- 関連するノードをグループ化することで、マップをさらに小さい領域に整理します。 これらのグループを折りたたみ、グループ間の依存関係のみが示されるようにします。これは、自動的に表示されます。 「[ノードのグループ化](#OrganizeGroups)」を参照してください。

- フィルターを使ってマップを簡略化し、興味のある種類のノードやリンクだけに注目できるようにします。 「[ノードとリンクのフィルター処理](#FilterNodes)」を参照してください。

- 大きなマップのパフォーマンスを最大にします。 詳細については、「[ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)」を参照してください。たとえば、マップ上の項目を更新した場合に Visual Studio でソリューションがリビルドされないようにするには、マップのツールバーで **[ビルドのスキップ]** をオンにします。

## <a name="change-the-map-layout"></a><a name="Selecting"></a> マップ レイアウトの変更

|**To**|**実行する手順**|
|-|-|
|グラフ全体の依存関係のフローを特定の方向に配置します。 これは、コードのアーキテクチャ レイヤーを確認するのに役立ちます。|マップのツールバーで **[レイアウト]** を選択してから、次を選択します。<br /><br /> -    **[上から下]** ![[上から下] グラフ ボタン](../modeling/media/topbottomgraphbutton.gif)<br />-    **[下から上]** ![[下から上] グラフ ボタン](../modeling/media/bottomtopgraphbutton.gif)<br />-    **[左から右]** ![[左から右] レイアウト ボタン](../modeling/media/leftrightgraphbutton.gif)<br />-    **[右から左]** ![[右から左] グラフ ボタン](../modeling/media/rightleftgraphbutton.gif)|
|コード内のクラスターの自然な依存関係を確認します。最も依存度の高いノードはクラスターの中心付近にあり、最も依存度の低いノードはそれらのクラスターの外側にあります。|マップのツールバーで、 **[レイアウト]** 、 **[クイック クラスター]** ![グラフ ツールバーの [クイック クラスター] ボタン](../modeling/media/quickclustersicon.gif) の順に選択します。|
|マップ上の 1 つまたは複数のノードを選択します。|ノードをクリックして選択します。 複数のノードを選択するか選択解除するには、**Ctrl** キーを押しながらクリックします。<br /><br /> キーボード: **Tab** キーを押すか方向キーを使って、フォーカスを表す、点線で表示された四角形をノードに移動し、**Space** キーを押して選択します。 **Ctrl** + **Space** キーを押して、複数のノードを選択または選択解除します。|
|マップ上で特定のノードを移動します。|ノードをドラッグして移動します。 ノードをドラッグするときに、他のノードやリンクを邪魔にならない位置に移動するには、**Shift** キーを押しながらノードをドラッグします。<br /><br /> キーボード: **Ctrl** キーを押しながら、方向キーを押します。|
|マップ上の他のノードやグループとは独立して、グループ内のレイアウトを変更します。|ノードを選択して、ショートカット メニューを開きます。 **[レイアウト]** を選択して、レイアウト スタイルを選択します。<br /><br /> または<br /><br /> ノードを選択して展開し、子ノードを表示します。 ノード タイトルをクリックして、グループのポップアップ ツールバーを表示し、 **[グループのレイアウト スタイルを変更します]** ![依存関係グラフ &#45; グループ ツールバー &#45; レイアウト](../modeling/media/dependencygraph_grouptoolbar.gif) 一覧を開きます。 ツリーのレイアウト、 **[クイック クラスター]** 、または **[リスト ビュー]** (グループのコンテンツを整理してリストに表示) のいずれかを選択します。<br /><br /> 詳細については、「[ノードのグループ化](#OrganizeGroups)」を参照してください。|
|マップ内のアクションを元に戻します。|**Ctrl** + **Z** キーを押すか、Visual Studio の **[元に戻す]** コマンドを使用します。|

## <a name="browse-the-map"></a><a name="Explore"></a> マップの参照

|**To**|**実行する手順**|
|-|-|
|マップをスキャンします。|マウスを使って、マップを任意の方向にドラッグします。<br /><br /> または<br /><br /> **Shift** キーを押しながら、マウス ホイールを回転させ、水平方向にスクロールします。 **Shift** + **Ctrl** キーを押しながら、マウス ホイールを回転させ、水平方向にスクロールします。|
|グラフを拡大または縮小します。|マウス ホイールを回します。<br /><br /> または<br /><br /> コード マップのツールバーの **[ズーム]** ドロップダウン リストを使います。<br /><br /> または<br /><br /> キーボード ショートカットを使います。 ズームインするには、**Ctrl+Shift+.** キーを押します。 (ピリオド) を押します。 ズームアウトするには、**Ctrl+Shift+,** (コンマ) キーを押します。|
|マウスを使って特定の領域をズームインします。|マウスの右ボタンをクリックしたまま、対象の領域を四角形で囲みます。|
|マップのサイズを変更してウィンドウに合わせます。|コード マップのツールバーの **[ズーム]** 一覧から、 **[ウィンドウのサイズに合わせて大きさを変更]** を選択します。<br /><br /> または<br /><br /> コード マップのツールバーの **[ウィンドウのサイズに合わせて大きさを変更]** アイコン ![マップのツールバーの [ズーム] アイコン](../modeling/media/almcodemapzoomicon.png) をクリックします。 キーボード: **Ctrl+0** (ゼロ) を押します。|
|マップ上のノードを名前で検索します。 **ヒント:** これは、マップ上の項目に対してのみ機能します。 マップ上ではなく、ソリューション内で項目を見つけるには、**ソリューション エクスプローラー** で検索して、マップにドラッグします。 (選択した項目をドラッグするか、**ソリューション エクスプローラー** のツールバーで **[コードマップに表示]** をクリックします)。|1. コード マップのツールバーで **検索** アイコン ![マップのツールバーの検索アイコン](../modeling/media/almcodemapfindicon.png) をクリックする (キーボード: **CTRL+F** キーを押す) と、マップの右上隅に検索ボックスが表示されます。<br />2. 項目名を入力して **Return** キーを押すか、"拡大鏡" アイコンをクリックします。 検索に一致する最初の項目が、マップで選択された状態で表示されます。<br />3. 検索をカスタマイズするには、ドロップダウン リストを開き、検索オプションを選択します。 オプションは、 **[次を検索]** 、 **[前を検索]** 、 **[すべて選択]** です。 次に、[検索] ボックスの横にある対応するボタンをクリックします。<br />     ![検索オプションのドロップダウン リスト](../modeling/media/almcodemapssearchdropdown.png)<br />     または、キーボードを使用します。**F3** キーを押して、次に一致するノードを選択するか、**Shift+F3** キーを押して、前に一致したノードを選択します。<br />4. 検索テキスト ボックスの下のアイコンをクリックして、検索語句の処理方法を指定するオプションのいずれかを選択します。<br />     ![一致するオプションの検索](../modeling/media/almcodemapssearchmatchicons.png)<br />     オプションは、左から順に、大文字と小文字を区別して検索、完全に一致する単語だけを検索、.NET の正規表現の構文を使用して検索、囲まれた項目と一致する項目が表示されるようにグループを自動的に展開する、となっています。 **重要:** 検索ボックスを使用することで折りたたまれたグループで一致を検索できるのは、これらのグループを既に展開している場合だけです。 これらの一致を検索し、親グループを自動的に展開するには、検索ボックスでこのオプションを選択します。|
|選択されていないノードをすべて選択します。|選択したノードのショートカット メニューを開きます。 **[選択]** 、 **[選択範囲の切り替え]** の順に選択します。|
|選択したノードにリンクしている追加のノードを選択します。|選択したノードのショートカット メニューを開きます。 **[選択]** を選択し、次のいずれかを実行します。<br /><br /> - 選択したノードに直接リンクしている追加のノードを選択するには、 **[出力方向の依存関係]** を選択します。<br />- 選択したノードから直接リンクしている追加のノードを選択するには、 **[出力方向の依存関係]** を選択します。<br />- 選択したノードとの間で直接リンクしている追加のノードを選択するには、 **[両方]** を選択します。<br />- 選択したノードとの間でリンクしているすべてのノードを選択するには、 **[接続しているサブグラフ]** を選択します。<br />- 選択したノードのすべての子を選択するには、 **[子 (複数)]** を選択します。|

## <a name="filter-nodes-and-links"></a><a name="FilterNodes"></a> ノードとリンクのフィルター処理

|**To**|**実行する手順**|
|-|-|
|フィルター パネルを表示または非表示にします。|コード マップのツールバーの **[フィルター]** ボタンを選択します。 **[フィルター]** ウィンドウは既定では、**ソリューション エクスプローラー** でタブ付きページとして表示されます。|
|マップに表示されるノードの種類をフィルター処理します。|[フィルター] ウィンドウの **[コード要素]** 一覧で、チェック ボックスをオンまたはオフにします。|
|マップに表示されるリンクの種類をフィルター処理します。|[フィルター] ウィンドウの **[リレーションシップ]** 一覧で、チェック ボックスをオンまたはオフにします。|
|マップ上のテスト プロジェクト ノードを表示または非表示にします。|[フィルター] ウィンドウの **[その他]** 一覧で **[テスト資産]** チェック ボックスをオンまたはオフにします。|

マップの [凡例] パネルに表示されるアイコンには、一覧の設定が反映されます。 [凡例] パネルを表示または非表示にするには、コード マップのツールバーの **[凡例]** ボタンをクリックします。

## <a name="examine-nodes-and-links"></a><a name="Inspect"></a> ノードとリンクの確認

コード マップには以下の種類のリンクが表示されます。

- 個々のリンクは、2 つのノード間の 1 つの関係を表します。

- グループ間リンクは、異なるグループの 2 つのノード間の 1 つの関係を表します。

- 集約リンクは、2 つのグループ間で同じ方向を指すすべての関係を表します。

> [!TIP]
> 既定では、マップには選択したノードのグループ間リンクのみが表示されます。 この動作を変更して、グループ間の集約リンクを表示または非表示にするには、コード マップのツールバーの **[レイアウト]** をクリックして、 **[詳細設定]** を選択し、 **[すべてのグループ間リンクを表示]** または **[すべてのグループ間リンクを非表示]** を選択します。 詳細については、「[ノードやリンクの表示と非表示を切り替える](#HidingShowing)」を参照してください。

|**To**|**実行する手順**|
|-|-|
|ノードまたはリンクの詳細を参照します。|マウス ポインターをノードまたはリンクの上に移動して、ツールヒントを表示します。<br /><br /> 集約されたリンクのツールヒントには、そのリンクが表す個々の依存関係が一覧表示されます。<br /><br /> または<br /><br /> ノードまたはリンクのショートカット メニューを開きます。 **[編集]** 、 **[プロパティ]** の順に選択します。|
|グループの内容を表示または非表示にします。|- グループを展開するには、ノードのショートカット メニューを開いて、 **[グループ]** 、 **[展開]** の順に選択します。<br />     または<br />     マウス ポインターをノード上に移動して、シェブロン (下向き矢印) ボタンを表示します。 このボタンをクリックすると、グループが展開されます。 キーボード: 選択したグループを展開するか折りたたむには、**正符号** キー ( **+** ) または **負符号** キー ( **-** ) を押します。<br />- グループを折りたたむには、ノードのショートカット メニューを開いて、 **[グループ]** 、 **[折りたたみ]** の順に選択します。<br />     または<br />     マウス ポインターをグループ上に移動して、シェブロン (上向き矢印) ボタンを表示します。 このボタンをクリックすると、グループが折りたたまれます。<br />- すべてのグループを展開するには、**Ctrl** + **A** キーを押して、すべてのノードを選択します。 マップのショートカット メニューを開いて、 **[グループ]** 、 **[展開]** の順に選択します。 **注:** すべてのグループを展開することで使用できないマップやメモリの問題が発生する場合、このコマンドは使用できません。 必要な詳細レベルにのみマップを展開することをお勧めします。<br />- すべてのグループを折りたたむには、ノードまたはマップのショートカット メニューを開きます。 **[グループ]** 、 **[すべて折りたたみ]** の順に選択します。|
|名前空間、型、またはメンバーのコード定義を確認します。|ノードのショートカット メニューを開き、 **[定義へ移動]** を選択します。<br /><br /> または<br /><br /> ノードをダブルクリックします。 展開したグループの場合、そのグループのヘッダーをダブルクリックします。<br /><br /> または<br /><br /> ノードを選択して、**F12** キーを押します。<br /><br /> 次に例を示します。<br /><br /> - 1 つのクラスを含んでいる名前空間の場合、クラスのコード ファイルが開き、そのクラスの定義が表示されます。 その他の場合、 **[シンボルの検索結果]** ウィンドウには、コード ファイルの一覧が表示されます。 **注:** Visual Basic 名前空間でこのタスクを実行すると、名前空間の背後にあるコード ファイルは開きません。 この問題は、Visual Basic 名前空間が含まれる選択したノードのグループでこのタスクを実行した場合にも発生します。 この問題を回避するには、手動で名前空間の背後にあるコード ファイルを参照するか、選択項目から名前空間のノードを除外します。<br />- クラスまたは部分クラスの場合、そのクラスのコード ファイルが開き、クラスの定義が表示されます。<br />- メソッドの場合、親クラスのコード ファイルが開き、メソッドの定義が表示されます。|
|集約リンクに参加する依存関係と項目を調べます。|関心あるリンクを選択し、選択した項目のショートカット メニューを開きます。 **[寄与するリンクの表示]** または **[新しいコード マップ上の寄与するリンクの表示]** を選択します。<br /><br /> Visual Studio で、リンクの両端にグループが展開され、リンクに参加する項目と依存関係のみが表示されます。 **注:** 部分的なグループの項目間の依存関係を調べる場合、次のような動作が発生することがあります。 <ul><li>調査に加わらない項目へのリンクは、存在している場合でも、マップに表示されなくなります。</li><li>部分的なグループの項目へのリンクを調べ、後で同じ項目への別のリンクを調べるとします。 この 2 番目の調査の際に、対象となる部分的なグループには、最初の調査の項目のみが表示されます。 最初の調査には加わらないで 2 番目の調査には加わったリンクとターゲット項目は、表示されません。</li></ul> グループから失われている項目を確認するには、 **[子の再フェッチ]** ![[子の再フェッチ] アイコン](../modeling/media/dependencygraph_deletednodesicon.png) を選択します (グループの一部のメンバーはマップに表示されないことが示されます)。 また、アクションを元に戻して (キーボード: **Ctrl+Z** キーを押します)、新しいマップで依存関係を調べることもできます。|
|異なるグループの複数ノード間の依存関係を調べます。|グループのすべての子が表示されるように、グループを展開します。 目的のすべてのノード (子を含む) を選択します。 マップに、選択したノード間のグループ間リンクが表示されます。<br /><br /> グループ内のノードをすべて選択するには、**Shift** キーとマウスの左ボタンを押したままの状態で、そのグループを囲む四角形を描画します。 マップ上のすべてのノードを選択するには、**Ctrl**+**A** キーを押します。 **ヒント:** 常にグループ間リンクを表示するには、マップのツールバーで **[レイアウト]** を選択し、 **[詳細設定]** 、 **[すべてのグループ間リンクを表示]** の順に選択します。|
|ノードまたはリンクの参照先の項目を確認する。|ノードのショートカット メニューを開き、 **[すべての参照を検索]** を選択します。 **注:** これは、マップの .dgml ファイルでノードまたはリンクに対して `Reference` 属性が設定されている場合にのみ適用されます。 ノードまたはリンクから項目に参照を追加するには、「[DGML ファイルを編集してコード マップをカスタマイズする](../modeling/customize-code-maps-by-editing-the-dgml-files.md)」を参照してください。|

## <a name="hide-or-show-nodes-and-links"></a><a name="HidingShowing"></a> ノードやリンクの表示と非表示を切り替える

ノードを非表示にすると、そのノードはレイアウト アルゴリズムに加わらないままになります。 既定では、グループ間リンクは非表示です。 グループ間リンクは、グループにまたがってノードを接続する個々のリンクです。 グループを折りたたむと、すべてのグループ間リンクが、グループ間の単一リンクにまとめられます。 グループを展開し、グループ内のノードを選択すると、グループ間リンクが表示されて、そのグループ内の依存関係が示されます。

> [!CAUTION]
> Visual Studio Enterprise で生成したマップを、Visual Studio Professional を使用するユーザーと共有する前に、他のユーザーが表示できるようにするノードやグループ間リンクを再表示しておく必要があります。 そうしない場合、これらのユーザーはそれらの項目を再表示できなくなります。

### <a name="to-hide-or-show-nodes"></a>ノードの表示/非表示を切り替えるには

|**To**|**実行する手順**|
|-|-|
|選択したノードを非表示にします。|1. 非表示にするノードを選択します。<br />2. 選択したノードまたはマップのショートカット メニューを開きます。 **[選択]** 、 **[選択範囲の非表示]** の順に選択します。|
|選択されていないノードを非表示にします。|1. 表示したままにしておくノードを選択します。<br />2. 選択したノードまたはマップのショートカット メニューを開きます。 **[選択]** 、 **[選択範囲以外を非表示]** の順に選択します。|
|非表示のノードを表示します。|- グループ内のすべての非表示のノードを表示するには、そのグループが展開されていることを最初に確認します。 ショートカット メニューを開き、 **[選択]** 、 **[子の再表示]** の順に選択します。<br />     または<br />     グループの左上隅の **[子の再表示]** ![[子の再表示] アイコン](../modeling/media/dependencygraph_filtericon_hiddennodes.gif) アイコンをクリックします (これは、非表示状態の子ノードがある場合にのみ表示されます)。<br />- 非表示状態のノードをすべて表示するには、マップまたはノードのショートカット メニューを開き、 **[選択]** 、 **[すべて再表示]** の順に選択します。|

### <a name="to-hide-or-show-links"></a>リンクの表示/非表示を切り替えるには

|**To**|**マップのツールバーで、[レイアウト]、[詳細設定] の順にクリックします。**|
|-|-|
|グループ間リンクを常時表示します。|**[すべてのグループ間リンクを表示]** 。 これにより、グループ間の集約されたリンクは非表示になります。|
|グループ間リンクを常時非表示にします。|**[すべてのグループ間リンクを非表示]**|
|選択したノードのグループ間リンクのみを表示します。|**[選択したノードのグループ間リンクを表示]**|
|すべてのリンクを非表示にします。|**[すべてのリンクを非表示]** 。 リンクを再び表示するには、上記のオプションのいずれかを選択します。|

## <a name="group-nodes"></a><a name="OrganizeGroups"></a> グループ ノード

|**To**|**実行する手順**|
|-|-|
|コンテナー ノードをグループ ノードまたはリーフ ノードとして表示します。|コンテナー ノードをリーフ ノードとして表示するには: ノードを選択して、選択した項目のショートカット メニューを開き、 **[グループ]** 、 **[リーフに変換]** の順に選択します。<br /><br /> コンテナー ノードをグループ ノードとして表示するには: ノードを選択して、選択した項目のショートカット メニューを開き、 **[グループ]** 、 **[グループに変換]** の順に選択します。|
|グループ内のレイアウトを変更します。|グループを選択して、ショートカット メニューを開き、 **[レイアウト]** を選択して、目的のレイアウト スタイルを選択します。<br /><br /> または<br /><br /> 1. グループを選択し、それが展開されていることを確認します。<br />2. グループ ヘッダーをもう一度クリックすると、グループ ツールバーが表示されます。<br />     ![依存関係のグラフ &#45; グループ ツールバー](../modeling/media/dependencygraph_group.png)<br />3. **[グループのレイアウト スタイルを変更]** 一覧 ![依存関係のグラフ &#45; グループ ツールバー &#45; レイアウト](../modeling/media/dependencygraph_grouptoolbar.gif) を開き、目的のレイアウト スタイルを選択します。<br /><br /> **[リスト ビュー]** によって、グループのメンバーが一覧に再配置されます。 **[グラフの既定の設定]** によって、グループのレイアウトがマップの既定のレイアウトにリセットされます。 その他のオプションについては、「[マップ レイアウトの変更](#Selecting)」を参照してください。|
|ノードをグループに追加します。|ノードをグループにドラッグします。<br /><br /> ノードをドラッグするときに、Visual Studio では、ノードを移動していることを示すインジケーターが表示されます。<br /><br /> ノードをグループ外にドラッグすることもできます。|
|ノードをグループ ノード以外に追加します。|ノードを目的のノードにドラッグします。 ノードをグループに追加することで、ターゲット ノードをグループに変換することもできます。|
|選択したノードをグループ化します。|1. グループ化するノードを選択します。 選択した最後のノードの上に、ポップアップ ツールバーが表示されます。<br />     ![依存関係のグラフ ツール バー](../modeling/media/depedencygraph_toolbar.png)<br />2. ツールバーで、4 番目のアイコン **[選択したノードをグループ化します]** を選択します (ノードが展開されている場合は、4 つではなく、5 つのアイコンが表示されます)。 新しいグループの名前を入力して、**Return** キーを押します。<br />     または<br />     グループ化するノードを選択して、選択した項目のショートカット メニューを開きます。 **[グループ]** 、 **[親グループの追加]** の順に選択して、新しいグループの名前を入力し、**Return** キーを押します。<br /><br /> グループ名は変更できます。 グループのショートカット メニューを開き、 **[編集]** 、 **[プロパティ]** の順に選択して、[Visual Studio プロパティ] ウィンドウを開きます。 必要に応じて、 **[ラベル]** プロパティでグループの名前を変更します。|
|グループを削除します。|削除する対象の 1 つまたは複数のグループを選択します。 選択した項目のショートカット メニューを開き、 **[グループ]** 、 **[グループの削除]** の順に選択します。|
|親グループからノードを削除します。|移動するノードを選択します。 選択した項目のショートカット メニューを開き、 **[グループ]** 、 **[親から削除]** の順に選択します。 これにより、祖父母グループまでのノード、または祖父母グループがない場合はグループの外側までのノードが削除されます。<br /><br /> または<br /><br /> ノードを選択し、グループからドラッグして外します。|

## <a name="add-remove-or-rename-nodes-links-and-comments"></a><a name="AddRemoveNodesLinks"></a> ノード、リンク、コメントの追加、削除、または名前の変更を行う

マップに表示される項目の数を増減させることで、マップをドリル ダウンしたり単純化したりすることができます。 また、アイテムの名前を変更したり、項目にコメントを追加することもできます。

> [!CAUTION]
> Visual Studio Ultimate を使用して作成したマップを、Visual Studio Professional を使用するユーザーと共有する場合、他のユーザーが表示できるようにするノードは、前もってマップに表示可能に設定しておく必要があります。 そうしない場合、これらのユーザーは削除されたコード要素を取得できなくなります。

### <a name="add-a-node-for-a-code-element"></a>コード要素に対するノードの追加

|**To**|**実行する手順**|
|-|-|
|現在のマウス ポインターの位置に、新しいジェネリック ノードを追加します。|1. 新しいコード要素を配置する、マップ上の場所にマウス ポインターを移動して、**Insert** キーを押します。<br />     または<br />     マップのショートカット メニューを開いて、 **[編集]** 、 **[追加]** 、 **[ジェネリック ノード]** の順に選択します。<br />2. 新しいノードの名前を入力して、**Return** キーを押します。|
|現在のマウス ポインターの位置に、特定の種類のコード要素ノードを追加します。|1. 新しいコード要素を配置する、マップ上の場所にマウス ポインターを移動して、マップのショートカット メニューを開きます。<br />2. **[編集]** 、 **[追加]** の順に選択して、目的のノードの種類を選択します。<br />3. 新しいノードの名前を入力して、**Return** キーを押します。|
|ジェネリック型または特定の型のコード要素ノードをグループに追加します。|1. グループ ノードを選択して、ショートカット メニューを開きます。<br />2. **[編集]** 、 **[追加]** の順に選択して、目的のノードの種類を選択します。<br />3. 新しいノードの名前を入力して、**Return** キーを押します。|
|既存のノードと同じ種類のノードを追加し、既存のノードからリンクを追加します。|1. コード要素を選択します。 その上にポップアップ ツールバーが表示されます。<br />     ![依存関係のグラフ ツール バー](../modeling/media/depedencygraph_toolbar.png)<br />2. ツールバーの 2 番目のアイコンである **[このノードと同じカテゴリの新しいノードを作成し、そのノードへのリンクを新しく追加します]** を選択します。<br />3. 新しいコード要素を配置するマップ上の場所を選択して、マウスの左ボタンをクリックします。<br />4. 新しいノードの名前を入力して、**Return** キーを押します。|
|フォーカスがある既存のコード要素からリンクされている、新しいジェネリック ノードを追加します。|1. キーボードを使って、リンク元のコード要素がフォーカスされる (点線で表示された四角形) まで、**Tab** キーを押します。<br />2. **Alt**+**Insert** キーを押します。<br />3. 新しいノードの名前を入力して、**Return** キーを押します。|
|フォーカスのある既存のコード要素からリンクされている、新しいジェネリック ノードを追加します。|1. キーボードを使って、リンク先のコード要素がフォーカスされる (点線で表示された四角形) まで、**Tab** キーを押します。<br />2. **Alt**+**Shift**+**Insert** キーを押します。<br />3. 新しいノードの名前を入力して、**Return** キーを押します。|

|**コード要素を追加するには**|**実行する手順**|
|-|-|
|ソリューション内のコード要素。|1. **ソリューション エクスプローラー** でコード要素を検索します。 **ソリューション エクスプローラー** の検索ボックスを使用するか、ソリューションを参照します。 **ヒント:** 型またはメンバーの依存関係があるコード要素を見つけるには、**ソリューション エクスプローラー** で型またはメンバーのショートカット メニューを開きます。 目的の関係を選択します。 **ソリューション エクスプローラー** には、指定した依存関係のあるコード要素のみが表示されます。<br />2. マップ画面に目的のコード要素をドラッグします。 クラス ビューまたはオブジェクト ブラウザーからコード要素をドラッグすることもできます。<br />     または<br />     **ソリューション エクスプローラー** で、マップするコード要素を選択します。 次に、**ソリューション エクスプローラー** のツールバーで、 **[コード マップに表示]** をクリックします。<br /><br /> 既定では、新しいコード要素の親コンテナーの階層がマップに表示されます。 コード マップのツールバーの **[親を含める]** ボタンを使って、この動作を変更します。 オフにすると、コード要素だけがマップに追加されます。 1 回のドラッグ アンド ドロップ アクションに対してだけ、この動作を反転させるには、**Ctrl** キーを押しながら、コード要素をマップにドラッグします。<br /><br /> Visual Studio は、選択項目の中の最上位レベルのコード項目に対してコード要素を追加します。 コード要素にその他のコード要素が含まれているかどうかを確認するには、コード要素にマウス ポインターを移動して、シェブロン (下向き矢印) を表示します。 シェブロンをクリックして、コード要素を展開します。 すべてのコード要素を展開するには、**Ctrl**+**A** キーを押してすべての要素を選択し、マップのショートカット メニューを開いて、 **[グループ]** 、 **[展開]** の順に選択します。 すべてのグループを展開することで、使用できないマップの問題やメモリ不足の問題が発生する場合、このコマンドは使用できません。|
|マップにコード要素に関連するコード要素を表示します。|コード マップのツールバーの **[関連項目の表示]** ボタンをクリックし、関心ある関連項目の種類を選択します。<br /><br /> または<br /><br /> コード要素のショートカット メニューを開きます。 関心あるリレーションシップの種類に応じて、メニューの **[表示...]** 項目のいずれかを選択します。 たとえば、現在の項目が参照している項目、現在の項目を参照する項目、クラスの基本と派生型、メソッドの呼び出し元、および含んでいるクラス、名前空間、アセンブリなどを確認できます。<br /><br /> 詳細については、[このトピック](../modeling/map-dependencies-across-your-solutions.md)を参照してください。|
|コンパイルされた .NET アセンブリ (.dll または .exe) またはバイナリ。|Visual Studio の外部から、アセンブリまたはバイナリをマップにドラッグします。<br /><br /> エクスプローラーからドラッグできるのは、エクスプローラーと Visual Studio を同じユーザー アクセス制御 (UAC: User Access Control) アクセス許可レベルで実行している場合のみです。 たとえば、UAC がオンになっていて、Visual Studio を管理者として実行している場合、Windows エクスプローラーまたはファイル エクスプローラーはドラッグ操作をブロックします。|

### <a name="AddNodes"></a>

#### <a name="add-a-link-between-existing-code-elements"></a>既存のコード要素間にリンクを追加する

1. ソース コード要素を選択します。 コード要素の上にツールバーが表示されます。

    ![依存関係のグラフ ツール バー](../modeling/media/depedencygraph_toolbar.png)

2. ツールバーの最初のアイコンである **[このノードから次にクリックするノードへのリンクを新しく作成します]** をクリックします。

3. 対象のコード要素をクリックします。 2 つのコード要素間にリンクが表示されます。

**OR**

1. マップ上でソース コード要素を選択します。

2. マウスがインストールされている場合、マップの範囲外に、マウス ポインターを移動します。

3. コード要素のショートカット メニューを開き、 **[編集]**  >  **[追加]**  >  **[一般的なリンク]** の順に選択します。

4. Tab キーを押して、リンクのターゲット コード要素を選択します。

5. **Enter** キーを押します。

### <a name="AddComments"></a>

#### <a name="add-a-comment-to-an-existing-node-on-the-map"></a>マップ上の既存のノードにコメントを追加する

1. コード要素を選択します。 その上にツールバーが表示されます。

     ![依存関係のグラフ ツール バー](../modeling/media/depedencygraph_toolbar.png)

2. ツールバーの 3 番目のアイコンである **[新しいコメント ノードと選択したノードへの新しいリンクを作成します]** を選択します。

     \- または

     コード要素のショートカット メニューを開き、 **[編集]**  >  **[新しいコメント]** の順に選択します。

3. コメントを入力します。 新しい行に入力するには、**Shift** + **Enter** キーを押します。

#### <a name="add-a-comment-to-the-map-itself"></a>マップ自体にコメントを追加する

1. マップのショートカット メニューを開き、 **[編集]**  >  **[新しいコメント]** の順に選択します。

2. コメントを入力します。 新しい行に入力するには、**Shift** + **Enter** キーを押します。

### <a name="RenameNodes"></a>

#### <a name="rename-a-code-element-or-link"></a>コード要素またはリンク名を変更する

1. 名前を変更するコード要素またはリンクを選択します。

2. **F2** キーを押すか、ショートカット メニューを開いて、 **[編集]**  >  **[名前の変更]** の順に選択します。

3. マップで編集ボックスが表示されたら、コード要素またはリンクの名前を変更します。

**OR**

1. ショートカット メニューを開いて、 **[編集]**  >  **[プロパティ]** の順に選択します。

2. Visual Studio の [プロパティ] ウィンドウで、 **[ラベル]** プロパティを編集します。

#### <a name="remove-a-code-element-or-link-from-the-map"></a>マップからコード要素またはリンクを削除します。

1. コード要素またはリンクを選択して、**Delete** キーを押します。

     \- または

     コード要素またはリンクのショートカット メニューを開き、 **[編集]**  >  **[削除]** の順に選択します。

2. 要素またはリンクがグループに含まれている場合、 **[子の再フェッチ]** ボタン ![[子の再フェッチ] アイコン](../modeling/media/dependencygraph_deletednodesicon.png) がグループ内に表示されます。 このボタンをクリックすると、足りない要素とリンクが再フェッチされます。

- 基本コードに影響を与えずに、マップからコード要素を削除できます。 コード要素を削除すると、その定義は、DGML (.dgml) ファイルから削除されます。

- DGML を編集したり、未定義のコード要素を追加したり、旧バージョンの Visual Studio を使用したりして作成したマップは、この機能をサポートしません。

#### <a name="flag-a-code-element-for-follow-up"></a>フォロー アップ用にコード要素にフラグを設定する

1. フォローアップ用にフラグを設定するコード要素またはリンクを選択します。

2. ショートカット メニューを開いて、 **[編集]**  >  **[フォローアップ用にフラグを設定]** の順に選択します。

- 既定では、コード要素は赤の背景色で表示されます。 適切なフォローアップ情報を使って、[コメントを追加](#AddComments)することを検討してください。

- **[編集]**  >  **[その他のフラグの色]** の順に選択することで、要素の背景色を変更したり、フォローアップ フラグをクリアしたりすることができます。

## <a name="change-the-style-of-a-code-element-or-link"></a><a name="ChangeStyleCodeOrLink"></a> コード要素またはリンクのスタイルを変更する

事前定義されたアイコンと色を使って、コード要素のアイコン、およびコード要素とリンクの色を変更できます。 たとえば、色を選択することで、特定のカテゴリまたは特定のプロパティを持つコード要素およびリンクを強調して表示できます。 これにより、マップの特定の領域を識別し、目立たせることができます。 マップの .dgml ファイルを編集して、カスタム アイコンと色を指定できます。「[DGML ファイルを編集してコード マップをカスタマイズする](../modeling/customize-code-maps-by-editing-the-dgml-files.md)」を参照してください。

### <a name="to-apply-a-predefined-color-or-icon-to-code-elements-or-links-with-a-certain-category-or-property"></a>特定のカテゴリまたは特定のプロパティを持つコード要素やリンクに定義済みの色またはアイコンを適用するには

1. マップのツールバーで **[凡例]** を選択します。

2. **[凡例]** ボックスで、コード要素カテゴリまたはプロパティが一覧に既に表示されているかどうかを確認します。

3. 一覧にカテゴリまたはプロパティが含まれていない場合は、 **[凡例]** ボックスの [ **+** ] を選択し、**ノード プロパティ]** [、]**ノード カテゴリ**[、]**リンク プロパティ**[、または ] **[リンク カテゴリ** を選択します。 次に、プロパティまたはカテゴリを選択します。 カテゴリまたはプロパティが **[凡例]** ボックスに表示されるようになります。

    > [!NOTE]
    > カテゴリまたはプロパティを作成し、コード要素に割り当てるには、マップの .dgml ファイルを編集します。「[DGML ファイルを編集してコード マップをカスタマイズする](../modeling/customize-code-maps-by-editing-the-dgml-files.md)」を参照してください。

4. **[凡例]** ボックスで、追加したか変更するカテゴリまたはプロパティの隣のアイコンをクリックします。

5. 次の表を使用して、変更するスタイルを選択します。

    |**次を変更するには**|**Choose**|
    |-|-|
    |背景の色|**バックグラウンド**|
    |輪郭の色|**ストローク**|
    |テキストの色 (結果を示すため、文字 "f" が表示されます)|**前景**|
    |アイコン|**アイコン**|

     色またはアイコンを選択できるように、 **[カラー セット ピッカー]** または **[アイコン セット ピッカー]** ダイアログ ボックスが表示されます。

6. **[カラー セット ピッカー]** または **[アイコン セット ピッカー]** ダイアログ ボックスで、次のいずれかを実行します。

    |**適用対象**|**実行する手順**|
    |-|-|
    |色またはアイコンのセット|**[カラー設定** **の選択]** (または **アイコン**) 一覧を開きます。 色またはアイコンのセットを選択します。|
    |特定の色またはアイコン|カテゴリまたはプロパティ値のリストを開きます。 色またはアイコンを選択します。|

    > [!NOTE]
    > **[凡例]** ボックス内のスタイルを、再整列、削除、または一時的に無効化できます。 「[[凡例] ボックスの編集](#ModifyLegend)」を参照してください。

## <a name="edit-the-legend-box"></a><a name="ModifyLegend"></a> [凡例] ボックスの編集

**[凡例]** ボックス内のスタイルを、次のように再整列、削除、または一時的に無効化できます。

1. **[凡例]** ボックスのスタイルのショートカット メニューを開きます。

2. 次のいずれかのタスクを実行します。

    |**To**|**Choose**|
    |-|-|
    |コード要素の無効化|**無効化**|
    |コード要素の削除|**削除**|
    |アイテムを上へ移動する|**[上へ移動]**|
    |コード要素を下へ移動|**[下へ移動]**|

## <a name="copy-styles-from-one-map-to-another"></a><a name="CopyLegend"></a> 一方のマップから他方のマップにスタイルをコピーする

1. **[凡例]** ボックスがソース マップに表示されることを確認します。 これが表示されていない場合は、マップのツールバーで **[凡例]** をクリックします。

2. **[凡例]** ボックスのショートカット メニューを開きます。 **[凡例のコピー]** を選択します。

3. ターゲット マップに凡例を貼り付けます。

## <a name="merge-code-maps"></a><a name="MergeMaps"></a> コード マップのマージ

マップ間でコード要素をコピーして貼り付けることで、マップをマージできます。 コード要素の識別子が一致する場合、コード要素の貼り付けはマージ操作と同様に機能します。 このタスクを簡単にするためには、視覚化するすべてのアセンブリとバイナリを同じフォルダー内に配置することで、各アセンブリまたはバイナリの完全パスが、マージする各マップに対して同じになるようにします。

また、それらのアセンブリやバイナリをドラッグして、そのフォルダーから同じマップへドラッグすることもできます。

## <a name="see-also"></a>関連項目

- [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)
- [コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)
- [コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [DGML ファイルを編集してコード マップをカスタマイズする](../modeling/customize-code-maps-by-editing-the-dgml-files.md)
- [Directed Graph Markup Language (DGML) リファレンス](../modeling/directed-graph-markup-language-dgml-reference.md)
