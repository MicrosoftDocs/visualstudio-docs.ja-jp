---
title: コマンドの設計 | Microsoft Docs
description: Visual Studio で VSPackage のコマンドを設計する方法について説明します。 表示される場所を指定する方法、使用できるタイミング、処理する方法を含みます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands
- commands, implementation
ms.assetid: 097108c3-f758-4b87-89d6-b32d12d9041a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0acef6dd38238ef58f1dd66f7d8de35318e4ffc6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078930"
---
# <a name="command-design"></a>コマンドの設計
VSPackage にコマンドを追加するときは、表示される場所、使用できるタイミング、処理する方法を指定する必要があります。

## <a name="define-commands"></a>コマンドを定義する
 新しいコマンドを定義するには、VSPackage プロジェクトに Visual Studio コマンド テーブル ( *.vsct*) ファイルを含めます。 Visual Studio パッケージ テンプレートを使用して VSPackage を作成した場合は、プロジェクトにこれらのファイルのいずれかが含まれています。 詳細については、「[Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)」を参照してください。

 Visual Studio では、見つかったすべての *.vsct* ファイルをマージして、コマンドを表示できるようにします。 これらのファイルは VSPackage のバイナリとは異なるため、Visual Studio では、コマンドを見つけるためにパッケージを読み込む必要はありません。 詳細については、「[VSPackages でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。

 Visual Studio では、<xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> 登録属性を使用して、メニューのリソースとコマンドを定義します。 詳細については、「[コマンドの実装](../../extensibility/internals/command-implementation.md)」を参照してください。

 コマンドは、実行時にさまざまな方法で変更できます。 表示または非表示にしたり、有効または無効にしたりすることができます。 異なるテキストやアイコンを表示したり、異なる値を含めたりすることができます。 Visual Studio によって VSPackage が読み込まれる前に、多くのカスタマイズを実行できます。 詳細については、「[VSPackages でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。

## <a name="command-handlers"></a>コマンド ハンドラー
 コマンドを作成する場合は、コマンドを実行するためのイベント ハンドラーを指定する必要があります。 ユーザーがコマンドを選択すると、適切にルーティングされる必要があります。 コマンドのルーティングとは、正しい VSPackage に送信して、有効または無効にしたり、表示または非表示にしたり、ユーザーが選択した場合に実行したりすることを意味します。 詳細については、「[コマンド ルーティング アルゴリズム](../../extensibility/internals/command-routing-algorithm.md)」を参照してください。

## <a name="visual-studio-command-environment"></a>Visual Studio でのコマンドの環境
 Visual Studio では、任意の数の VSPackage をホストして、それぞれで独自のコマンド セットが提供されるようにすることができます。 環境には、現在のタスクに適したコマンドのみが表示されます。 詳細については、「[コマンドの可用性](../../extensibility/internals/command-availability.md)」および[選択コンテキスト オブジェクト](../../extensibility/internals/selection-context-objects.md)に関する記事を参照してください。

 新しいコマンド、メニュー、ツール バー、またはショートカット メニューを定義する VSPackage では、ネイティブ アセンブリまたはマネージド アセンブリ内のリソースを参照するレジストリ エントリを通じて、インストール時に、そのコマンド情報が Visual Studio に提供されます。 その後、各リソースによってバイナリ データ リソース ( *.cto*) ファイルが参照されます。これは、Visual Studio のコマンド テーブル ( *.vsct*) ファイルをコンパイルするときに生成されます。 これにより、インストールされているすべての VSPackage を読み込むことなく、マージされたコマンド セット、メニュー、ツール バーを Visual Studio で提供できるようになります。

### <a name="command-organization"></a>コマンドの編成
 環境では、コマンドがグループ、優先順位、メニューによって配置されます。

- グループは、**切り取り**、**コピー**、**貼り付け** のコマンド グループなど、関連するコマンドの論理的なコレクションです。 グループは、メニューに表示されるコマンドです。

- 優先順位によって、グループ内の個々のコマンドがメニューに表示される順序が決定されます。

- メニューは、グループのコンテナーとして機能します。

  環境では、一部のコマンド、グループ、メニューが事前定義されます。 詳細については、「[既定のコマンド、グループ、およびツール バーの配置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)」を参照してください。

  コマンドは、プライマリ グループに割り当てることができます。 プライマリ グループでは、メイン メニューの構造と **[カスタマイズ]** ダイアログ ボックスでコマンドの位置を制御します。 コマンドは複数のグループに表示できます。たとえば、コマンドをメイン メニュー、ショートカット メニュー、ツール バー上に配置できます。 詳細については、「[VSPackages でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)」を参照してください。

### <a name="command-routing"></a>コマンド ルーティング
 VSPackage のコマンドの呼び出しとルーティングの処理は、オブジェクト インスタンスでメソッドを呼び出すプロセスとは異なります。

 環境では、最も内側の (ローカル) コマンド コンテキスト (現在の選択に基づく) から最も外側の (グローバルな) コンテキストに、コマンドが順次ルーティングされます。 コマンドを実行できる最初のコンテキストが、コマンドが処理されるコンテキストです。 詳細については、「[コマンド ルーティング アルゴリズム](../../extensibility/internals/command-routing-algorithm.md)」を参照してください。

 ほとんどの場合、環境では <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを使用してコマンドを処理します。 コマンド ルーティング スキームでは、さまざまなオブジェクトでコマンドを処理できるため、任意の数のオブジェクトで <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> を実装できます。これには、Microsoft ActiveX コントロール、ウィンドウ ビューの実装、ドキュメント オブジェクト、プロジェクト階層、VSPackage オブジェクト自体 (グローバル コマンドの場合) が含まれます。 階層でのコマンドのルーティングなど、一部の特殊なケースでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> インターフェイスを実装する必要があります。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[コマンドの実装](../../extensibility/internals/command-implementation.md)|VSPackage でコマンドを実装する方法について説明します。|
|[コマンドの可用性](../../extensibility/internals/command-availability.md)|Visual Studio のコンテキストで使用可能なコマンドを判断する方法について説明します。|
|[コマンド ルーティング アルゴリズム](../../extensibility/internals/command-routing-algorithm.md)|Visual Studio のコマンド ルーティング アーキテクチャによってさまざまな VSPackage でコマンドを処理できるようになる仕組みについて説明します。|
|[コマンド配置のガイドライン](../../extensibility/internals/command-placement-guidelines.md)|Visual Studio 環境でコマンドを配置する方法について説明します。|
|[VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)|VSPackage で Visual Studio のコマンド アーキテクチャを最大限に活用する方法について説明します。|
|[既定のコマンド、グループ、およびツール バーの配置](../../extensibility/internals/default-command-group-and-toolbar-placement.md)|VSPackage で Visual Studio に含まれているコマンドを最適に使用する方法について説明します。|
|[VSPackage を管理する](../../extensibility/managing-vspackages.md)|Visual Studio で VSPackage を読み込む方法について説明します。|
|[Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)|VSPackage でコマンドのレイアウトと外観を記述するために使用される XML ベースの *.vsct* ファイルに関する情報を提供します。|
