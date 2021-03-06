---
title: Visual Studio SDK の用語集 | Microsoft Docs
description: この用語集では、Visual Studio SDK のドキュメントで使用される用語の定義について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- glossary [Visual Studio SDK]
ms.assetid: b64d432b-c39b-4904-ad18-3c3218b6e3aa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 49e91a64220882eea196819a1860052dc871bec4
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905424"
---
# <a name="visual-studio-sdk-glossary"></a>Visual Studio SDK の用語集
この用語集では、[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] のドキュメントで使用される用語の定義について説明します。

## <a name="terms"></a>用語
 アドイン: プライマリ アプリケーションに追加されたユーティリティ アプリケーション、ドライバー、またはその他のソフトウェア。 Visual Studio 統合開発環境 (IDE) では、アドインは IDE の機能を拡張するオートメーションベースのアプリケーションです。

 オートメーション モデル: オートメーション モデル (以前のバージョンの Visual Studio では、拡張モデルとして知られていました) は、IDE を駆動する基盤となるルーチンへのアクセスを可能にするプログラミング インターフェイスです。 アドイン、ウィザード、およびマクロは、オートメーション モデルのオブジェクトを使用して、IDE の機能を制御または拡張します。

 コマンド UI コンテキスト: UI コマンドまたは要素 (ツール バーなど) の表示との GUID の関連付け。 コマンド UI コンテキストは、ウィンドウにアタッチされていないので、選択コンテキストとは異なります。

 コマンド UI コンテキストは、次の場合に使用できます。

- 特定のウィンドウがアクティブになったときに表示されるツール バーに GUID を割り当てる。

- VSPackage を読み込んだり実行したりすることなく、コマンドの可用性に GUID を割り当てる。

- アクティブなキー バインドに影響を与える GUID を割り当てる。

- マクロの記録を有効にする GUID を割り当てる。

