---
title: Visual Studio におけるクロス プラットフォーム モバイル開発 | Microsoft Docs
description: この記事では、Visual Studio を使用して、Android、iOS、Windows デバイス用のアプリを構築する方法について説明します。
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 10/17/2019
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 8202717a-e990-45cf-b092-438651ccb38a
author: conceptdev
ms.author: crdun
manager: crdun
ms.workload:
- multiple
ms.openlocfilehash: 2f3c611ae157be4f2ea89254856bdd3b6fba448d
ms.sourcegitcommit: 63cb90e8cea112aa2ce8741101b309dbc709e393
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2021
ms.locfileid: "110687677"
---
# <a name="cross-platform-mobile-development-in-visual-studio"></a>Visual Studio におけるクロス プラットフォーム モバイル開発

Android、iOS、および Windows デバイス用のアプリを Visual Studio を使用して作成することができます。  アプリを設計する過程で Visual Studio のツールを利用すると、Microsoft 365、Azure App Services、Application Insights などの接続済みサービスを簡単に追加できます。

アプリを作成するには、C# と .NET Framework、HTML と JavaScript、または C++ を使用します。 コード、文字列、イメージを共有できるほか、場合によってはユーザー インターフェイスも共有できます。

ゲームまたは没入感のあるグラフィカル アプリを作成する場合は、Visual Studio Tools for Unity をインストールすれば、Visual Studio と Unity の強力な生産性機能をすべて活用できます。Unity は、iOS、Android、Windows、およびその他のプラットフォームで実行するアプリ用のクロスプラットフォームのゲーム/グラフィックス エンジンおよび開発環境として人気を博しています。

## <a name="build-an-app-for-android-ios-and-windows-net-framework"></a>Android、iOS、および Windows 用のアプリをビルドする (.NET Framework)

![デバイス](../cross-platform/media/homedevices.png "HomeDevices")

Visual Studio Tools for Xamarin を利用すれば、コードや UI を共有し、同じソリューションで Android、iOS、Windows を対象にできます。

