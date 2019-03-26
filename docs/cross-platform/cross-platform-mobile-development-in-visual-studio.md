---
title: Visual Studio におけるクロス プラットフォーム モバイル開発 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2018
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 8202717a-e990-45cf-b092-438651ccb38a
author: conceptdev
ms.author: crdun
manager: crdun
ms.workload:
- multiple
ms.openlocfilehash: 2144ebd4725532d3dbbf4685f6629cbbbdd7c73e
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58069685"
---
# <a name="cross-platform-mobile-development-in-visual-studio"></a>Visual Studio におけるクロス プラットフォーム モバイル開発

Android、iOS、および Windows デバイス用のアプリを Visual Studio を使用して作成することができます。  アプリを設計する過程で Visual Studio のツールを利用すると、Office 365、Azure App Services、Application Insights などの接続済みサービスを簡単に追加できます。

アプリを作成するには、C# と .NET Framework、HTML と JavaScript、または C++ を使用します。 コード、文字列、イメージを共有できるほか、場合によってはユーザー インターフェイスも共有できます。

ゲームまたは没入感のあるグラフィカル アプリを作成する場合は、Visual Studio Tools for Unity をインストールすれば、Visual Studio と Unity の強力な生産性機能をすべて活用できます。Unity は、iOS、Android、Windows、およびその他のプラットフォームで実行するアプリ用のクロスプラットフォームのゲーム/グラフィックス エンジンおよび開発環境として人気を博しています。

## <a name="build-an-app-for-android-ios-and-windows-net-framework"></a>Android、iOS、および Windows 用のアプリをビルドする (.NET Framework)

![デバイス](../cross-platform/media/homedevices.png "HomeDevices")

Visual Studio Tools for Xamarin を利用すれば、コードや UI を共有し、同じソリューションで Android、iOS、Windows を対象にできます。