- デバッグ モードをアクティブ化したり、エディターでデザイン モードと実行モードを切り替えたりするために、GUID を割り当てる。

  コンポーネント: アプリケーションの機能の一部を構成するソフトウェアの一部。そのアプリケーションにソフトウェアの実装に関する既存の情報はありません。 コンポーネントとアプリケーションの間の通信は、OLE スタイルのインターフェイスを介してのみ行われます。

  コンポーネント マネージャー: サービス `SOleComponentManager`。最上位のコンポーネントに対して非ユーザー インターフェイスの調整サービスを提供します。 `SOleComponentManager` サービスは、`IOleComponentManager` インターフェイスを実装します。

  コンポーネント UI マネージャー: サービス `SOleComponentUIManager`。ユーザー インターフェイスの調整サービスを提供します。 `SOleComponentUIManager` サービスは、`IOleComponentUIManager` および `IOleInPlaceComponentUIManager` インターフェイスを実装します。

  コンテキスト バッグ: 環境コンポーネントにアタッチされた `IVsUserContext` オブジェクト (COM オブジェクト)。 このオブジェクトは、検索キーワード、**F1** キーワード、およびコンポーネントに関連する属性を保持します。 また、コンテキスト バッグは、リンクされている任意のサブコンテキスト バッグを指します。

  コンテキスト プロバイダー: 関連付けられているコンテキスト バッグを持つ IDE 内のコンポーネント。 このようなコンポーネントには、ツール ウィンドウ、エディター、またはプロジェクト階層が含まれます。

  デザイナー: UI (フォーム、ボタン、およびその他のコントロール) の要素をユーザーが操作できるプログラミング インターフェイス。

  DocData: ドキュメントとビューの分離が存在する環境での、ドキュメントの基になるデータをカプセル化する COM オブジェクト (たとえば、テキスト エディターの場合、これはすべてのテキスト エディター ビューの基になるテキスト バッファーになります)。 EditorFactory がこのオブジェクトを提供していない場合、IDE はその代わりになるものを作成します。 このオブジェクトの役割は、同じ `DocData` 上の複数のビューに対してデータの永続性と共有セマンティクスを管理することです。 `DocData` オブジェクトが `IOleCommandTarget` インターフェイスをサポートしている場合は、UIShell のコマンド ルーティングに含まれます。

  DocObject: ホストによって提供されるフレーム内で UI をホストするために使用されるテクノロジ。 具体的には、この用語は `IOleDocument` と関連するインターフェイスをサポートする埋め込みを指します。 このテクノロジには、COM ドキュメントの実装の詳細、Visual Basic 5.0 のツール ウィンドウ、Visual Basic 6.0 の ActiveX デザイナーなど、さまざまな潜在用途があります。

  ドキュメント: ドキュメント全体 (`DocData` と `DocView` の両方) を総称して呼ぶために使用されます。 たとえば、DocumentFrame には `DocView` が含まれていますが、`DocData` への参照を保持して永続性を扱うこともできます。

  DocView: ユーザーが基になる `DocData` を表示および操作するために使用する DocObject/Embedding/WindowPane。 ユーザーは、`DocObject` インターフェイス設計の一部であるドキュメント/ビューの分離を利用しません。 ユーザーは、`DocData` として知られている基になるデータの抽象的な概念 (あまり形式化されていない) を使用するのではなく、ビューとして機能する DocObject 全体を使用します。 `DocView` オブジェクトは、常に IDE のドキュメント フレーム オブジェクト (MDI 子ウィンドウ) と共に埋め込まれます。

  DTE: `DTE` (開発ツール機能拡張) オブジェクトは、Visual Studio オートメーション モデルの最上位のアクセス ポイントです。このオブジェクトを使用して、IDE をプログラムによって自動化したり拡張したりできます。

  ダイナミック ヘルプ ウィンドウ: IDE によって実装され、検索キーワードや **F1** ヘルプ トピックの一覧を表示するツール ウィンドウ。

  エディター: `DocView` を実装するコード (クラス、CLSID)。 また、ビューとデータの分離がサポートされている場合にも `DocData` を実装します。

  拡張機能: IDE に対して変更、カスタマイズ、または追加を行う機能。 オートメーション モデルまたは Vspackage を使用して拡張機能を作成します。

  外部エディター: Microsoft Word など、IDE に固有ではないエディター。 独自のメカニズムを使用して登録されており、IDE の外部で使用できます。 このエディターを埋め込むことができる場合は、IDE のウィンドウ内に表示されます。 埋め込むことができない場合は、別の最上位ウィンドウが作成されます。

  階層: ノードのツリー。各ノードは、一連のプロパティに関連付けられます。

  独立した最上位コンポーネント: モードレスの最上位ウィンドウを使用するコンポーネント。スタンドアロンのアプリケーション ウィンドウとして効果的に動作できますが、インプロセス オブジェクトとして実装されます。 そのため、独立した最上位コンポーネントでは、IDE でモダリティとメッセージ ループ サービスを調整する必要があります。 インプロセス オブジェクトには、独自のメッセージ ループはありません。

  情報プロバイダー: 情報プロバイダーは、キーワードを検索し、`IVsUserContextItem` オブジェクトの形式でトピックの一覧を返すことができるモジュールです。 情報プロバイダーに **F1** や検索キーワード項目を提供するには、システムにコンパイル済みヘルプ ファイル ( *.HxS*) を登録します。 これらのファイルのヘルプ トピックには、[ダイナミック ヘルプ] ウィンドウに表示されるトピックの一覧と、ユーザーが **F1** キーを押せるかどうかが表示されます。

  インプレース コンポーネント: IDE によって所有されるドキュメント ウィンドウ内に視覚的に含まれるウィンドウを管理するための `IOleInPlaceComponent` インターフェイスを実装する VSPackage オブジェクト。 インプレース コンポーネントは標準の OLE メニューの結合には加わりません。その代わりに、ユーザー インターフェイス要素を IDE と統合します。

  インプレース コンポーネントには、固定されたインプレース コンポーネントとコンポーネント コントロールの 2 種類があります。

  固定されたインプレース コンポーネントには、IDE に直接組み込まれているかのように思える、IDE のユーザー インターフェイスに強固に統合されたメニュー、ツールバー、コマンドがあります。

  コンポーネント コントロールには、IDE に統合された独自のユーザー インターフェイス要素はありません。代わりに、IDE のメニュー、コマンド、ツールバーを使用します。 たとえば、Bold コマンドを使用して、フォームに埋め込まれているリッチ テキスト コントロール内の選択された単語を太字にすることができます。 ただし、コンポーネント コントロールは、動的にインストールされたコンポーネント固有の UI 要素を表示するように要求できます。

  言語サービス: VSPackage 開発者が、テキストのマーキングや色分けなどのコンピューター言語コード エディターの機能を実装できるようにするオブジェクトのセット。

  その他のファイル プロジェクト: プロジェクトに含まれていないオープン ファイルを格納するために使用されるプロジェクト。 このプロジェクト内の項目の一覧は保存されません。

  プロジェクト: プロジェクトは、階層オブジェクト、または `IVsHierarchy` インターフェイスを実装する COM オブジェクトで構成されます。

  プロジェクト固有のデザイナーまたはエディター: プロジェクト タイプから独立させて使用できないデザイナー。 プロジェクト固有のすべてのデザイナーは、エディター ファクトリ情報をレジストリに入力する必要があります。 特定のプロジェクトで特定のファイルの種類が開かれるたびに、IDE がデザイナーをインスタンス化できるようになります。

  プロジェクト タイプ ウィンドウ: グローバル選択コンテキストから、現在アクティブなプロジェクト階層と項目を常に追跡するウィンドウ。 プロジェクト タイプのウィンドウでは、`SVsTrackSelectionEx` サービスを使用して、IDE に変更のアラートを通知したり、ユーザーにフィードバックを表示したりします。 ソリューション エクスプローラーは、プロジェクト タイプのウィンドウの一例です。

  プロパティ ウィンドウは、以前のプロパティ ブラウザーです。

  参照ベースのプロジェクト: プロジェクトのファイルを同じディレクトリに配置する必要がないプロジェクト。 代わりに、他の関連のないディレクトリからのファイルへの参照は、プロジェクト自体によって格納および管理されます。

  実行中のドキュメント テーブル: IDE で現在開いているすべてのドキュメントの一覧を維持する内部構造。 この一覧には、これらのドキュメントが現在編集中かどうかに関係なく、メモリ内の開いているすべてのドキュメントが含まれます。 ドキュメントとは、エディターで開かれたストアド プロシージャ、プロジェクト内のファイル、またはメイン プロジェクト ファイル (*.vcproj ファイルなど) を含む、保存されているアイテムのことです。

  選択コンテキスト: IDE 内のすべてのウィンドウの詳細に含まれ、アクティブな選択を追跡するために使用されるデータ。 選択コンテキストは次のもので構成されます。

