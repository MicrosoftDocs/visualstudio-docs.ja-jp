---
title: Python 用 Web アプリケーション テンプレート
description: Visual Studio には、Bottle、Flask、および Django フレームワークを使用する Python Web アプリケーション用のテンプレートが用意されています。サポートには、デバッグの構成や Azure App Service への発行が含まれています。
ms.date: 01/28/2019
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 6553017034dc46cfd1c035564a83dde89d77d057
ms.sourcegitcommit: 4908561809ad397c99cf204f52d5e779512e502c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112254850"
---
# <a name="python-web-application-project-templates"></a>Python Web アプリケーション プロジェクト テンプレート

Visual Studio の Python は、さまざまなフレームワークを処理するように構成できるプロジェクト テンプレートとデバッグ ランチャーにより、Bottle、Flask、Django などのフレームワークでの Web プロジェクトの開発をサポートします。 これらのテンプレートには、必要な依存関係を宣言する *requirements.txt* が含まれています。 これらのテンプレートのいずれかを基にプロジェクトを作成する場合は、それらのパッケージをインストールするように Visual Studio から求められます (この記事で後述する「[プロジェクト要件をインストールする](#install-project-requirements)」を参照してください)。

Pyramid などの他のフレームワークには、汎用の **Web プロジェクト** テンプレートを使用できます。 この場合、フレームワークはテンプレートと一緒にインストールされません。 そのため、プロジェクトで使用する環境に必要なパッケージをインストールします ([「[Python 環境] ウィンドウ」の「[パッケージ] タブ」](python-environments-window-tab-reference.md#packages-tab)を参照してください)。

Python Web アプリを Azure にデプロイする方法については、「[Azure App Service への発行](publishing-python-web-applications-to-azure-from-visual-studio.md)」を参照してください。

## <a name="use-a-project-template"></a>プロジェクト テンプレートを使用する

テンプレートからプロジェクトを作成するには、 **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** の順に作成します。 Web プロジェクト用のテンプレートを表示するには、ダイアログ ボックスの左側で **[Python]**  >  **[Web]** の順に選択します。 プロジェクトとソリューションの名前を指定して必要なテンプレートを選択し、ソリューション ディレクトリと Git リポジトリのオプションを設定し、 **[OK]** を選択します。

![Web アプリ用の新しいプロジェクト ダイアログ](media/projects-new-project-dialog-web.png)

::: moniker range="<=vs-2017"

前述の汎用的な **Web プロジェクト** テンプレートは、空の Visual Studio プロジェクトのみを提供し、コードはなく Python プロジェクトであること以外に前提条件もありません。 **Azure クラウド サービス** テンプレートの詳細については、「[Python 用 Azure クラウド サービス プロジェクト](python-azure-cloud-service-project-template.md)」を参照してください。

::: moniker-end

::: moniker range=">=vs-2019"

前述の汎用的な **Web プロジェクト** テンプレートは、空の Visual Studio プロジェクトのみを提供し、コードはなく Python プロジェクトであること以外に前提条件もありません。

::: moniker-end

その他のテンプレートはすべて、Bottle、Flask、または Django の Web フレームワークに基づいており、次のセクションで説明する 3 つの一般的なグループに分類されます。 このようなテンプレートのいずれかで作成されたアプリには、アプリをローカルで実行およびデバッグするのに必要なコードが含まれています。 また、各テンプレートでは、実稼働 Web サーバーで使用するために必要な [WSGI アプリ オブジェクト](https://www.python.org/dev/peps/pep-3333/) (python.org) も用意されています。

### <a name="blank-group"></a>空白のグループ

**空の \<framework> Web プロジェクト** テンプレートはいずれも、ほぼ最小限の定型コードと、*requirements.txt* ファイルに宣言されている必要な依存関係を使用してプロジェクトを作成します。

| Template | [説明] |
| --- | --- |
| **Blank Bottle Web プロジェクト** | *app.py* に対するホーム ページと、非常に短いインライン ページ テンプレートを使用して `/` にエコーする `/hello/<name>` ページとを備えた最小限のアプリを `<name>` 内に生成します。 |
| **空の Django Web プロジェクト** | コア Django サイト構造を持つが Django アプリが含まれない Django プロジェクトを生成します。 詳細については、[Django テンプレート](python-django-web-application-project-template.md)に関する記事と [Django 手順 1](learn-django-in-visual-studio-step-01-project-and-solution.md)に関する記事を参照してください。 |
| **Blank Flask Web プロジェクト** | "Hello World!" を 1 つ使用した最小限のアプリを生成します。 ページの`/`します。 このアプリは、[クイック スタート: Visual Studio を使用して初めての Python Web アプリを作成](../ide/quickstart-python.md?toc=/visualstudio/python/toc.json&bc=/visualstudio/python/_breadcrumb/toc.json)に関する記事で詳細説明した手順を実行して得られた結果と類似しています。 [Flask の詳細情報の手順 1](learn-flask-visual-studio-step-01-project-solution.md) に関するページも参照してください。

### <a name="web-group"></a>Web グループ

**\<Framework> Web プロジェクト** テンプレートはいずれも、選択したフレームワークに関係なく、同一の設計によるスターター Web アプリを作成します。 アプリにはホーム ページ、バージョン情報ページ、連絡先ページが含まれると共に、ナビゲーション バーとブートス トラップによる応答性に優れたデザインが使用されます。 各アプリはサーバーの静的ファイルに対して適切に構成され (CSS、JavaScript、フォント)、各アプリではフレームワークに適したページ テンプレート メカニズムが使用されます。

| Template | [説明] |
| --- | --- |
| **Bottle Web プロジェクト** | 静的ファイルが *static* フォルダーに含まれていて、*app.py* 内のコードを通して処理されるアプリを生成します。 個々のページに対するルーティングは *routes.py* に含まれており、*views* フォルダーにはページのテンプレートが含まれています。|
| **Django Web プロジェクト** | 3 つのページ、認証サポート、および SQLite データベース (データ モデルはなし) を使用して Django プロジェクトと Django アプリを生成します。 詳細については、[Django テンプレート](python-django-web-application-project-template.md)に関する記事と [Django 手順 4](learn-django-in-visual-studio-step-04-full-django-project-template.md) に関する記事を参照してください。 |
| **Flask Web プロジェクト** | 静的ファイルが *static* フォルダーに含まれていているアプリを生成します。 *views.py* 内のコードによってルーティングが処理され、Jinja エンジンを使用するページ テンプレートが *templates* に含まれています。 *runserver.py* ファイルはスタートアップ コードを提供します。 [Flask の詳細情報の手順 4](learn-flask-visual-studio-step-04-full-flask-project-template.md) に関するページを参照してください。 |
| **Flask/Jade Web プロジェクト** | **Flask Web プロジェクト** テンプレートの場合と同じアプリを、Jinja テンプレート エンジン用の Jade 拡張を使用して生成します。 |

::: moniker range="vs-2017"
### <a name="polls-group"></a>ポーリング グループ

**ポーリング \<framework> Web プロジェクト** テンプレートは、さまざまなポーリングの質問に対してユーザーが投票するために使用するスターター Web アプリを作成します。 各アプリは、**Web** プロジェクト テンプレートの構造に基づいてビルドされ、データベースを使用してポーリングとユーザー応答を管理します。 アプリには適切なデータ モデルと、*samples.json* ファイルからポーリングを読み込む特殊なアプリ ページ ("/seed") とが含まれています。

| Template | [説明] |
| --- | --- |
| **Polls Bottle Web プロジェクト** | `REPOSITORY_NAME` 環境変数を使用して構成されるメモリ内データベース、MongoDB、または Azure テーブル ストレージに対して実行できるアプリを生成します。 データ モデルとデータ ストア コードは *models* フォルダーに含まれ、*settings.py* ファイルには、どのデータ ストアを使用するかを決定するコードが含まれます。 |
| **ポーリング Django Web プロジェクト** | 3 つのページと SQLite データベースを使用して Django プロジェクトと Django アプリを生成します。 認証された管理者がポーリングを作成および管理できるように、Django 管理インターフェイスにカスタマイズを含めます。 詳細については、[Django テンプレート](python-django-web-application-project-template.md)に関する記事と [Django 手順 6](learn-django-in-visual-studio-step-06-polls-django-web-project-template.md) に関する記事を参照してください。 |
| **Polls Flask Web プロジェクト** | `REPOSITORY_NAME` 環境変数を使用して構成されるメモリ内データベース、MongoDB、または Azure テーブル ストレージに対して実行できるアプリを生成します。 データ モデルとデータ ストア コードは *models* フォルダーに含まれ、*settings.py* ファイルには、どのデータ ストアを使用するかを決定するコードが含まれます。 アプリでは、ページ テンプレートに対して Jinja エンジンが使用されます。 [Flask の詳細情報の手順 5](learn-flask-visual-studio-step-05-polls-flask-web-project-template.md) に関するページを参照してください。 |
| **Polls Flask/Jade Web プロジェクト** | **Polls Flask Web プロジェクト** テンプレートの場合と同じアプリを、Jinja テンプレート エンジン用の Jade 拡張を使用して生成します。 |
::: moniker-end

## <a name="install-project-requirements"></a>プロジェクト要件をインストールする

フレームワーク固有のテンプレートからプロジェクトを作成する場合、pip を使用して必要なパッケージをインストールするためのダイアログが表示されます。 Web プロジェクトの[仮想環境](selecting-a-python-environment-for-a-project.md#use-virtual-environments)を使用して、Web サイトのパブリッシュ時に正しい依存関係が含まれるようにすることもお勧めします。

![プロジェクト テンプレートに必要なパッケージをインストールするダイアログ](media/template-web-requirements-txt-wizard.png)

ソース管理を使用している場合、仮想環境は *requirements.txt* でしか再作成できないので、仮想環境フォルダーは通常は省略されます。 そのフォルダーを除外する最善の方法としては、上に示したプロンプト内で **[I will install them myself]\(自分でインストールする\)**  を選択して、仮想環境を作成する前に自動コミットを無効にします。 詳細については、[Django のチュートリアル - 手順 1-2 および手順 1-3](learn-django-in-visual-studio-step-01-project-and-solution.md#step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository) に関するページと [Flask のチュートリアル - 手順 1-2 および手順 1-3](learn-flask-visual-studio-step-01-project-solution.md#step-1-2-examine-the-git-controls-and-publish-to-a-remote-repository) に関するページを参照してください。

Microsoft Azure App Service にデプロイする場合は、Python のバージョンとして[サイト拡張機能](./managing-python-on-azure-app-service.md?view=vs-2019&preserve-view=true)を選び、パッケージを手動でインストールします。 また、Azure App Service は、Visual Studio からデプロイされるときに *requirements.txt* ファイルからパッケージを自動的にインストール **しない** ため、[aka.ms/PythonOnAppService](managing-python-on-azure-app-service.md) の構成の詳細に従ってください。

::: moniker range="<=vs-2017"

Microsoft Azure Cloud Services は *requirements.txt* ファイルをサポート *します*。 詳細については、[Azure クラウド サービス プロジェクト](python-azure-cloud-service-project-template.md)に関する記事をご覧ください。

::: moniker-end

## <a name="debugging"></a>デバッグ

Web プロジェクトのデバッグが開始されると、Visual Studio はローカル Web サーバーをランダムなポート上で起動し、そのアドレスとポートを既定のブラウザーで開きます。 追加のオプションを指定するには、プロジェクトを右クリックし、 **[プロパティ]** を選択し、 **[Web ランチャー]** タブを選択します。

![一般的な Web テンプレートの Web ランチャーのプロパティ](media/template-web-launcher-properties.png)

**[デバッグ]** グループで、次の操作を実行します。

- **[検索パス]** 、 **[スクリプトの引数]** 、 **[インタープリターの引数]** 、 **[インタープリター パス]** : これらのオプションは、[通常のデバッグ](debugging-python-in-visual-studio.md)の場合と同じです。
- **[起動 URL]** : ブラウザーで開かれる URL を指定します。 既定値は `localhost` です。
- **[ポート番号]** : URL に何も指定されなかった場合に使用するポート (Visual Studio によって既定で自動的に選択されます)。 この設定により、ローカル デバッグ サーバーがリッスンするポートを構成するためにテンプレートで使用される `SERVER_PORT` 環境変数の既定値をオーバーライドできます。

**[サーバー コマンドの実行]** と **[サーバー コマンドのデバッグ]** グループ (後者はイメージに表示されている内容の下にあります) のプロパティによって、Web サーバーの起動方法が決定されます。 多くのフレームワークでは、現在のプロジェクトの外部のスクリプトを使用する必要があるため、スクリプトをここで構成でき、スタートアップ モジュールの名前をパラメーターとして渡すことができます。

- **[コマンド]** : Python スクリプト ( *\*.py* ファイル)、モジュール名 (`python.exe -m module_name` など)、または 1 行のコード (`python.exe -c "code"` など) にすることができます。 ドロップダウンの値は、これらの種類のどれが対象であるかを示します。
- **[引数]** : これらの引数は、コマンド ラインでコマンドに続いて渡されます。
- **[環境]** : 環境変数を指定する \<NAME>=\<VALUE> ペアの改行区切りリスト。 これらの変数は、ポート番号や検索パスなど、環境を変更できるすべてのプロパティの後に設定されるため、これらの値を上書きできます。

MSBuild 構文を使用して任意のプロジェクト プロパティまたは環境変数を指定できます。例: `$(StartupFile) --port $(SERVER_PORT)`。
`$(StartupFile)` はスタートアップ ファイルの相対パスで、`{StartupModule}` はスタートアップ ファイルのインポート可能な名前です。 `$(SERVER_HOST)` と `$(SERVER_PORT)` は、 **[起動 URL]** プロパティと **[ポート番号]** プロパティによって自動的に設定されるか、 **[環境]** プロパティによって設定される通常の環境変数です。

> [!Note]
> **[サーバー コマンドの実行]** の値は、 **[デバッグ]**  >  **[サーバーを起動します]** コマンドまたは **Ctrl**+**F5** キーで使用されます。 **[サーバー コマンドのデバッグ]** グループは、 **[デバッグ]**  >  **[デバッグ サーバーの開始]** コマンドまたは **F5** キーで使用されます。

### <a name="sample-bottle-configuration"></a>サンプルの Bottle 構成

**Bottle Web プロジェクト** テンプレートには、必要な構成を実行する定型コードが含まれています。 ただし、インポートされた bottle アプリにはこのコードが含まれていない場合があります、その場合、次の設定はインストールされた `bottle` モジュールを使用してアプリを起動します。

- **[Run Server Command (サーバー コマンドの実行)]** グループ:
  - **[コマンド]** : `bottle` (モジュール)
  - **[引数]** : `--bind=%SERVER_HOST%:%SERVER_PORT% {StartupModule}:app`

- **[Debug Server Command (サーバー コマンドのデバッグ)]** グループ:
  - **[コマンド]** : `bottle` (モジュール)
  - **[引数]** `--debug --bind=%SERVER_HOST%:%SERVER_PORT% {StartupModule}:app`

デバッグに Visual Studio を使用する場合、`--reload` オプションはお勧めしません。

### <a name="sample-pyramid-configuration"></a>サンプルの Pyramid 構成

Pyramid アプリは、現在、`pcreate` コマンドライン ツールを使用して作成するのが最適です。 アプリが作成されたら、[ **[既存の Python コードから]**](managing-python-projects-in-visual-studio.md#create-a-project-from-existing-files) テンプレートを使用してインポートできます。 その後、 **[汎用 Web プロジェクト]** カスタマイズを選択してオプションを構成します。 これらの設定は、Pyramid が `..\env` にある仮想環境にインストールされていることを想定しています。

- **[デバッグ]** グループ:
  - **[サーバー ポート]** : 6543 (または *.ini* ファイルで構成されているポート)

- **[Run Server Command (サーバー コマンドの実行)]** グループ:
  - コマンド: `..\env\scripts\pserve-script.py` (スクリプト)
  - 引数: `Production.ini`

- **[Debug Server Command (サーバー コマンドのデバッグ)]** グループ:
  - コマンド: `..\env\scripts\pserve-script.py` (スクリプト)
  - 引数: `Development.ini`

> [!Tip]
> Pyramid アプリのフォルダーは、通常、プロジェクト ルートの 1 レベル下に位置するため、プロジェクトの **[作業ディレクトリ]** プロパティを構成することが必要な場合があります。

### <a name="other-configurations"></a>その他の構成

別のフレームワークの設定を共有する場合、または別のフレームワークの設定を要求する場合は、[GitHub で懸案事項](https://github.com/Microsoft/PTVS/issues)を開きます。

::: moniker range="<=vs-2017"

## <a name="convert-a-project-to-azure-cloud-service"></a>プロジェクトを Azure クラウド サービス プロジェクトに変換する

**[Microsoft Azure クラウド サービス プロジェクトに変換]** コマンド (下図) は、クラウド サービス プロジェクトをソリューションに追加します。 このプロジェクトには、使用する仮想マシンとサービスのデプロイ設定と構成が含まれています。 クラウド プロジェクトで **[発行]** コマンドを使用して、Cloud Services にデプロイします。Python プロジェクトの **[発行]** コマンドでは、引き続き Web サイトにデプロイされます。 詳細については、[Azure クラウド サービス プロジェクト](python-azure-cloud-service-project-template.md)に関する記事を参照してください。

![[Microsoft Azure クラウド サービス プロジェクトに変換] コマンド](media/template-web-convert-menu.png)

::: moniker-end

## <a name="see-also"></a>参照

- [Python 項目テンプレートのリファレンス](python-item-templates.md)
- [Azure App Service に発行する](publishing-python-web-applications-to-azure-from-visual-studio.md)