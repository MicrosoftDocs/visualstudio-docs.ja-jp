---
title: Visual Studio SDK の内部 | Microsoft Docs
description: Visual studio のアーキテクチャ、コンポーネント、サービス、スキーマ、ユーティリティなどの、Visual Studio SDK の拡張機能について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- roadmap, Visual Studio integration SDK
- Visual Studio integration SDK roadmap
- integration roadmap, Visual Studio SDK
ms.assetid: 9118eaa4-0453-4dc5-9e16-c7062d254869
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e11ee862f43ead3605d8e07dc159e18da13413b8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074705"
---
# <a name="inside-the-visual-studio-sdk"></a>Visual Studio SDK の内部

このセクションでは、Visual Studio のアーキテクチャ、コンポーネント、サービス、スキーマ、ユーティリティなどの Visual Studio の拡張機能に関する詳細な情報を提供します。

## <a name="extensibility-architecture"></a>機能拡張アーキテクチャ
 次の図は、Visual Studio の機能拡張のアーキテクチャを示しています。 VSPackage は、サービスとして IDE 全体で共有されるアプリケーション機能を提供します。 標準 IDE には、IDE ウィンドウ機能へのアクセスを提供する、<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> などのさまざまなサービスも用意されています。

 ![環境アーキテクチャ グラフィック](../../extensibility/internals/media/environment.gif "環境") Visual Studio アーキテクチャの一般的なビュー

## <a name="vspackages"></a>VSPackages
 VSPackage は、UI 要素、サービス、プロジェクト、エディター、およびデザイナーで Visual Studio を構成および拡張するソフトウェア モジュールです。 VSPackage は、Visual Studio の中心のアーキテクチャ単位です。 詳細については、「 [VSPackages](../../extensibility/internals/vspackages.md)」を参照してください。

## <a name="visual-studio-shell"></a>Visual Studio Shell
 Visual Studio Shell は、基本機能を提供し、コンポーネント VSPackage と MEF 拡張機能間の相互通信をサポートします。 詳細については、[Visual Studio Shell](../../extensibility/internals/visual-studio-shell.md) に関するページを参照してください。

## <a name="user-experience-guidelines"></a>ユーザー エクスペリエンス ガイドライン
 Visual Studio の新機能の設計を計画している場合は、「[Visual Studio ユーザー エクスペリエンス ガイドライン](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)」の設計と使用性のヒントに関するガイドラインを参照してください。