|**詳細を表示**|
|--------------------|
|[Visual Studio のインストール](http://visualstudio.microsoft.com/products/visual-studio-community-vs) (VisualStudio.com)|
|[Visual Studio での Xamarin について学習する](https://visualstudio.microsoft.com/xamarin/) (VisualStudio.com)|
|[Xamarin モバイル アプリ開発ドキュメント](/xamarin/) |
|[Xamarin アプリを使用した DevOps](/xamarin/tools/ci/devops/) |
|[Visual Studio でのユニバーサル Windows アプリについて学習する](https://visualstudio.microsoft.com/vs/universal-windows-platform/) (VisualStudio.com)|
|[Swift と C# との間の類似点について学習する](https://aka.ms/scposter) (download.microsoft.com)|

###  <a name="AndroidHTML"></a> 1 つのコード ベースから Android、iOS、Windows を対象にする

 C# または F# を使用することで (Visual Basic は現時点ではサポートされていません)、Android、iOS、Windows のネイティブ アプリを開発できます。  始めるには、Visual Studio 2017 をインストールし、インストーラーで **[.NET によるモバイル開発]** オプションを選びます。

 Visual Studio 2017 を既にインストールしてある場合は、**Visual Studio インストーラー**をもう一度実行し、Xamarin に対して上と同じ **[.NET によるモバイル開発]** オプションを選びます。

 完了すると、プロジェクト テンプレートが **[新しいプロジェクト]** ダイアログ ボックスに表示されます。 Xamarin テンプレートを見つける最も簡単な方法は、"Xamarin" で検索することです。

 Xamarin は Android、iOS、Windows のネイティブ機能を .NET のクラスとメソッドとして表示します。 つまり、アプリにはネイティブ API とネイティブ コントロールのフル アクセスが与えられます。ネイティブ プラットフォーム言語で記述されたアプリと同様の応答性を持ちます。

 プロジェクトを作成した後は、生産性を高める Visual Studio の機能をすべて活用できます。 たとえば、デザイナーを使用してページを作成し、IntelliSense を使用してモバイル プラットフォームのネイティブ API を探索できます。 アプリを実行して表示を確認する準備ができたら、Android SDK エミュレーターを使用して Windows アプリをネイティブに実行できます。 テザリングされた Android デバイスや Windows デバイスを直接使用することもできます。 iOS プロジェクトでは、Mac のネットワークに接続し、Visual Studio から iOS エミュレーターを起動したり、テザリングされたデバイスに接続したりできます。

#### <a name="design-one-set-of-pages-that-render-across-all-devices-by-using-xamarinforms"></a>すべてのデバイス用にレンダリングするページを 1 セット、Xamarin.Forms を使用してデザインする

 アプリのデザインの複雑さによっては、プロジェクト テンプレートの [ *Mobile Apps* ] グループにある **[Xamarin.Forms]** テンプレートを使用して作成することを検討します。 Xamarin.Forms は、Android、iOS、Windows 間で共有できる単一のユーザー インターフェイスを作成する UI ツールキットです。  Xamarin.Forms ソリューションをコンパイルすると、Android アプリ、iOS アプリ、Windows アプリが生成されます。 詳しくは、「[Xamarin によるモバイル開発の概要](/xamarin/cross-platform/get-started/introduction-to-mobile-development/)」および [Xamarin.Forms のドキュメント](/xamarin/xamarin-forms/)に関するページをご覧ください。

####  <a name="ShareHTML"></a> Android、iOS、および Windows アプリ間でコードを共有する

 Xamarin.Forms を使用せず、プラットフォームごとに個別にデザインすることにした場合は、UI 以外のコードの大部分をプラットフォームのプロジェクト (Android、iOS、および Windows) 間で共有できます。 これには、ビジネス ロジック、クラウド統合、データベース アクセス、または .NET Framework を対象とするその他のコードが含まれます。 特定のプラットフォームを対象とするコードのみ、共有することができません。

 ![Windows、iOS、Android の UI でコードを共有](../cross-platform/media/sharecode.png "ShareCode")

 共有プロジェクト、ポータブル クラス ライブラリ プロジェクト、またはその両方を使用して、コードを共有できます。 共有プロジェクトに最適なコードもあれば、ポータブル クラス ライブラリ プロジェクトにより適したコードもあります。

|**詳細を表示**|
|--------------------|
|[コード共有のオプション](/xamarin/cross-platform/app-fundamentals/code-sharing/) (Xamarin) |
|[.NET でのコード共有オプション](/dotnet/standard/cross-platform/) |

###  <a name="WindowsHTML"></a> Windows 10 デバイスを対象にする

 ![Windows デバイス](../cross-platform/media/windowsdevices.png "Windows デバイス")

 Windows 10 デバイスを幅広く対象とした単一のアプリを作成する必要がある場合は、ユニバーサル Windows アプリを作成します。 1 つのプロジェクトを使用してアプリをデザインすれば、どのデバイスを使用して表示してもアプリのページが正しくレンダリングされます。

 ユニバーサル Windows プラットフォーム (UWP) アプリのプロジェクト テンプレートから作業を開始します。 ページを視覚的にデザインした後、それらのページをプレビュー ウィンドウで開くと、さまざまな種類のデバイスでどのように表示されるかを確認できます。 デバイスに表示されるページが気に入らない場合は、画面サイズ、解像度、あるいは縦モードまたは横モードなどのさまざまな向きに合わせて、ページを最適化できます。 このような操作すべてを、Visual Studio の直感的なツール ウィンドウと簡単にアクセスできるメニュー オプションを使用して実行できます。 アプリを実行してコードをデバッグする準備ができたら、さまざまな種類のデバイスのデバイス エミュレーターやシミュレーターのすべてが、**[標準]** ツールバーの 1 つのドロップダウン リストにまとめられています。

|**詳細を表示**|
|--------------------|
|[ユニバーサル Windows プラットフォームの紹介](/windows/uwp/get-started/universal-application-platform-guide)|
|[最初のアプリの作成](/windows/uwp/get-started/your-first-app)|
|[ユニバーサル Windows プラットフォーム (UWP) 向けアプリの開発](../cross-platform/develop-apps-for-the-universal-windows-platform-uwp.md)|
|[アプリを Universal Windows Platform (UWP) へ移行する](https://msdn.microsoft.com/library/mt148501.aspx)|

##  <a name="HTML"></a> Android、iOS、および Windows 用のアプリをビルドする (HTML/JavaScript)

 ![Windows、iOS、Android デバイス](../cross-platform/media/homedevices.png "Windows、iOS、Android デバイス")

 HTML と JavaScript に精通した Web 開発者は、Visual Studio Tools for Apache Cordova を使用して、Windows、Android、および iOS を対象とすることができます。 これらのアプリは 3 つのすべてのプラットフォームを対象にすることができ、開発者が最も慣れているスキルとプロセスを使用してアプリを作成できます。

 Apache Cordova は、プラグイン モデルを含むフレームワークです。 このプラグイン モデルは、3 つのすべてのプラットフォーム (Android、iOS、Windows) のネイティブ デバイス機能にアクセスするために使用できる単一の JavaScript API を提供します。

 これらの API はクロスプラットフォームであるため、記述するコードの大部分を 3 つのすべてのプラットフォーム間で共有できます。 このため、開発と保守のコストを削減できます。 また、ゼロから始める必要がありません。 他の種類の Web アプリケーションを既に作成してある場合は、Cordova アプリでそれらのファイルを共有できるため、修正や再設計の必要はありません。

 ![Javascript でのマルチデバイス ハイブリッド アプリ](../cross-platform/media/multidevicehybridapps.png "Javascript でのマルチデバイス ハイブリッド アプリ")

 作業を開始するには、Visual Studio をインストールして、セットアップ中に **[JavaScript によるモバイル開発]** 機能を選択します。 Cordova ツールにより、マルチプラットフォーム アプリをビルドするために必要なすべてのサード パーティのソフトウェアが自動的にインストールされます。

 拡張機能をインストールした後、Visual Studio を開き、**[空のアプリケーション (Apache Cordova)]** プロジェクトを作成します。 その後、JavaScript または TypeScript を使用してアプリを開発できます。 また、プラグインを追加してアプリの機能を拡張することもでき、プラグインの API はコードを記述するときに IntelliSense に表示されます。

 アプリを実行してコードをデバッグする準備ができたら、エミュレーターとして、Apache Ripple エミュレーターや Android Emulator、ブラウザー、またはコンピューターに直接接続したデバイスなどを選択します。 その後、アプリを起動します。 Windows PC でアプリを開発している場合は、この上さらにそのアプリを実行することもできます。 これらのオプションすべては、Visual Studio Tools for Apache Cordova の一部として Visual Studio に組み込まれます。

 ユニバーサル Windows プラットフォーム (UWP) アプリを作成するためのプロジェクト テンプレートは、Visual Studio でまだ使用できるので、Windows デバイスだけを対象にする場合は、自由に使用してください。 後で Android および iOS を対象にすることを決定した場合は、いつでも Cordova プロジェクトにコードを移植できます。

|**詳細を表示**|
|--------------------|
|[Visual Studio のインストール](http://visualstudio.microsoft.com/products/visual-studio-community-vs) (VisualStudio.com)|
|[Visual Studio Tools for Apache Cordova の使用を開始する](/visualstudio/cross-platform/tools-for-cordova/)|
|[Visual Studio Emulator for Android について学習する](http://visualstudio.microsoft.com/explore/msft-android-emulator-vs) (VisualStudio.com)|

<a name="CPP"></a>

## <a name="build-an-app-for-android-and-windows-c"></a>Android および Windows 用のアプリをビルドする (C++)
 ![C++ を使用し、Android、iOS、Windows 向けに開発する](../cross-platform/media/cross_plat_cpp_intro_image.png "Cross_Plat_CPP_Intro_Image")

 最初に、Visual Studio 2017 と **C++ によるモバイル開発**ワークロードをインストールします。 その後、Android 用のネイティブ アクティビティ アプリケーションか、Windows を対象とするアプリを構築できます。 iOS を対象とする C++ テンプレートは、まだ利用できません。 必要であれば、同じソリューションで Android と Windows を対象にし、クロスプラットフォームの静的または動的な共有ライブラリを使用して両方でコードを共有することができます。

 ゲームなどの高度なグラフィックス操作を必要とする Android アプリをビルドする必要がある場合に、C++ を利用できます。 **[ネイティブ アクティビティ アプリケーション (Android)]** プロジェクトから開始できます。 このプロジェクトでは、C 言語のツール チェーンが完全にサポートされます。

 ![ネイティブ アクティビティ プロジェクト テンプレート](../cross-platform/media/cross-plat_cpp_native.png "ネイティブ アクティビティ プロジェクト テンプレート")

 アプリケーションを実行して結果を確認する準備ができたら、Android Emulator を使用できます。 高速で信頼性が高く、簡単にインストールして構成できます。

 C++ とユニバーサル Windows プラットフォーム (UWP) アプリ プロジェクト テンプレートを使用すると、幅広い Windows 10 デバイスを対象とするアプリケーションを作成することもできます。 この点については、このトピックで前に説明した「[Windows 10 デバイスを対象にする](#WindowsHTML)」セクションをお読みください。

 静的または動的な共有ライブラリを作成して、Android および Windows 間で C++ コードを共有することができます。

 ![静的および動的共有ライブラリ](../cross-platform/media/cross_plat_cpp_libraries.png "静的および動的共有ライブラリ")

 このセクションで既に説明したものと同様に、Windows または Android のプロジェクトでそのライブラリを使用することができます。 また、Xamarin、Java、またはアンマネージ DLL 内の関数を呼び出すことのできる任意の言語を使用してビルドするアプリで、そのライブラリを利用できます。

 これらのライブラリでコードを記述するときは、IntelliSense を使用して Android プラットフォームと Windows プラットフォームのネイティブ API を探索できます。 これらのライブラリ プロジェクトは Visual Studio デバッガーと完全に統合されるため、デバッガーの高度な機能をすべて活用して、ブレークポイントの設定、コードのステップ実行、問題点の検索と修正を行うことができます。

|**詳細を表示**|
|--------------------|
|[Visual Studio のダウンロード](http://visualstudio.microsoft.com/products/visual-studio-community-vs) (VisualStudio.com)|
|[Visual C++ for Cross-Platform Mobile Development ツールのインストール](https://msdn.microsoft.com/library/dn707591.aspx) (MSDN ライブラリ)|
|[C++ を使用して複数のプラットフォームを対象とすることについて学習する](https://visualstudio.microsoft.com/vs/cplusplus-mdd/) (VisualStudio.com)|
|[必要なものをインストールしてから、Android 用のネイティブ アクティビティ アプリケーションを作成する](https://msdn.microsoft.com/library/dn707595.aspx) (MSDN ライブラリ)|
|[Android と Windows アプリでの C++ コードの共有について学習する](https://visualstudio.microsoft.com/vs/cplusplus-mdd/) (VisualStudio.com)|
|[C++ のクロス プラットフォーム モバイル開発の例](https://msdn.microsoft.com/library/dn707596.aspx) (MSDN ライブラリ)|
|[C++ のクロス プラットフォーム モバイル開発のその他の例](https://code.msdn.microsoft.com/site/search?f%5B0%5D.Type=SearchText&f%5B0%5D.Value=android&f%5B1%5D.Type=ProgrammingLanguage&f%5B1%5D.Value=C%2B%2B&f%5B1%5D.Text=C%2B%2B) (code.msdn)|

<a name="Unity"></a>

## <a name="build-a-cross-platform-game-for-android-ios-and-windows-by-using-visual-studio-tools-for-unity"></a>Android、iOS、Windows 用のクロスプラットフォーム ゲームを Visual Studio Tools for Unity を使用してビルドする

 Visual Studio Tools for Unity は、Visual Studio の強力なコード編集、生産性向上、およびデバッグ ツールを、Windows、iOS、Android、および Web を含むその他のプラットフォームを対象とするクロスプラットフォームのゲーム/グラフィックス エンジンおよび没入感のあるアプリ開発環境として人気の高い *Unity* と統合するための Visual Studio 用の無料の拡張機能です。

 ![VSTU 開発環境](../cross-platform/media/vstu_overview.png "Visual Studio Tools for Unity の概要")

 Visual Studio tools Unity (VSTU) を利用すると、Visual Studio を使用して C# でゲームとエディター スクリプトを記述した後、強力なデバッガーを使用してエラーを検出して修正できます。 VSTU の最新リリースでは、Unity 2018.1 のサポートが提供され、Unity の ShaderLab シェーダー言語の構文の色分け、Unity との同期機能の向上、デバッグの機能向上、MonoBehavior ウィザードによるコード生成の機能強化などがなされました。 また、VSTU により、Unity のプロジェクト ファイル、コンソール メッセージ、およびゲームを開始する機能が Visual Studio に統合されるため、コードの記述中に Unity エディターとの間で切り替える手間を少なくできます。

|**詳細を表示**|
|--------------------|
|[Visual Studio での Unity ゲーム構築について学習する](https://visualstudio.microsoft.com/vs/features/game-development/#tab-4b0d0be8de5f65564ad)|
|[Visual Studio Tools for Unity についてさらに学習する](../cross-platform/visual-studio-tools-for-unity.md) |
|[Visual Studio Tools for Unity を使い始める](../cross-platform/getting-started-with-visual-studio-tools-for-unity.md) |
|[Visual Studio Tools for Unity 2.0 Preview の最新の拡張機能について学習する](https://devblogs.microsoft.com/visualstudio/visual-studio-tools-for-unity-2-0-preview/) (Visual Studio ブログ)|
|[Visual Studio Tools for Unity 2.0 Preview の紹介ビデオを見る](http://www.bing.com/videos/search?q=visual+studio+tools+for+unity&qs=n&form=QBVLPG&pq=visual+studio+tools+for+unity&sc=6-29&sp=-1&sk=#view=detail&mid=0A13177F0BC7463A24080A13177F0BC7463A2408) (ビデオ)|
|[Unity について学習する](http://unity3d.com/) (Unity Web サイト)|

## <a name="see-also"></a>関連項目

- [Visual Studio プロジェクトに Office 365 API を追加する](https://docs.microsoft.com/office/developer-program/office-365-developer-program)
- [Azure App Services - モバイル アプリ](https://azure.microsoft.com/services/app-service/mobile/)
- [Visual Studio App Center](https://docs.microsoft.com/appcenter)