|**詳細を表示**|
|--------------------|
|[Visual Studio のインストール](https://visualstudio.microsoft.com/vs/community/) (VisualStudio.com)|
|[Visual Studio での Xamarin について学習する](https://visualstudio.microsoft.com/xamarin/) (VisualStudio.com)|
|[Xamarin モバイル アプリ開発ドキュメント](/xamarin/) |
|[Xamarin アプリを使用した DevOps](/xamarin/tools/ci/devops/) |
|[Visual Studio でのユニバーサル Windows アプリについて学習する](https://visualstudio.microsoft.com/vs/universal-windows-platform/) (VisualStudio.com)|
|[Swift と C# との間の類似点について学習する](https://aka.ms/scposter) (download.microsoft.com)|

### <a name="target-android-ios-and-windows-from-a-single-code-base"></a><a name="AndroidHTML"></a> 1 つのコード ベースから Android、iOS、Windows を対象にする

 C# または F# を使用することで (Visual Basic は現時点ではサポートされていません)、Android、iOS、Windows のネイティブ アプリを開発できます。  始めるには、Visual Studio をインストールし、インストーラーで **[.NET によるモバイル開発]** オプションを選択します。

 Visual Studio を既にインストールしてある場合は、**Visual Studio インストーラー** をもう一度実行し、Xamarin に対して上と同じ **[.NET によるモバイル開発]** オプションを選択します。

 完了すると、プロジェクト テンプレートが **[新しいプロジェクト]** ダイアログ ボックスに表示されます。 Xamarin テンプレートを見つける最も簡単な方法は、"Xamarin" で検索することです。

 Xamarin は Android、iOS、Windows のネイティブ機能を .NET のクラスとメソッドとして表示します。 つまり、アプリにはネイティブ API とネイティブ コントロールのフル アクセスが与えられます。ネイティブ プラットフォーム言語で記述されたアプリと同様の応答性を持ちます。

 プロジェクトを作成した後は、生産性を高める Visual Studio の機能をすべて活用できます。 たとえば、デザイナーを使用してページを作成し、IntelliSense を使用してモバイル プラットフォームのネイティブ API を探索できます。 アプリを実行して表示を確認する準備ができたら、Android SDK エミュレーターを使用して Windows アプリをネイティブに実行できます。 テザリングされた Android デバイスや Windows デバイスを直接使用することもできます。 iOS プロジェクトでは、Mac のネットワークに接続し、Visual Studio から iOS エミュレーターを起動したり、テザリングされたデバイスに接続したりできます。

#### <a name="design-one-set-of-pages-that-render-across-all-devices-by-using-xamarinforms"></a>すべてのデバイス用にレンダリングするページを 1 セット、Xamarin.Forms を使用してデザインする

 アプリのデザインの複雑さによっては、プロジェクト テンプレートの [ *Mobile Apps* ] グループにある **[Xamarin.Forms]** テンプレートを使用して作成することを検討します。 Xamarin.Forms は、Android、iOS、Windows 間で共有できる単一のユーザー インターフェイスを作成する UI ツールキットです。  Xamarin.Forms ソリューションをコンパイルすると、Android アプリ、iOS アプリ、Windows アプリが生成されます。 詳しくは、「[Xamarin によるモバイル開発の概要](/xamarin/cross-platform/get-started/introduction-to-mobile-development/)」および [Xamarin.Forms のドキュメント](/xamarin/xamarin-forms/)に関するページをご覧ください。

#### <a name="share-code-between-android-ios-and-windows-apps"></a><a name="ShareHTML"></a> Android、iOS、および Windows アプリ間でコードを共有する

 Xamarin.Forms を使用せず、プラットフォームごとに個別にデザインすることにした場合は、UI 以外のコードの大部分をプラットフォームのプロジェクト (Android、iOS、および Windows) 間で共有できます。 これには、ビジネス ロジック、クラウド統合、データベース アクセス、または .NET Framework を対象とするその他のコードが含まれます。 特定のプラットフォームを対象とするコードのみ、共有することができません。

 ![Windows、iOS、および Android の UI 間でコードを共有する](../cross-platform/media/sharecode.png "ShareCode")

 共有プロジェクト、ポータブル クラス ライブラリ プロジェクト、またはその両方を使用して、コードを共有できます。 共有プロジェクトに最適なコードもあれば、ポータブル クラス ライブラリ プロジェクトにより適したコードもあります。

|**詳細を表示**|
|--------------------|
|[コード共有のオプション](/xamarin/cross-platform/app-fundamentals/code-sharing/) (Xamarin) |
|[.NET でのコード共有オプション](/dotnet/standard/cross-platform/) |

### <a name="target-windows-10-devices"></a><a name="WindowsHTML"></a> Windows 10 デバイスを対象にする

 ![Windows デバイス](../cross-platform/media/windowsdevices.png "Windows デバイス")

 Windows 10 デバイスを幅広く対象とした単一のアプリを作成する必要がある場合は、ユニバーサル Windows アプリを作成します。 1 つのプロジェクトを使用してアプリをデザインすれば、どのデバイスを使用して表示してもアプリのページが正しくレンダリングされます。

 ユニバーサル Windows プラットフォーム (UWP) アプリのプロジェクト テンプレートから作業を開始します。 ページを視覚的にデザインした後、それらのページをプレビュー ウィンドウで開くと、さまざまな種類のデバイスでどのように表示されるかを確認できます。 デバイスに表示されるページが気に入らない場合は、画面サイズ、解像度、あるいは縦モードまたは横モードなどのさまざまな向きに合わせて、ページを最適化できます。 このような操作すべてを、Visual Studio の直感的なツール ウィンドウと簡単にアクセスできるメニュー オプションを使用して実行できます。 アプリを実行してコードをデバッグする準備ができたら、さまざまな種類のデバイスのデバイス エミュレーターやシミュレーターのすべてが、 **[標準]** ツールバーの 1 つのドロップダウン リストにまとめられています。

|**詳細を表示**|
|--------------------|
|[ユニバーサル Windows プラットフォームの紹介](/windows/uwp/get-started/universal-application-platform-guide)|
|[最初のアプリの作成](/windows/uwp/get-started/your-first-app)|
|[ユニバーサル Windows プラットフォーム (UWP) 向けアプリの開発](../cross-platform/develop-apps-for-the-universal-windows-platform-uwp.md)|

::: moniker range="vs-2017"

## <a name="build-an-app-for-android-ios-and-windows-htmljavascript"></a><a name="HTML"></a> Android、iOS、および Windows 用のアプリをビルドする (HTML/JavaScript)

 ![Windows、iOS、Android の各デバイス](../cross-platform/media/homedevices.png "Windows、iOS、Android の各デバイス")

 HTML と JavaScript に精通した Web 開発者は、Visual Studio Tools for Apache Cordova を使用して、Windows、Android、および iOS を対象とすることができます。 これらのアプリは 3 つのすべてのプラットフォームを対象にすることができ、開発者が最も慣れているスキルとプロセスを使用してアプリを作成できます。

 Apache Cordova は、プラグイン モデルを含むフレームワークです。 このプラグイン モデルは、3 つのすべてのプラットフォーム (Android、iOS、Windows) のネイティブ デバイス機能にアクセスするために使用できる単一の JavaScript API を提供します。

 これらの API はクロスプラットフォームであるため、記述するコードの大部分を 3 つのすべてのプラットフォーム間で共有できます。 このため、開発と保守のコストを削減できます。 また、ゼロから始める必要がありません。 他の種類の Web アプリケーションを既に作成してある場合は、Cordova アプリでそれらのファイルを共有できるため、修正や再設計の必要はありません。

 ![JavaScript でのマルチデバイス ハイブリッド アプリ](../cross-platform/media/multidevicehybridapps.png "JavaScript を使用したマルチデバイス ハイブリッド アプリ")

 作業を開始するには、Visual Studio をインストールして、セットアップ中に **[JavaScript によるモバイル開発]** 機能を選択します。 Cordova ツールにより、マルチプラットフォーム アプリをビルドするために必要なすべてのサード パーティのソフトウェアが自動的にインストールされます。

 拡張機能をインストールした後、Visual Studio を開き、 **[空のアプリケーション (Apache Cordova)]** プロジェクトを作成します。 その後、JavaScript または TypeScript を使用してアプリを開発できます。 また、プラグインを追加してアプリの機能を拡張することもでき、プラグインの API はコードを記述するときに IntelliSense に表示されます。

 アプリを実行してコードをデバッグする準備ができたら、エミュレーターとして、Apache Ripple エミュレーターや Android Emulator、ブラウザー、またはコンピューターに直接接続したデバイスなどを選択します。 その後、アプリを起動します。 Windows PC でアプリを開発している場合は、この上さらにそのアプリを実行することもできます。 これらのオプションすべては、Visual Studio Tools for Apache Cordova の一部として Visual Studio に組み込まれます。

 ユニバーサル Windows プラットフォーム (UWP) アプリを作成するためのプロジェクト テンプレートは、Visual Studio でまだ使用できるので、Windows デバイスだけを対象にする場合は、自由に使用してください。 後で Android および iOS を対象にすることを決定した場合は、いつでも Cordova プロジェクトにコードを移植できます。

|**詳細を表示**|
|--------------------|
|[Visual Studio のインストール](https://visualstudio.microsoft.com/vs/community/) (VisualStudio.com)|
|[Visual Studio Tools for Apache Cordova の使用を開始する](/previous-versions/visualstudio/cross-platform/tools-for-cordova/)|
|[Visual Studio Emulator for Android について学習する](https://visualstudio.microsoft.com/vs/msft-android-emulator/) (VisualStudio.com)|

::: moniker-end

<a name="CPP"></a>

## <a name="build-an-app-for-android-ios-and-windows-c"></a>Android、iOS、Windows 用のアプリを作成する (C++)

![C&#43;&#43; を使用して Android、iOS、Windows 用に作成する](../cross-platform/media/cross_plat_cpp_intro_image.png "Cross_Plat_CPP_Intro_Image")

 最初に、Visual Studio と **C++ によるモバイル開発** ワークロードをインストールします。 その後は、Android 用の Native-Activity アプリケーションか、Windows または iOS を対象とするアプリを構築できます。 必要であれば、同じソリューションで Android、iOS、Windows を対象にし、クロスプラットフォームの静的または動的な共有ライブラリを使用して、それらの間でコードを共有することができます。

 ゲームなどの高度なグラフィックス操作を必要とする Android アプリをビルドする必要がある場合に、C++ を利用できます。 **Native-Activity アプリケーション (Android)** プロジェクトで開始します。 このプロジェクトでは、C 言語のツール チェーンが完全にサポートされます。

 ![Native-Activity プロジェクトのテンプレート](../cross-platform/media/cross-plat_cpp_native.png "ネイティブ アクティビティ プロジェクトのテンプレート")

 アプリケーションを実行して結果を確認する準備ができたら、Android Emulator を使用できます。 高速で信頼性が高く、簡単にインストールして構成できます。

 C++ とユニバーサル Windows プラットフォーム (UWP) アプリ プロジェクト テンプレートを使用すると、幅広い Windows 10 デバイスを対象とするアプリケーションを作成することもできます。 この点については、このトピックで前に説明した「[Windows 10 デバイスを対象にする](#WindowsHTML)」セクションをお読みください。

 静的または動的な共有ライブラリを作成して、Android、iOS、Windows 間で C++ コードを共有することができます。

 ![静的および動的な共有ライブラリ](../cross-platform/media/cross_plat_cpp_libraries.png "静的および動的な共有ライブラリ")

 このセクションで既に説明したものと同様に、Windows、iOS、または Android のプロジェクトでそのライブラリを使用することができます。 また、Xamarin、Java、またはアンマネージ DLL 内の関数を呼び出すことのできる任意の言語を使用してビルドするアプリで、そのライブラリを利用できます。

 これらのライブラリでコードを記述するときは、IntelliSense を使用して Android プラットフォームと Windows プラットフォームのネイティブ API を探索できます。 これらのライブラリ プロジェクトは Visual Studio デバッガーと完全に統合されるため、デバッガーの高度な機能をすべて活用して、ブレークポイントの設定、コードのステップ実行、問題点の検索と修正を行うことができます。

|**詳細を表示**|
|--------------------|
|[Visual Studio をダウンロードする](https://visualstudio.microsoft.com/downloads/) (VisualStudio.com)|
|[C++ によるクロスプラットフォーム モバイル開発をインストールする](/cpp/cross-platform/install-visual-cpp-for-cross-platform-mobile-development)|
|[C++ を使用して複数のプラットフォームを対象とすることについて学習する](https://visualstudio.microsoft.com/vs/cplusplus-mdd/) (VisualStudio.com)|
|[必要なものをインストールしてから、Android 用の C++ ネイティブ アクティビティ アプリケーションを作成する](/cpp/cross-platform/create-an-android-native-activity-app)|
|[Android と Windows アプリでの C++ コードの共有について学習する](https://visualstudio.microsoft.com/vs/cplusplus-mdd/) (VisualStudio.com)|
|[C++ でのクロスプラットフォーム モバイル開発の例](/cpp/cross-platform/cross-platform-mobile-development-examples)|

<a name="Unity"></a>

## <a name="build-a-cross-platform-game-for-android-ios-and-windows-by-using-visual-studio-tools-for-unity"></a>Android、iOS、Windows 用のクロスプラットフォーム ゲームを Visual Studio Tools for Unity を使用してビルドする

 Visual Studio Tools for Unity は、Visual Studio の強力なコード編集、生産性向上、およびデバッグ ツールを、Windows、iOS、Android、および Web を含むその他のプラットフォームを対象とするクロスプラットフォームのゲーム/グラフィックス エンジンおよび没入感のあるアプリ開発環境として人気の高い *Unity* と統合するための Visual Studio 用の無料の拡張機能です。

 ![VSTU 開発環境](../cross-platform/media/vstu_overview.png "Visual Studio Tools for Unity の概要")

 Visual Studio tools Unity (VSTU) を利用すると、Visual Studio を使用して C# でゲームとエディター スクリプトを記述した後、強力なデバッガーを使用してエラーを検出して修正できます。 VSTU の最新リリースでは、Unity 2018.1 のサポートが提供され、Unity の ShaderLab シェーダー言語の構文の色分け、Unity との同期機能の向上、デバッグの機能向上、MonoBehavior ウィザードによるコード生成の機能強化などがなされました。 また、VSTU により、Unity のプロジェクト ファイル、コンソール メッセージ、およびゲームを開始する機能が Visual Studio に統合されるため、コードの記述中に Unity エディターとの間で切り替える手間を少なくできます。

|**詳細を表示**|
|--------------------|
|[Visual Studio での Unity ゲーム構築について学習する](https://visualstudio.microsoft.com/vs/features/game-development/#tab-4b0d0be8de5f65564ad)|
|[Visual Studio Tools for Unity についてさらに学習する](/gamedev/unity/get-started/visual-studio-tools-for-unity.md) |
|[Visual Studio Tools for Unity を使い始める](/gamedev/unity/get-started/getting-started-with-visual-studio-tools-for-unity.md) |
|[Visual Studio Tools for Unity 2.0 Preview の最新の拡張機能について学習する](https://devblogs.microsoft.com/visualstudio/visual-studio-tools-for-unity-2-0-preview/) (Visual Studio ブログ)|
|[Visual Studio Tools for Unity 2.0 Preview の紹介ビデオを見る](https://www.bing.com/videos/search?q=visual+studio+tools+for+unity&qs=n&form=QBVLPG&pq=visual+studio+tools+for+unity&sc=6-29&sp=-1&sk=#view=detail&mid=0A13177F0BC7463A24080A13177F0BC7463A2408&preserve-view=true) (ビデオ)|
|[Unity について学習する](https://unity.com/) (Unity Web サイト)|

## <a name="see-also"></a>関連項目

- [Visual Studio プロジェクトに Microsoft 365 API を追加する](/office/developer-program/office-365-developer-program)
- [Azure App Services - モバイル アプリ](https://azure.microsoft.com/services/app-service/mobile/)
- [Visual Studio App Center](/appcenter)