- プロジェクト階層の `IVsHierarchy` インターフェイスへのポインター。

- プロジェクト項目の項目識別子。

- アクティブなオブジェクトのプロパティへのアクセスを提供する `ISelectionContainer` インターフェイスへのポインター。

- 要素値の配列。

  サービス: 単一の COM オブジェクト内に存在する一連の COM インターフェイスのコントラクト。 GUID によって識別されるサービスを作成する際に、サービスを実行する COM インターフェイスのセットを定義します。 COM オブジェクトは、サービスを使用して相互に通信します。

  ソリューション: ユーザーが作業する関連プロジェクトのグループ。

  標準デザイナー: プロジェクト タイプに関係なく使用できるデザイナー。 すべての標準デザイナーは、エディター ファクトリ情報をレジストリに入力する必要があります。 IDE は、特定の拡張子を持つファイルを開くたびに、デザイナーをインスタンス化できます。 データはファイルに保存する必要があります。

  標準エディター: 特定のプロジェクト タイプに依存せずに使用できるエディター。 このようなエディターでは、EditorFactories がレジストリに登録されています。 これにより、IDE がエディターを見つけて起動できます。

  標準 OS エディター: Visual Studio の固有ではない埋め込み。 既知の Win32 キーを使用して登録されます (たとえば、Win32 Explorer が起動方法を認識している場合)。 このようなエディターを埋め込むことができる場合、エディターは IDE の所定の場所に表示されます。 それ以外の場合は、このようなエディター用に別の最上位ウィンドウが作成されます。

  サブコンテキスト バッグ: コンテキスト バッグにリンクされた `IVsUserContext` オブジェクト。 オブジェクトは、IDE コンポーネント内の選択項目の検索キーワード、**F1** キーワード、および属性を保持します。 サブコンテキストの例として、ツール ウィンドウのコマンドや、エディターのキーワードがあります。

  タスク一覧: IDE によって実装され、アクティブなタスクの一覧を表示するツール ウィンドウ。

  テキスト バッファー: オブジェクト `VSTextBuffer` の共通名。

  テキスト ビュー: オブジェクト `VSTextView` の共通名。

  ツール最上位コンポーネント: モードレス ポップアップ ウィンドウとして動作するコンポーネント。IDE のユーザー インターフェイスと緊密に連携します。 独立した最上位コンポーネントと同様に、ツール最上位コンポーネントもモダリティとメッセージ ループ サービスを IDE で調整する必要があります。

  最上位コンポーネント: IDE ウィンドウのクライアント領域ではなく、モードレスの最上位ウィンドウを管理する VSPackage オブジェクト。 最上位コンポーネントは、アイドル時間へのアクセスのようなメッセージ ループ サービスを利用するための `IOleComponent` インターフェイスを実装します。

  UI アクティブ: 表示可能な現在フォーカスのある VSPackage オブジェクト。

  UI 階層: 階層の表示を可能にする、`IVsUIHierarchy` インターフェイスを実装する COM オブジェクト。 UI 階層ウィンドウは、プロパティ ウィンドウを更新するための `ISelectionContainer` インターフェイスを実装します。その他のプロジェクト タイプ ウィンドウは、必要に応じて、この実装を使用できます。

  VSCT: Visual Studio コマンド テーブル。 .vsct ファイルには、XML 形式のメニュー、ツールバー、およびコマンドの配置と動作に関する情報が含まれています。

  VSPackage: Visual Studio IDE を拡張するインストール可能なソフトウェアの構成要素。ユーザー インターフェイス、サービス、プロジェクト タイプ、エディター/デザイナーの 1 つ以上の項目に寄与します。 VSPackage は、`IVsPackage` インターフェイスを実装する COM オブジェクトと、選択やその他の機能をサポートする他のインターフェイスを実装する 1 つ以上のその他の COM オブジェクトで構成されます。 また、VSPackage には特定の登録要件があります。
