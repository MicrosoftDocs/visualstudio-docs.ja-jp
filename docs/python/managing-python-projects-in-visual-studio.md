---
title: Python アプリケーション プロジェクトの管理
description: Visual Studio のプロジェクトでは、ファイル間の依存関係とアプリケーションの関係の複雑さが管理されます。
ms.date: 03/18/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: c9a20ea3baee84657e26e2d98bb5726c20ceba9e
ms.sourcegitcommit: 4908561809ad397c99cf204f52d5e779512e502c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112254902"
---
# <a name="python-projects-in-visual-studio"></a>Visual Studio の Python プロジェクト

通常、Python アプリケーションはフォルダーとファイルのみを使って定義されますが、アプリケーションが大きくなり、おそらく自動生成されたファイル、Web アプリケーション用 JavaScript などが含まれるようになると、この構造は複雑になる可能性があります。 Visual Studio のプロジェクトは、このような複雑さを管理するのに役立ちます。 プロジェクト ( *.pyproj* ファイル) には、プロジェクトに関連付けられたすべてのソース ファイルとコンテンツ ファイルの識別、各ファイルのビルド情報の格納、ソース管理システムと統合するための情報の保持、論理コンポーネントへのアプリケーションの整理の補助などの機能があります。

![ソリューション エクスプローラーでの Python プロジェクト](media/projects-solution-explorer.png)

さらに、プロジェクトは常に Visual Studio の *ソリューション* 内で管理され、ソリューションは相互に参照する可能性のある任意の数のプロジェクトを含むことができます。 たとえば、Python プロジェクトは、拡張モジュールを実装する C++ プロジェクトを参照できます。 この関係を利用して、Visual Studio では Python プロジェクトのデバッグが開始されると、必要に応じて C++ プロジェクトが自動的に構築されます。 (一般的な説明については、「[Visual Studio のソリューションおよびプロジェクト](../ide/solutions-and-projects-in-visual-studio.md)」を参照してください)。