## <a name="commands"></a>コマンド
 コマンドは、ドキュメントの印刷、ビューの更新、ファイルの新規作成などのタスクを実行する関数です。

 Visual Studio を拡張すると、コマンドを作成して Visual Studio Shell に登録することができます。 これらのコマンドを IDE のメニューやツールバーなどにどのように表示するかを指定できます。 通常、カスタム コマンドは **[ツール]** メニューに表示され、ツール ウィンドウを表示するためのコマンドは、 **[表示]** メニューの **[その他のウィンドウ]** サブメニューに表示されます。

 コマンドを作成するときは、コマンド用のイベント ハンドラーも作成する必要があります。 イベント ハンドラーでは、コマンドをいつ表示または有効にするかを決定し、そのテキストを変更できるようにし、アクティブになったときにコマンドが適切に応答することを保証します。 ほとんどの場合、IDE では、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> インターフェイスを使用してコマンドを処理します。 Visual Studio ではコマンドは、ローカルの選択に基づいて最も内側のコマンド コンテキストから処理を開始し、グローバルの選択に基づいて最も外側のコンテキストに進みます。 メイン メニューに追加したコマンドは、すぐにスクリプトに利用できます。

 詳細については、「[コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。

## <a name="menus-and-toolbars"></a>メニューとツール バー
 メニューとツール バーは、ユーザーがコマンドを呼び出す手段を提供します。 メニューはコマンドの行または列であり、通常はツール ウィンドウの上部に個々のテキスト項目として表示されます。 サブメニューは 2 次メニューであり、ユーザーが小さな矢印を含むコマンドをクリックしたときに表示されます。 コンテキスト メニューは、ユーザーが特定の UI 要素を右クリックしたときに表示されます。 一般的なメニュー名には、 **[ファイル]** 、 **[編集]** 、 **[表示]** 、 **[ウィンドウ]** などがあります。 詳細については、「[メニューとコマンドの拡張](../../extensibility/extending-menus-and-commands.md)」を参照してください。

 ツール バーは、ボタンと他のコントロール (コンボ ボックス、リスト ボックス、テキスト ボックスなど) の行または列です。 ツール バーのボタンには、通常はアイコンのイメージがあります。 **[ファイルを開く]** コマンドの場合のフォルダー アイコンや、 **[印刷]** コマンドの場合のプリンターなどです。 すべてのツール バー要素は、コマンドに関連付けられています。 ツール バー ボタンをクリックすると、関連付けられているコマンドが実行されます。 ドロップダウン コントロールの場合は、ドロップダウン リスト内の各項目が異なるコマンドに関連付けられています。 Splitter コントロールなどの一部のツール バー コントロールは混合型です。 このコントロールの一方の側はツール バー ボタン、もう一方の側は、クリックしたときに複数のコマンドを表示する下矢印です。

## <a name="tool-windows"></a>ツール ウィンドウ
 ツール ウィンドウは、情報を表示するために IDE で使用されます。 "**ツールボックス**"、"**ソリューション エクスプローラー**"、 **[プロパティ]** ウィンドウ、および "**Web ブラウザー**" はツール ウィンドウの例です。

 通常、ツール ウィンドウには、ユーザーが操作できるさまざまなコントロールが用意されています。 たとえば、 **[プロパティ]** ウィンドウでは、ユーザーが特定の目的に対応するオブジェクトのプロパティを設定できます。 **[プロパティ]** ウィンドウはこの意味で特殊化されていますが、さまざまな状況で使用できるため、一般的でもあります。 同様に、 **[出力]** ウィンドウはテキストベースの出力を提供するため特殊化されていますが、Visual Studio の多くのサブシステムが Visual Studio ユーザーに出力を提供するために使用できるため、一般的です。

 いくつかのツール ウィンドウが含まれている次の Visual Studio の図について考えてみましょう。

 ![スクリーン ショット](../../extensibility/internals/media/t1gui.png "T1gui")

 一部のツール ウィンドウは、ソリューション エクスプローラーのツール ウィンドウを表示し、他のツール ウィンドウを非表示にして、タブをクリックすることで使用できるようにする、1 つのウィンドウにまとめてドッキングされています。 この図には、1 つのウィンドウにまとめてドッキングされている他の 2 つのツール ウィンドウ ( **[エラー一覧]** ウィンドウと **[出力]** ウィンドウ) が示されています。

 また、複数のエディター ウィンドウが表示されている、メインのドキュメント ウィンドウも示されています。 ツール ウィンドウには通常 1 つのインスタンスしかありませんが (1 つしか開けない "**ソリューション エクスプローラー**" など)、エディター ウィンドウには複数のインスタンスがある場合があります。そのそれぞれは別個のドキュメントを編集するために使用されますが、すべてが同じウィンドウにドッキングされています。 この図は、2 つのエディター ウィンドウ、1 つのフォーム デザイナー ウィンドウがあるドキュメント ウィンドウを示しています。 ドキュメント ウィンドウ内のすべてのウィンドウは、タブをクリックすると使用可能になりますが、EditorPane.cs ファイルが含まれているエディター ウィンドウが表示されていて、アクティブになっています。

 Visual Studio を拡張すると、Visual Studio ユーザーが拡張機能を操作するためのツール ウィンドウを作成できます。 また、Visual Studio ユーザーがドキュメントを編集するための独自のエディターを作成することもできます。 ツール ウィンドウとエディターは Visual Studio に統合されるため、タブでのドッキングや表示が正しく行われるようにプログラムする必要はありません。 Visual Studio に正しく登録されると、Visual Studio のツール ウィンドウとドキュメント ウィンドウの一般的な機能が自動的に組み込まれます。 詳細については、「[ツール ウィンドウの拡張とカスタマイズ](../../extensibility/extending-and-customizing-tool-windows.md)」を参照してください。

## <a name="document-windows"></a>ドキュメント ウィンドウ
 ドキュメント ウィンドウは、マルチドキュメント インターフェイス (MDI) ウィンドウのフレーム化された子ウィンドウです。 通常、ドキュメント ウィンドウは、テキスト エディター、フォーム エディター (デザイナーとも呼ばれます)、または編集コントロールをホストするために使用されますが、他の機能の種類をホストすることもできます。 **[新しいファイル]** ダイアログ ボックスには、Visual Studio に用意されているドキュメント ウィンドウの例が含まれています。

 ほとんどのエディターは、プログラミング言語や、HTML ページ、フレームセット、C++ ファイル、ヘッダー ファイルなどのファイルの種類に固有です。 ユーザーは、 **[新しいファイル]** ダイアログ ボックスでテンプレートを選択して、テンプレートに関連付けられているファイルの種類のエディター用のドキュメント ウィンドウを動的に作成します。 ドキュメント ウィンドウは、ユーザーが既存のファイルを開いたときにも作成されます。

 ドキュメント ウィンドウは、MDI クライアント領域に制限されています。 各ドキュメント ウィンドウには上部にタブがあり、タブ オーダーは MDI 領域で開いている他のウィンドウにリンクされています。 ドキュメント ウィンドウのタブを右クリックすると、ショートカット メニューが表示されます。これには、MDI 領域を水平または垂直の複数のタブ グループに分割するためのオプションが含まれています。 MDI 領域を分割すると、複数のファイルを同時に表示することができます。 詳細については、[ドキュメント ウィンドウ](../../extensibility/internals/document-windows.md)に関するページを参照してください。

## <a name="editors"></a>エディター
 Visual Studio エディターでは、Managed Extensibility Framework (MEF) を使用して、カスタマイズしたり、独自の種類のコンテンツに使用したりできます。 多くの場合、エディターを拡張するために VSPackage を作成する必要はありませんが、シェルの機能 (メニュー コマンドやショートカット キーなど) を含める場合は、MEF 拡張と VSPackage を組み合わせることができます。

 また、たとえばデータベースの読み取りと書き込みを行う場合や、デザイナーを使用する場合に、カスタム エディターを作成することもできます。 メモ帳や Microsoft ワードパッドなどの外部エディターを使用することもできます。 詳細については、「[エディターと言語サービスの拡張機能](../../extensibility/editor-and-language-service-extensions.md)」を参照してください。

## <a name="language-services"></a>言語サービス
 Visual Studio エディターで新しいプログラミング キーワードや新しいプログラミング言語をサポートするようにしたい場合は、言語サービスを作成します。 各言語サービスは、特定のエディター機能を完全に実装したり、部分的に実装したり、またはまったく実装しない場合があります。 言語サービスでは、構成方法に応じて、構文の強調表示、かっこの一致、IntelliSense のサポート、およびエディターのその他の機能を使用できます。

 言語サービスの中核となるのは、パーサーとスキャナーです。 スキャナー (レクサー) はソース ファイルをトークンと呼ばれる要素に分割し、パーサーはそれらのトークン間の関係を確立します。 言語サービスを作成する場合は、Visual Studio が言語のトークンと文法を理解できるように、パーサーとスキャナーを実装する必要があります。 マネージドまたはアンマネージ言語サービスを作成できます。 詳細については、「[従来の言語サービスの機能拡張](../../extensibility/internals/legacy-language-service-extensibility.md)」を参照してください。

## <a name="projects"></a>プロジェクト

Visual Studio でプロジェクトとは、ソース コードやその他のリソースを整理したりビルドしたりするために開発者が使用するコンテナーです。 プロジェクトを使用すると、ソース コード、Web サービスやデータベースへの参照、およびその他のリソースの整理、ビルド、デバッグ、およびデプロイを実行することができます。 VSPackage では、プロジェクト タイプ、プロジェクトのサブタイプ、およびカスタム ツールを提供することで、Visual Studio プロジェクト システムを拡張できます。

プロジェクトは "*ソリューション*" 内でまとめて収集することもできます。これは、アプリケーションを作成するために連携して動作する 1 つ以上のプロジェクトをグループ化したものです。 ソリューションに関連するプロジェクトと状態の情報は、2 つのソリューション ファイル (テキストベースの[ソリューション (.sln) ファイル](solution-dot-sln-file.md)とバイナリ [ソリューション ユーザー オプション (.suo) ファイル](solution-user-options-dot-suo-file.md)) に格納されます。 これらのファイルは、以前のバージョンの Visual Basic で使用されていたグループ (.vbg) ファイル、および以前のバージョンの C++ で使用されていたワークスペース (.dsw) およびユーザー オプション (.opt) ファイルに似ています。

詳細については、[プロジェクト](../../extensibility/internals/projects.md)および[ソリューション](../../extensibility/internals/solutions-overview.md)に関するページを参照してください。

## <a name="project-and-item-templates"></a>プロジェクト テンプレートと項目テンプレート
 Visual Studio には、定義済みのプロジェクト テンプレートとプロジェクト項目テンプレートが含まれています。 また、独自のテンプレートを作成したり、コミュニティからテンプレートを取得して、それらを Visual Studio に統合したりすることもできます。 [MSDN コード ギャラリー](https://code.msdn.microsoft.com/site/search?query=visual%20studio)は、テンプレートと拡張機能のための場所です。

 テンプレートには、特定の種類のアプリケーション、コントロール、ライブラリ、またはクラスをビルドするために必要なプロジェクトの構造と基本ファイルが含まれています。 これらのテンプレートのいずれかに似たソフトウェアを開発する場合は、テンプレートを基にしているプロジェクトを作成してから、そのプロジェクト内のファイルを変更します。

> [!NOTE]
> このテンプレートのアーキテクチャは、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] プロジェクトではサポートされていません。

 詳細については、「[プロジェクトおよびプロジェクト項目テンプレートの追加](../../extensibility/internals/adding-project-and-project-item-templates.md)」を参照してください。

## <a name="properties-and-options"></a>プロパティとオプション
 **[プロパティ]** ウィンドウには、1 つまたは複数の選択された項目のプロパティが表示されます。[[プロパティの拡張]](../../extensibility/internals/extending-properties.md) オプションのページには、プログラミング言語や VSPackage などの特定のコンポーネントに関連するオプションのセットが含まれています (「[オプションとオプション ページ](../../extensibility/internals/options-and-options-pages.md)」)。 設定は、通常、インポートおよびエクスポート可能な UI 関連の機能です (「[ユーザー設定のサポート](../../extensibility/internals/support-for-user-settings.md)」)。

## <a name="visual-studio-services"></a>Visual Studio のサービス
 サービスは、コンポーネントが使用する特定のインターフェイスのセットを提供します。 Visual Studio には、拡張機能を含む、どのコンポーネントでも使用できる一連のサービスが用意されています。 たとえば、Visual Studio のサービスを使用すると、ツール ウィンドウを動的に表示または非表示にしたり、ヘルプ、ステータス バー、または UI イベントへのアクセスを有効にしたりできます。 Visual Studio エディターには、エディター拡張機能によってインポートできるサービスも用意されています。 詳細については、「[サービスの使用と提供](../../extensibility/using-and-providing-services.md)」を参照してください。

## <a name="debugger"></a>デバッガー
 デバッガーは、言語固有のデバッグ コンポーネントに対するユーザー インターフェイスです。 新しい言語サービスを作成した場合は、デバッガーにフックするために特定のデバッグ エンジンを作成する必要があります。 詳細については、「[Visual Studio デバッガーの拡張性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)」を参照してください。

## <a name="source-control"></a>ソース管理
 ソース管理プラグインまたは VSPackage の実装の詳細については、[ソース管理](../../extensibility/internals/source-control.md)に関するページを参照してください。

## <a name="wizards"></a>ウィザード
 ウィザードは新しいプロジェクト タイプと組み合わせて作成できるため、ウィザードは、ユーザーがそのタイプの新しいプロジェクトを作成するときに正しい決定を下すのに役立ちます。 詳しくは、「[ウィザード](../../extensibility/internals/wizards.md)」を参照してください。

## <a name="custom-tools"></a>カスタム ツール
 カスタム ツールを使用すると、プロジェクト内の項目にツールを関連付けて、ファイルが保存されるたびにそのツールを実行することができます。 詳細については、[カスタム ツール](../../extensibility/internals/custom-tools.md)に関するページを参照してください。

## <a name="vssdk-utilities"></a>VSSDK ユーティリティ
 VSSDK には、VSPackage のさまざまな側面を操作するために必要になる可能性のある一連のユーティリティが含まれています。 詳細については、「[VSSDK ユーティリティ](../../extensibility/internals/vssdk-utilities.md)」を参照してください。

## <a name="using-windows-installer"></a>Windows インストーラーを使用する
 場合によっては、VSIX インストーラーではなく Windows インストーラーの使用が必要になることがあります。たとえば、レジストリへの書き込みが必要になることがあります。 拡張機能との Windows インストーラーの使用の詳細については、「[Windows インストーラーを使用した VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)」を参照してください。

## <a name="help-viewer"></a>ヘルプ ビューアー
 独自のヘルプおよび F1 ページをヘルプ ビューアーに統合することができます。 詳細については、「[Microsoft ヘルプ ビューアー SDK](../../extensibility/internals/microsoft-help-viewer-sdk.md)」を参照してください。