Visual Studio には、多数のアプリケーション構造を短時間で設定するためのさまざまな Python プロジェクト テンプレートが用意されており、既存のフォルダー ツリーからプロジェクトを作成するためのテンプレートや、クリーンな空のプロジェクトを作成するためのテンプレートなどがあります。 インデックスについては、「[プロジェクト テンプレート](#project-templates)」をご覧ください。

<a name="lightweight-usage-project-free"></a>

::: moniker range=">=vs-2019"
> [!Tip]
> Visual Studio 2019 では、Python コードが含まれるフォルダーを開き、Visual Studio のプロジェクトやソリューションのファイルを作成せずに、そのコードを実行することができます。 詳細については、[クイック スタート:フォルダー内の Python コードを開いて実行する](quickstart-05-python-visual-studio-open-folder.md)」をご覧ください。 ただし、このセクションで説明するように、プロジェクト ファイルを使用する利点があります。
::: moniker-end

> [!Tip]
> プロジェクトを使用しないと、Visual Studio のすべてのバージョンが Python コードで問題なく動作します。 たとえば、Python ファイル自体を開き、オート コンプリート、IntelliSense、デバッグなどの機能を利用できます (エディターで右クリックして、 **[デバッグの開始]** を選択します)。 ただし、このようなコードは常に既定のグローバル環境を使うので、コードが別の環境向けのものである場合は正しくない入力候補やエラーが表示されることがあります。 さらに、Visual Studio は 1 つのファイルが開かれたフォルダー内のすべてのファイルとパッケージを分析するので、かなりの CPU 時間を消費します。
>
> 「[既存ファイルからのプロジェクトの作成](#create-project-from-existing-files)」で説明されているように、既存のコードから Visual Studio プロジェクトを作成すると簡単です。

![ビデオのムービー カメラ アイコン](../install/media/video-icon.png "ビデオを見る") [Deep Dive: Use source control with Python projects](https://youtu.be/Aq8eqApnugM)」(Deep Dive: Python プロジェクトでのソース管理の使用) (youtube.com、8 分 55 秒) もご覧ください。

## <a name="add-files-assign-a-startup-file-and-set-environments"></a>ファイルの追加、スタートアップ ファイルの割り当て、環境の設定

アプリケーションを開発するときは、通常、さまざまな種類の新しいファイルをプロジェクトに追加する必要があります。 プロジェクトを右クリックして **[追加]**  >  **[既存の項目]** を選択すると、追加するファイルを参照できます。また、 **[追加]**  >  **[新しい項目]** を選択すると、さまざまな項目テンプレートがダイアログに表示されます。 [項目テンプレート](python-item-templates.md)のリファレンスで説明されているように、オプションには、空の Python ファイル、Python クラス、単体テスト、Web アプリケーションに関連する各種ファイルなどがあります。 テスト プロジェクトでこれらのオプションを調べ、お使いのバージョンの Visual Studio で使用可能なものについて知ることができます。

Python の各プロジェクトには 1 つのスタートアップ ファイルが割り当てられており、**ソリューション エクスプローラー** では太字で表示されます。 デバッグを開始すると (**F5** キーを押すか、 **[デバッグ]**  >  **[デバッグを開始]** を選択する)、または **対話型** ウィンドウでプロジェクトを実行すると (**Shift**+**Alt**+**F5** キーを押すか、 **[デバッグ]**  >  **[Python Interactive でプロジェクトを実行]** を選択する)、スタートアップ ファイルが実行されます。 これを変更するには、新しいファイルを右クリックして **[スタートアップ アイテムとして設定]** を選択します (または、Visual Studio の古いバージョンでは **[スタートアップ ファイルとして設定]**)。

> [!Tip]
> 選択したスタートアップ ファイルをプロジェクトから削除したが新しいファイルを選択しなかった場合、Visual Studio では、プロジェクトを実行しようとしたときにどの Python ファイルから始めればよいかわかりません。 この場合、Visual Studio 2017 バージョン 15.6 以降ではエラーが表示されます。それより前のバージョンでは、Python インタープリターが実行された出力ウィンドウが開くか、出力ウィンドウは表示されますが、ほぼ瞬時に消失します。 このような動作が発生する場合は、スタートアップ ファイルが割り当てられていることを確認します。
>
> 何らかの理由で出力ウィンドウを開いたままにする場合は、プロジェクトを右クリックし、**[プロパティ]** の **[デバッグ]** タブを選択し、**[インタープリター引数]** フィールドに `-i` を追加します。 この引数により、プログラム完了後にインタープリターは対話モードになり、ユーザーが C **Ctrl**+**Z** > **Enter** キーの順に押して終了するまで、ウィンドウは開いたままになります。

::: moniker range="vs-2017"
新しいプロジェクトは常に既定のグローバル Python 環境と関連付けられます。 プロジェクトを別の環境 (仮想環境を含む) と関連付けるには、プロジェクトで **[Python 環境]** ノードを右クリックし、**[Python 環境の追加/削除]** を選んで、使う環境を選びます。
::: moniker-end
::: moniker range=">=vs-2019"
新しいプロジェクトは常に既定のグローバル Python 環境と関連付けられます。 プロジェクトを別の環境 (仮想環境を含む) と関連付けるには、プロジェクトで **[Python 環境]** ノードを右クリックし、**[環境の追加...]** を選択して、使用する環境を選択します。 ツール バーの環境ドロップダウン コントロールを使用して、環境を選択したり、プロジェクトに別の環境を追加したりすることもできます。

![Python ツール バーの [環境の追加] コマンド](media/environments/environments-toolbar-2019.png)
::: moniker-end

アクティブな環境を変更するには、**ソリューション エクスプローラー** で目的の環境を右クリックして、**[環境をアクティブ化する]** を選びます (次の図を参照)。 詳細については、[プロジェクト用の環境の選択](selecting-a-python-environment-for-a-project.md)に関するページを参照してください。

![Python プロジェクト用の環境のアクティブ化](media/projects-activate-environment.png)

<a name="project-types"></a>

## <a name="project-templates"></a>プロジェクト テンプレート

Visual Studio には、新規に、または既存のコードから、Python プロジェクトをセットアップする複数の方法が用意されています。 テンプレートを使うには、 **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** メニュー コマンドを選択するか、**ソリューション エクスプローラー** でソリューションを右クリックして **[追加]**  >  **[新しいプロジェクト]** を選択します。どちらの場合も、 **[新しいプロジェクト]** ダイアログが表示されます。 Python 固有のテンプレートを表示するには、「Python」を検索するか、 **[インストール済み]**  >  **[Python]** ノードを選択します。

![Python テンプレートが表示されている [新しいプロジェクト] ダイアログ](media/projects-new-project-dialog.png)

::: moniker range="<=vs-2017"

次の表は、Visual Studio 2017 で使うことができるテンプレートをまとめたものです (以前のバージョンでは利用できないテンプレートもあります)。

| Template | 説明 |
| --- | --- |
| [**既存の Python コードから**](#create-project-from-existing-files) | フォルダー構造に存在する既存の Python コードから Visual Studio プロジェクトを作成します。  |
| **Python アプリケーション** | 空のソース ファイルを 1 つ含む新しい Python アプリケーションの基本的なプロジェクト構造です。 既定では、プロジェクトは既定のグローバル環境のコンソール インタープリターで実行します。これは、[異なる環境を割り当てる](selecting-a-python-environment-for-a-project.md)ことで変更できます。 |
| [**Azure クラウド サービス**](python-azure-cloud-service-project-template.md) | Python で記述された Azure クラウド サービス用のプロジェクトです。 |
| [**Web プロジェクト**](python-web-application-project-templates.md) | Bottle、Django、Flask などのさまざまなフレームワークに基づく Web アプリ用のプロジェクトです。 |
| **IronPython アプリケーション** | [Python Application (Python アプリケーション)] テンプレートに似ていますが、IronPython を既定で使って、.NET 相互運用と .NET 言語での混合モード デバッグを可能にします。 |
| **IronPython WPF アプリケーション** | IronPython と、アプリケーションのユーザー インターフェイス用に Windows Presentation Foundation の XAML ファイルを使うプロジェクト構造です。 Visual Studio は XAML UI デザイナーを提供し、コードビハインドを Python で記述でき、アプリケーションはコンソールを表示しないで実行します。 |
| **IronPython Silverlight Web ページ** | Silverlight を使ってブラウザーで実行する IronPython プロジェクトです。 アプリケーションの Python コードは、スクリプトとして Web ページに含まれます。 定型のスクリプト タグは、Silverlight の内部で実行する IronPython を初期化する JavaScript コードを生成し、それによって Python コードは DOM と対話できます。 |
| **IronPython Windows フォーム アプリケーション** | IronPython と、Windows フォームを含むコードを使って作成された UI を使うプロジェクト構造。 アプリケーションはコンソールを表示しないで実行します。 |
| **バックグラウンド アプリケーション (IoT)** | デバイス上でバックグラウンド サービスとして実行する Python プロジェクトの配置をサポートします。 詳しくは、[Windows IoT デベロッパー センター](https://dev.windows.com/en-us/iot)をご覧ください。 |
| **Python 拡張機能モジュール** | このテンプレートは、Visual Studio 2017 以降の Python ワークロードで **Python ネイティブ開発ツール** をインストールしてある場合、Visual C++ の下に表示されます (「[インストール](installing-python-support-in-visual-studio.md)」を参照)。 「[Python 用 C++ 拡張機能の作成](working-with-c-cpp-python-in-visual-studio.md)」で説明されているものに似た、C++ 拡張 DLL のコア構造を提供します。 |
::: moniker-end

::: moniker range=">=vs-2019"

次の表は、Visual Studio 2019 で使うことができるテンプレートをまとめたものです (以前のバージョンでは利用できないテンプレートもあります)。

| Template | 説明 |
| --- | --- |
| [**既存の Python コードから**](#create-project-from-existing-files) | フォルダー構造に存在する既存の Python コードから Visual Studio プロジェクトを作成します。  |
| **Python アプリケーション** | 空のソース ファイルを 1 つ含む新しい Python アプリケーションの基本的なプロジェクト構造です。 既定では、プロジェクトは既定のグローバル環境のコンソール インタープリターで実行します。これは、[異なる環境を割り当てる](selecting-a-python-environment-for-a-project.md)ことで変更できます。 |
| [**Web プロジェクト**](python-web-application-project-templates.md) | Bottle、Django、Flask などのさまざまなフレームワークに基づく Web アプリ用のプロジェクトです。 |
| **IronPython アプリケーション** | [Python Application (Python アプリケーション)] テンプレートに似ていますが、IronPython を既定で使って、.NET 相互運用と .NET 言語での混合モード デバッグを可能にします。 |
| **IronPython WPF アプリケーション** | IronPython と、アプリケーションのユーザー インターフェイス用に Windows Presentation Foundation の XAML ファイルを使うプロジェクト構造です。 Visual Studio は XAML UI デザイナーを提供し、コードビハインドを Python で記述でき、アプリケーションはコンソールを表示しないで実行します。 |
| **IronPython Silverlight Web ページ** | Silverlight を使ってブラウザーで実行する IronPython プロジェクトです。 アプリケーションの Python コードは、スクリプトとして Web ページに含まれます。 定型のスクリプト タグは、Silverlight の内部で実行する IronPython を初期化する JavaScript コードを生成し、それによって Python コードは DOM と対話できます。 |
| **IronPython Windows フォーム アプリケーション** | IronPython と、Windows フォームを含むコードを使って作成された UI を使うプロジェクト構造。 アプリケーションはコンソールを表示しないで実行します。 |
| **バックグラウンド アプリケーション (IoT)** | デバイス上でバックグラウンド サービスとして実行する Python プロジェクトの配置をサポートします。 詳しくは、[Windows IoT デベロッパー センター](https://dev.windows.com/en-us/iot)をご覧ください。 |
| **Python 拡張機能モジュール** | このテンプレートは、Visual Studio 2017 以降の Python ワークロードで **Python ネイティブ開発ツール** をインストールしてある場合、Visual C++ の下に表示されます (「[インストール](installing-python-support-in-visual-studio.md)」を参照)。 「[Python 用 C++ 拡張機能の作成](working-with-c-cpp-python-in-visual-studio.md)」で説明されているものに似た、C++ 拡張 DLL のコア構造を提供します。 |
::: moniker-end

> [!Note]
> Python はインタープリター言語であるため、Visual Studio 内の Python プロジェクトでは、他のコンパイル言語のプロジェクト (C# など) のようにスタンドアロンの実行可能ファイルは生成されません。 詳細については、[質問と回答](overview-of-python-tools-for-visual-studio.md#questions-and-answers)のセクションをご覧ください。

<a name="create-project-from-existing-files"></a>

### <a name="create-a-project-from-existing-files"></a>既存のファイルからプロジェクトを作成する

> [!Important]
> ここで説明するプロセスでは、元のソース ファイルの移動やコピーは行いません。 コピーで作業する場合は、まず、フォルダーを複製します。

[!INCLUDE[project-from-existing](includes/project-from-existing.md)]

## <a name="linked-files"></a>リンク ファイル

リンク ファイルは、プロジェクトに取り込まれますが、通常はアプリケーションのプロジェクト フォルダーの外部に存在するファイルです。 **ソリューション エクスプローラー** では、通常のファイルにショートカットがオーバーレイされたアイコンで示されます。![リンクのあるファイル アイコン](media/projects-linked-file-icon.png)

リンクのあるファイルは、`<Compile Include="...">` 要素を使って *.pyproj* ファイルで指定されます。 リンク ファイルは、ディレクトリ構造外の相対パスを使う場合は暗黙的になり、**ソリューション エクスプローラー** 内のパスを使う場合は明示的となります。

```xml
<Compile Include="..\test2.py">
    <Link>MyProject\test2.py</Link>
</Compile>
```

次のいずれかの条件が満たされると、リンク ファイルは無視されます。

- リンク ファイルに Link メタデータが含まれ、Include 属性で指定されたパスがプロジェクト ディレクトリ内に存在する
- リンク ファイルがプロジェクト階層内に存在するファイルと重複する
- リンク ファイルに Link メタデータが含まれ、リンク パスがプロジェクト階層の外部の相対パスである
- リンク パスがルートになっている

### <a name="work-with-linked-files"></a>リンク ファイルの使用

既存の項目をリンクとして追加するには、ファイルを追加するプロジェクトのフォルダーを右クリックし、 **[追加]**  >  **[既存の項目]** を選びます。 表示されるダイアログで、ファイルを選び、**[追加]** ボタンのドロップダウンから **[リンクとして追加]** を選びます。 競合するファイルがない場合は、選んだフォルダーにリンクが作成されます。 ただし、同じ名前のファイルが既に存在する場合、またはそのファイルへのリンクがプロジェクト内に既に存在する場合は、リンクは追加されません。

プロジェクト フォルダーに既に存在するファイルにリンクしようとした場合は、リンクとしてではなく通常のファイルとして追加されます。 ファイルをリンクに変換するには、 **[ファイル]**  >  **[名前を付けて保存]** を選び、プロジェクト階層外の場所にファイルを保存します。Visual Studio は自動的にそれをリンクに変換します。 同様に、 **[ファイル]**  >  **[名前を付けて保存]** を使ってプロジェクト階層内のどこかにファイルを保存することにより、リンクをファイルに戻すことができます。

**ソリューション エクスプローラー** でリンク ファイルを移動すると、リンクは移動されますが、実際のファイルは影響を受けません。 同様に、リンクを削除すると、リンクだけが削除されて、ファイルには影響ありません。

リンク ファイルの名前を変更することはできません。

## <a name="references"></a>References

Visual Studio のプロジェクトは、プロジェクトと拡張機能への参照の追加をサポートし、参照は **ソリューション エクスプローラー** の **[参照]** ノードに表示されます。

![Python プロジェクトでの拡張機能の参照](media/projects-extension-references.png)

通常、拡張機能の参照は、プロジェクト間の依存関係を示し、設計時に IntelliSense するか、またはコンパイル時にリンクを提供するために使われます。 Python プロジェクトも同様の方法で参照を使いますが、Python の動的な性質のため、主として設計時に強化された IntelliSense を提供するために使われます。 また、追加の依存関係をインストールするために Microsoft Azure への配置で使うこともできます。

### <a name="extension-modules"></a>拡張モジュール

*.pyd* ファイルへの参照により、生成されるモジュールに対する IntelliSense が有効になります。 Visual Studio は *.pyd* ファイルを Python インタープリターに読み込み、その型と関数を調べます。 また、関数でシグネチャ ヘルプを提供するためにドキュメントの文字列の解析を試みます。

ディスクで拡張モジュールが更新された場合、Visual Studio はバックグラウンドでモジュールを再分析します。 このアクションによる実行時動作への影響はありませんが、分析が完了するまで一部の入力候補が使えなくなります。

また、モジュールを含むフォルダーへの[検索パス](search-paths.md)の追加が必要になることもあります。

### <a name="net-projects"></a>.NET プロジェクト

IronPython を使う場合は、.NET アセンブリへの参照を追加して IntelliSense を有効にすることができます。 ソリューション内の .NETプロジェクトの場合は、Python プロジェクトで **[参照]** ノードを右クリックし、**[参照の追加]** を選び、**[プロジェクト]** タブを選んで、目的のプロジェクトを参照します。 別にダウンロードした DLL の場合は、代わりに **[参照]** タブを選び、目的の DLL を参照します。

IronPython での参照は、`clr.AddReference('<AssemblyName>')` への呼び出しが行われるまで使えないので、`clr.AddReference` の適切な呼び出しをアセンブリに追加する必要もあります (通常は、コードの先頭)。 たとえば、Visual Studio で **IronPython Windows フォーム アプリケーション** プロジェクト テンプレートによって作成されるコードには、ファイルの先頭に次の 2 つの呼び出しが含まれます。

```python
import clr
clr.AddReference('System.Drawing')
clr.AddReference('System.Windows.Forms')

from System.Drawing import *
from System.Windows.Forms import *

# Other code omitted
```

### <a name="webpi-projects"></a>WebPI プロジェクト

デプロイ用の WebPI 製品エントリへの参照を Microsoft Azure Cloud Services に追加し、クラウドで WebPI フィードを使って追加コンポーネントをインストールできます。 既定では、表示されるフィードは Python 固有であり、Django、CPython、およびその他の主要なコンポーネントが含まれます。 次に示すように、独自のフィードを選ぶこともできます。 Microsoft Azure に発行すると、セットアップ タスクは参照されているすべての製品をインストールします。

> [!IMPORTANT]
> WebPI プロジェクトは、Visual Studio 2017 または Visual Studio 2019 では使用できません。

![WebPI の参照](media/projects-webPI-components.png)
