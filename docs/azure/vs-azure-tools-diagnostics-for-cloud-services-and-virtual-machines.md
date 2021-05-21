---
title: 診断 - Azure Cloud Services と VM
ms.custom: SEO-VS-2020
description: Visual Studio で Azure クラウド サービスと仮想マシン (VM) をデバッグするための診断を設定する方法について説明します。
author: ghogen
manager: jmartens
ms.topic: conceptual
ms.workload: azure-vs
ms.date: 06/28/2018
ms.author: mikejo
ms.openlocfilehash: e98d335d53edb7e8771db3314944a11c534d046b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844308"
---
# <a name="set-up-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Azure クラウド サービスと仮想マシンに対する診断を設定する
Azure クラウド サービスまたは Azure 仮想マシンのトラブルシューティングを行うときは、Visual Studio を使用して Azure Diagnostics を簡単に構成できます。 診断は、クラウド サービスを実行する仮想マシンと仮想マシン インスタンスのシステム データとログ データを取り込みます。 診断データは、選択したストレージ アカウントに転送されます。 Azure での診断ログの詳細については、「[Azure App Service の Web アプリの診断ログの有効化](/azure/app-service/web-sites-enable-diagnostic-log)」を参照してください。

この記事では、Visual Studio を使用して、Azure Diagnostics を有効にして設定する方法を示します。診断は、デプロイの前と後のどちらでも有効にできます。 Azure 仮想マシンで診断を設定する方法、収集する診断情報の種類を選択する方法、および収集された情報を表示する方法についても取り上げます。

Azure Diagnostics を設定するには、次のオプションのいずれかを使用できます。

* Visual Studio の **[診断構成]** ダイアログ ボックスで、診断設定を変更します。 この設定は、diagnostics.wadcfgx という名前のファイルに保存されます (Azure SDK 2.4 以前は、このファイルは diagnostics.wadcfg という名前でした)。 構成ファイルを直接変更することもできます。 ファイルを直接更新した場合、構成の変更内容は、次回 Azure にクラウド サービスをデプロイしたとき、またはエミュレーターでサービスを実行したときに有効になります。
* Visual Studio で Cloud Explorer またはサーバー エクスプローラーを使用して、実行中のクラウド サービスまたは仮想マシンの診断設定を変更します。

## <a name="azure-sdk-26-diagnostics-changes"></a>Azure SDK 2.6 での診断の変更
Visual Studio では、Azure SDK 2.6 以降のプロジェクトには、次の変更が適用されます。

* ローカル エミュレーターで診断がサポートされるようになりました。 つまり、Visual Studio での開発およびテスト時に診断データを収集し、開発中のアプリケーションが正しくトレースを作成することを確認できます。 接続文字列 `UseDevelopmentStorage=true` により、Visual Studio で Azure ストレージ エミュレーターを使用してクラウド サービス プロジェクトを実行している間に行われる診断データの収集が有効になります。 すべての診断データは、開発ストレージのストレージ アカウントに収集されます。
* 診断ストレージ アカウントの接続文字列 `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` は、サービス構成 (.cscfg) ファイルに格納されます。 Azure SDK 2.5 では、診断ストレージ アカウントは diagnostics.wadcfgx ファイルに指定されます。

接続文字列は、Azure SDK 2.6 以降と Azure SDK 2.4 以前では、いくつかの重要な点で動作が異なります。

* Azure SDK 2.4 以前では、接続文字列は、診断プラグインが診断ログを転送するためのストレージ アカウント情報を取得する目的でランタイムとして使用されます。
* Azure SDK 2.6 以降では、Visual Studio が診断接続文字列を使用して、発行時に Azure Diagnostics 拡張機能を適切なストレージ アカウント情報で設定します。 接続文字列を使用して、Visual Studio が発行時に使用するさまざまなサービス構成に対して、異なるストレージ アカウントを定義できます。 ただし、Azure SDK 2.5 以降は診断プラグインを使用できないため、.cscfg ファイルだけでは診断拡張機能を設定することはできません。 拡張機能は、Visual Studio や PowerShell などのツールを使用して、別途設定する必要があります。
* PowerShell を使用した診断拡張機能の設定プロセスを単純化するために、Visual Studio からの出力パッケージには、各ロールの診断拡張機能用のパブリック構成 XML が含まれます。 Visual Studio は、診断接続文字列を使用して、パブリック構成内のストレージ アカウント情報を取り込みます。 パブリック構成ファイルは、拡張機能フォルダーに作成されます。 パブリック構成ファイルには、PaaSDiagnostics.&lt;ロール名\>.PubConfig.xml のパターンで名前が付けられます。 このパターンを PowerShell ベースのデプロイで使用すれば、各構成をロールにマップすることができます。
* [Azure ポータル](https://portal.azure.com)は、.cscfg ファイル内の接続文字列を使用して診断データにアクセスします。 データは **[監視]** タブに表示されます。ポータルで監視データを詳細出力するようにサービスを設定するには、接続文字列が必要です。

## <a name="migrate-projects-to-azure-sdk-26-and-later"></a>プロジェクトを Azure SDK 2.6 以降に移行する
Azure SDK 2.5 から Azure SDK 2.6 以降に移行するとき、.wadcfgx ファイルに指定した診断ストレージ アカウントがある場合は、そのストレージ アカウントがそのファイルにそのまま残ります。 さまざまなストレージ構成で異なるストレージ アカウントを使用できる柔軟性を活用するには、接続文字列をプロジェクトに手動で追加します。 Azure SDK 2.4 以前から Azure SDK 2.6 にプロジェクトを移行する場合、診断接続文字列は保持されます。 ただし、前のセクションで説明したように、Azure SDK 2.6 では接続文字列の扱いが変更されているので注意してください。

### <a name="how-visual-studio-determines-the-diagnostics-storage-account"></a>使用する診断ストレージ アカウントを Visual Studio がどのように決定するか
* 診断接続文字列が .cscfg ファイルに指定されている場合、Visual Studio は、発行時と、パッケージ化中のパブリック構成 XML ファイルの生成時に、.cscfg ファイルに指定されている診断接続文字列を使用して診断拡張機能を設定します。
* 診断接続文字列が .cscfg ファイルに指定されていない場合、Visual Studio は、発行時と、パッケージ化中のパブリック構成 XML ファイルの生成時に、.wadcfgx ファイルに指定されているストレージ アカウントを使用して診断拡張機能を設定します。
* .cscfg ファイルの診断接続文字列は、.wadcfgx ファイルのストレージ アカウントよりも優先されます。 診断接続文字列が .cscfg ファイルに指定されている場合、Visual Studio はその接続文字列を使用し、.wadcfgx のストレージ アカウントを無視します。

### <a name="what-does-the-update-development-storage-connection-strings-check-box-do"></a>[...開発ストレージの接続文字列を...更新する] チェック ボックスは何をしますか。
**[Microsoft Azure への公開時に診断とキャッシュのための開発ストレージの接続文字列を Microsoft Azure ストレージ アカウントの資格情報で更新する]** チェック ボックスは、開発ストレージ アカウントの接続文字列を、発行時に指定した Azure ストレージ アカウントに更新する便利な方法です。

たとえば、このチェック ボックスを選択し、診断接続文字列に `UseDevelopmentStorage=true` を指定した場合、プロジェクトを Azure に発行すると、Visual Studio によって、診断接続文字列が発行ウィザードで指定したストレージ アカウントに自動的に更新されます。 ただし、実際のストレージ アカウントが診断接続文字列として指定されている場合は、そのアカウントが使用されます。

## <a name="diagnostics-functionality-differences-in-azure-sdk-24-and-earlier-vs-azure-sdk-25-and-later"></a>Azure SDK 2.4 以前と Azure SDK 2.5 以降の診断機能の違い
プロジェクトを Azure SDK 2.4 以前から Azure SDK 2.5 以降にアップグレードする場合、次の診断機能の違いに留意してください。

* **構成 API は非推奨になりました**。 Azure SDK 2.4 以前のバージョンでは、プログラムから診断を構成できましたが、Azure SDK 2.5 以降ではプログラムによる診断の構成は非推奨扱いとなりました。 現在、診断の構成をコードで定義している場合、その診断機能を引き続き利用するためには、移行したプロジェクトでそれらの設定を最初から構成し直す必要があります。 Azure SDK 2.4 の診断構成ファイルは diagnostics.wadcfg です。 Azure SDK 2.5 以降の診断構成ファイルは diagnostics.wadcfgx です。
* **クラウド サービス アプリケーションの診断はロール レベルでのみ構成できます**。 Azure SDK 2.5 以降、クラウド サービス アプリケーションの診断は、インスタンス レベルでは設定できません。
* **アプリを配置するたびに、診断構成が更新されます**。 これにより、Visual Studio サーバー エクスプローラーで診断構成を変更してからアプリを再デプロイした場合、パリティの問題が発生する可能性があります。
* **Azure SDK 2.5 以降、クラッシュ ダンプは、コードではなく、診断構成ファイル内に構成されます**。 クラッシュ ダンプをコードで構成している場合は、構成をコードから構成ファイルに手動で転送する必要があります。 クラッシュ ダンプは、Azure SDK 2.6 への移行中に転送されることはありません。

## <a name="turn-on-diagnostics-in-cloud-service-projects-before-you-deploy-them"></a>クラウド サービス プロジェクトをデプロイする前に診断を有効にする
サービスをデプロイする前にエミュレーターで実行するとき、Azure で実行するロールの診断データを Visual Studio で収集できます。 Visual Studio で診断設定に対して行った変更はすべて、diagnostics.wadcfgx 構成ファイルに保存されます。 これらの設定で、クラウド サービスのデプロイ時に診断データが保存されるストレージ アカウントを指定します。

[!INCLUDE [cloud-services-wad-warning](./includes/cloud-services-wad-warning.md)]

### <a name="to-turn-on-diagnostics-in-visual-studio-before-deployment"></a>デプロイ前に Visual Studio で診断を有効にするには

1. ロールのショートカット メニューで **[プロパティ]** を選択します。 ロールの **[プロパティ]** ダイアログ ボックスで、**[構成]** タブを選択します。
2. **[診断]** セクションで **[診断を有効にする]** チェック ボックスがオンになっていることを確認します。

    ![[診断の有効化] オプションにアクセスする](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. 診断データ用のストレージ アカウントを指定するには、省略記号 (...) ボタンを選択します。

    ![Specify the storage account to use](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. Azure ストレージ エミュレーター、Azure サブスクリプション、手動で入力した資格情報のうち、どれを使って接続するかを **[ストレージ接続文字列の作成]** ダイアログ ボックスで指定します。

    ![Storage account dialog box](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)

   * **[Microsoft Azure ストレージ エミュレーター]** を選択した場合、接続文字列は `UseDevelopmentStorage=true` に設定されます。
   * **[サブスクリプション]** オプションを選択した場合は、使用する Azure サブスクリプションを選択し、アカウント名を入力できます。 Azure サブスクリプションを管理するには、**[アカウントの管理]** を選択します。
   * **[手動で入力された資格情報]** オプションを選択した場合は、使用する Azure アカウントの名前とキーを入力します。
5. **[診断構成]** ダイアログ ボックスを表示するには、**[構成]** を選択します。 **[全般]** と **[ログ ディレクトリ]** を除く各タブは、収集できる診断データのソースを表します。 既定の **[全般]** タブでは、診断データの収集オプションとして、**[エラーのみ]**、**[すべての情報]**、**[カスタム プラン]** を指定できます。 既定の **[エラーのみ]** オプションでは、警告またはトレース メッセージが転送されないため、必要とするストレージ容量が最小限で済みます。 **[すべての情報]** オプションは最も多くの情報を転送し、最も多くのストレージを使用するため、コストが最も高いオプションです。

   > [!NOTE]
   > [ディスク クォータ (MB)] のサポートされる最小サイズは 50 MB で、既定のサイズは 4 GB です。 ただし、メモリ ダンプを収集する場合は、10 GB のような高い値に増やしてください。
   >

    ![Enable Azure diagnostics and configuration](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. この例では、**[カスタム プラン]** オプションを選択して、収集するデータをカスタマイズできるようにします。
7. **[ディスク クォータ (MB)]** ボックスに、ストレージ アカウントで診断データ用に割り当てる容量を設定できます。 既定の値を変更することも、そのまま使用することもできます。
8. 収集する診断データに対応する各タブで、 **[\<log type\> の転送を有効にする]** チェック ボックスをオンにします。 たとえば、アプリケーション ログを収集する場合は、**[アプリケーション ログ]** タブで **[アプリケーション ログの転送を有効にする]** チェック ボックスをオンにします。 それ以外にも、診断データの種類ごとに必要な情報があれば指定します。 各タブの構成情報については、この記事の後半にある「**診断データのソースを構成する**」セクションを参照してください。
9. 目的の診断データの収集をすべて有効にしたら、**[OK]** を選択します。
10. Visual Studio で Azure クラウド サービス プロジェクトを通常どおり実行します。 アプリケーションを使用すると、有効にしたログ情報が、指定した Azure ストレージ アカウントに保存されます。

## <a name="turn-on-diagnostics-on-azure-virtual-machines"></a>Azure 仮想マシンの診断を有効にする
Azure 仮想マシンの診断データを Visual Studio で収集できます。

### <a name="to-turn-on-diagnostics-on-azure-virtual-machines"></a>Azure 仮想マシンの診断を有効にするには

1. サーバー エクスプローラーで [Azure] ノードを選択し、まだ接続していない場合は Azure サブスクリプションに接続します。
2. **[Virtual Machines]** ノードを展開します。 新しい仮想マシンを作成するか、既存のノードを選択できます。
3. 目的の仮想マシンのショートカット メニューで **[構成]** を選択します。 [仮想マシンの構成] ダイアログ ボックスが表示されます。

    ![Azure 仮想マシンを構成する](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. Microsoft Monitoring Agent 診断拡張機能がまだインストールされていない場合は追加します。 この拡張機能で、Azure 仮想マシンに関する診断データを収集することができます。 **[インストールされている拡張機能]** の下の **[使用可能な拡張機能を選択してください]** ドロップダウン リスト ボックスで、**[Microsoft Monitoring Agent 診断]** を選択します。

    ![Azure 仮想マシン拡張機能をインストールする](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)

    > [!NOTE]
   > 他の診断拡張機能も仮想マシンで使用できます。 詳細については、「[Windows 用の仮想マシン拡張機能とその機能](/azure/virtual-machines/windows/extensions-features)」を参照してください。
   >
   >
5. 拡張機能を追加してその **[診断構成]** ダイアログ ボックスを表示するには、**[追加]** を選択します。
6. ストレージ アカウントを指定するには、**[構成]** を選択し、**[OK]** を選択します。

    **[全般]** と **[ログ ディレクトリ]** を除く各タブは、収集できる診断データのソースを表します。

    ![Enable Azure diagnostics and configuration](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)

    既定の **[全般]** タブでは、診断データの収集オプションとして、**[エラーのみ]**、**[すべての情報]**、**[カスタム プラン]** を指定できます。 既定のオプションの **[エラーのみ]** では、警告またはトレース メッセージを転送しないため、必要とするストレージ容量が最小限で済みます。 **[すべての情報]** オプションは転送する情報量が最も多いため、ストレージ コストが最も高いオプションです。
7. この例では、収集するデータをカスタマイズできるよう、**[カスタム プラン]** オプションを選択します。
8. **[ディスク クォータ (MB)]** ボックスでは、ストレージ アカウントで診断データ用に割り当てる容量を指定します。 既定の値は必要に応じて変更可能です。
9. 収集する診断データに対応する各タブで、**[\<log type\> の転送を有効にする]** チェック ボックスをオンにします。

    たとえば、アプリケーション ログを収集する場合は、 **[アプリケーション ログ]** タブで **[アプリケーション ログの転送を有効にする]** チェック ボックスをオンにします。それ以外にも、診断データの種類ごとに必要な情報があれば指定します。 各タブの構成情報については、この記事の後半にある「**診断データのソースを構成する**」セクションを参照してください。
10. 目的の診断データの収集をすべて有効にしたら、**[OK]** を選択します。
11. 更新したプロジェクトを保存します。

    **[Microsoft Azure のアクティビティ ログ]** ウィンドウのメッセージに、仮想マシンが更新されたことが示されます。

## <a name="set-up-diagnostics-data-sources"></a>診断データのソースを構成する
診断データの収集を有効にしたら、収集対象のデータ ソースと収集する情報を厳密に選択できます。 以降のセクションでは、**[診断構成]** ダイアログ ボックスの各タブと各構成オプションの意味について説明します。

### <a name="application-logs"></a>アプリケーション ログ
アプリケーション ログには Web アプリケーションによって生成された診断情報が記録されます。 アプリケーション ログを取り込む場合は、**[アプリケーション ログの転送を有効化]** チェック ボックスをオンにします。 ストレージ アカウントへのアプリケーション ログの転送間隔を増減するには、**[転送間隔 (分)]** の値を変更します。 ログに取り込む情報の量も、**[ログ レベル]** の値を設定することによって変更できます。 たとえば、取り込む情報の量を増やすには **[詳細]** を、重要なエラーのみ取り込むには **[重大]** を選択します。 アプリケーション ログを出力する特定の診断プロバイダーがある場合は、プロバイダーの GUID を **[プロバイダー GUID]** ボックスに追加することでログを取り込むことができます。

  ![アプリケーション ログ](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

アプリケーション ログの詳細については、「[Azure App Service の Web アプリの診断ログの有効化](/azure/app-service/web-sites-enable-diagnostic-log)」を参照してください。

### <a name="windows-event-logs"></a>Windows イベント ログ
Windows イベント ログを取り込むには、**[Windows イベント ログの転送を有効にする]** チェック ボックスをオンにします。 ストレージ アカウントへのイベント ログの転送間隔を増減するには、**[転送間隔 (分)]** の値を変更します。 追跡するイベントの種類に該当するチェック ボックスをオンにしてください。

![イベント ログ](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Azure SDK 2.6 以降を使用している場合、カスタム データ ソースを指定するには、 **[\<Data source name\>]** テキスト ボックスにそれを入力し、 **[追加]** をクリックします。 指定したデータ ソースが diagnostics.cfcfg ファイルに追加されます。

Azure SDK 2.5 を使用している場合、カスタム データ ソースを指定するには、次の例のように、diagnostics.wadcfgx ファイルの `WindowsEventLog` セクションに目的のデータ ソースを追加できます。

```xml
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```

### <a name="performance-counters"></a>パフォーマンス カウンター
パフォーマンス カウンターの情報は、システムのボトルネックを特定して、システムとアプリケーションのパフォーマンスを微調整するのに役立ちます。 詳細については、「[Azure アプリケーションでのパフォーマンス カウンターの作成と使用](/azure/cloud-services/diagnostics-performance-counters)」を参照してください。 パフォーマンス カウンターを取り込むには、**[パフォーマンス カウンターの転送を有効にする]** チェック ボックスをオンにします。 ストレージ アカウントへのイベント ログの転送間隔を増減するには、**[転送間隔 (分)]** の値を変更します。 追跡するパフォーマンス カウンターに該当するチェック ボックスをオンにしてください。

![パフォーマンス カウンター](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

リストにないパフォーマンス カウンターを追跡するには、構文の候補を使用してパフォーマンス カウンターを入力し、 **[追加]** を選択します。 追跡できるパフォーマンス カウンターは、仮想マシンのオペレーティング システムによって決まります。構文の詳細については、「[カウンター パスの指定](/windows/win32/perfctrs/specifying-a-counter-path)」を参照してください。

### <a name="infrastructure-logs"></a>インフラストラクチャ ログ
インフラストラクチャ ログには、Azure 診断インフラストラクチャ、RemoteAccess モジュール、および RemoteForwarder モジュールに関する情報があります。 インフラストラクチャ ログに関する情報を収集するには、**[インフラストラクチャ ログの転送を有効にする]** チェック ボックスをオンします。 ストレージ アカウントへのインフラストラクチャ ログの転送間隔を増減するには、**[転送間隔 (分)]** の値を変更します。

![診断インフラストラクチャ ログ](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

詳細については、「[Azure Diagnostics を使用したログ データの収集](/azure/cloud-services/cloud-services-dotnet-diagnostics)」を参照してください。

### <a name="log-directories"></a>[ログ ディレクトリ]
ログ ディレクトリには、インターネット インフォメーション サービス (IIS) の要求、失敗した要求、または選択したフォルダーのログ ディレクトリから収集されたデータがあります。 ログ ディレクトリを取り込むには、**[ログ ディレクトリの転送を有効にする]** チェック ボックスをオンにします。 ストレージ アカウントへのログの転送間隔を増減するには、**[転送間隔 (分)]** の値を変更します。

**[IIS ログ]** や **[失敗した要求ログ]** など、収集するログのチェック ボックスを選択します。 既定のストレージ コンテナー名が指定されていますが、必要に応じて名前を変更できます。

任意のフォルダーからログを取り込むことができます。 **[絶対ディレクトリのログ]** セクションにパスを指定し、**[ディレクトリの追加]** を選択します。 ログは指定したコンテナーに取り込まれます。

![[ログ ディレクトリ]](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>ETW ログ
[[Windows イベント トレーシング]](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx)(ETW) を使用している場合、ETW ログを取り込むには、**[ETW のログの転送を有効にする]** チェック ボックスをオンにします。 ストレージ アカウントへのログの転送間隔を増減するには、**[転送間隔 (分)]** の値を変更します。

イベントは、指定したイベント ソースおよびイベント マニフェストから取り込まれます。 イベント ソースを指定するには、**[イベント ソース]** セクションで名前を入力し、**[イベント ソースの追加]** を選択します。 同様に、**[イベント マニフェスト]** セクションでイベント マニフェストを指定し、**[イベント マニフェストの追加]** を選択できます。

![ETW ログ](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

[System.Diagnostics.aspx](/dotnet/api/system.diagnostics) 名前空間のクラスを通して ASP.NET で ETW フレームワークがサポートされています。 Microsoft.WindowsAzure.Diagnostics は、標準の [System.Diagnostics.aspx](/dotnet/api/system.diagnostics) クラスを継承して拡張する名前空間です。この名前空間では、Azure 環境のログ記録フレームワークとして [System.Diagnostics.aspx](/dotnet/api/system.diagnostics) を使用できます。 詳細については、[Microsoft Azure でログ記録とトレースを制御する方法](/archive/msdn-magazine/2010/june/msdn-magazine-cloud-diagnostics-take-control-of-logging-and-tracing-in-windows-azure)と [Azure クラウドサービスと仮想マシンでの診断の有効化](/azure/cloud-services/cloud-services-dotnet-diagnostics)に関するページを参照してください。

### <a name="crash-dumps"></a>クラッシュ ダンプ
ロール インスタンスがクラッシュしたときの情報を取り込むには、**[クラッシュ ダンプの転送を有効にする]** チェック ボックスをオンにします。 (ASP.NET によってほとんどの例外が処理されるため、これは一般的に worker ロールに対してのみ機能します)。クラッシュ ダンプに充てる記憶域スペースの割合を増減するには、 **[ディレクトリのクォータ (%)]** の値を変更します。 クラッシュ ダンプが保存されるストレージ コンテナーを変更でき、ダンプの種類として **[フル]** または **[ミニ]** を選択できます。

次のスクリーンショットは、現在追跡されているプロセスを一覧表示しています。 取り込むプロセスのチェック ボックスをオンにしてください。 別のプロセスを一覧に追加するには、プロセス名を入力し、**[プロセスの追加]** を選択します。

![クラッシュ ダンプ](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

詳細については、[Microsoft Azure でログ記録とトレースを制御する方法](/archive/msdn-magazine/2010/june/msdn-magazine-cloud-diagnostics-take-control-of-logging-and-tracing-in-windows-azure)と [Microsoft Azure Diagnostics (第 4 部: カスタム ログ コンポーネントと Azure Diagnostics 1.3 の変更点)](https://www.red-gate.com/simple-talk/cloud/platform-as-a-service/microsoft-azure-diagnostics-part-4-custom-logging-components-and-azure-diagnostics-1.3-changes/) に関するページを参照してください。

## <a name="view-the-diagnostics-data"></a>診断データの表示
クラウド サービスまたは仮想マシンの診断データを収集したら、そのデータを表示することができます。

### <a name="to-view-cloud-service-diagnostics-data"></a>クラウド サービスの診断データを表示するには
1. クラウド サービスを通常どおりにデプロイして実行します。
2. Visual Studio が生成するレポートまたはストレージ アカウントのテーブルのどちらでも診断データを表示できます。 レポートのデータを表示するには、Cloud Explorer またはサーバー エクスプローラーを開き、目的のロールのノードのショートカット メニューを開いて、**[診断データの表示]** を選択します。

    ![診断データを表示する](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)

    利用可能なデータを示したレポートが表示されます。

    ![Visual Studio の Microsoft Azure Diagnostics レポート](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)

    最新のデータが表示されない場合は、転送間隔が経過するまで待ちます。

    データをすぐに更新するには、**[更新]** リンクを選択します。 データを自動的に更新するには、**[自動更新]** ドロップダウン リスト ボックスで間隔を選択します。 エラー データをエクスポートするには、**[CSV にエクスポート]** ボタンをクリックして、Excel ワークシートで開くことができるコンマ区切り値ファイルを作成します。

    Cloud Explorer またはサーバー エクスプローラーで、対象のデプロイに関連付けられたストレージ アカウントを開きます。
3. テーブル ビューアーで診断テーブルを開き、収集したデータを確認します。 IIS ログおよびカスタム ログについては、BLOB コンテナーを開くことができます。 次の表に、異なるログ ファイルのデータを含むテーブルまたは BLOB コンテナーの一覧を示します。 テーブルの項目には、ログ ファイルのデータだけでなく、**EventTickCount**、**DeploymentId**、**Role**、および **RoleInstance** が含まれており、どの仮想マシンとロールがデータがいつ生成したかを特定できます。

   | 診断データ | 説明 | 場所 |
   | --- | --- | --- |
   | アプリケーション ログ |コードが **System.Diagnostics.Trace** クラスのメソッドを呼び出すことで生成するログ。 |WADLogsTable |
   | イベント ログ |仮想マシンの Windows イベント ログから生成されるデータ。 Windows がこれらのログに情報を格納しますが、アプリケーションやサービスも、このログを使用してエラーまたはログ情報を報告します。 |WADWindowsEventLogsTable |
   | パフォーマンス カウンター |仮想マシンで使用できるパフォーマンス カウンターのデータを収集できます。 パフォーマンス カウンターは、オペレーティング システムが備えている機能であり、メモリ使用率やプロセッサ時間など多くの統計情報を保持します。 |WADPerformanceCountersTable |
   | インフラストラクチャ ログ |診断インフラストラクチャ自体から生成されるログ。 |WADDiagnosticInfrastructureLogsTable |
   | IIS ログ |Web 要求を記録するログ。 クラウド サービスが大量のトラフィックを取得する場合、これらのログは長くなる可能性があります。 このデータは、必要なときにのみ収集して格納することをお勧めします。 |失敗した要求のログは、そのデプロイ、ロール、およびインスタンスのパスにある wad-iis-failedreqlogs の BLOB コンテナーで見つけることができます。 ログ全体は wad-iis-logfiles にあります。 各ファイルのエントリは WADDirectories テーブルで生成されます。 |
   | クラッシュ ダンプ |クラウド サービス (通常はワーカー ロール) のバイナリ イメージを提供します。 |wad-crush-dumps BLOB コンテナー |
   | カスタム ログ ファイル |ユーザー定義のログ データです。 |ストレージ アカウントのカスタム ログ ファイルの場所をコードで指定できます。 たとえば、カスタム BLOB コンテナーを指定できます。 |
4. データが切り捨てられる場合は、その種類のデータのバッファーを拡張したり、仮想マシンからストレージ アカウントへのデータ転送の間隔を短くしてみてください。
5. (省略可能) ストレージ コストを削減するために、折を見てストレージ アカウントからデータを消去します。
6. フル デプロイを行うと、Azure の diagnostics.cscfg ファイル (Azure SDK 2.5 の場合は .wadcfgx) が更新され、診断構成に対する変更があれば、クラウド サービスによってピックアップされます。 既存のデプロイを更新した場合は、Azure で .cscfg ファイルは更新されません。 その場合でも、次のセクションの手順に従って診断の設定を変更することができます。 フル デプロイの実行と既存のデプロイの更新の詳細については、 [Azure アプリケーションの公開ウィザード](vs-azure-tools-publish-azure-application-wizard.md)に関するページを参照してください。

### <a name="to-view-virtual-machine-diagnostics-data"></a>仮想マシンの診断データを表示するには
1. 仮想マシンのショートカット メニューで **[診断データの表示]** を選択します。

    ![Azure 仮想マシンの診断データを表示する](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)

    **[診断の概要]** ダイアログ ボックスが表示されます。

    ![Azure virtual machine diagnostics summary](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)

    最新のデータが表示されない場合は、転送間隔が経過するまで待ちます。

    データをすぐに更新するには、**[更新]** リンクを選択します。 データを自動的に更新するには、**[自動更新]** ドロップダウン リスト ボックスで間隔を選択します。 エラー データをエクスポートするには、**[CSV にエクスポート]** ボタンをクリックして、Excel ワークシートで開くことができるコンマ区切り値ファイルを作成します。

## <a name="set-up-cloud-service-diagnostics-after-deployment"></a>クラウド サービスのデプロイ後に診断を設定する
既に実行しているクラウド サービスの問題について調べるとき、最初にロールをデプロイするときには指定しなかったデータを収集したい場合があります。 その場合は、サーバー エクスプローラーで設定を変更することで必要なデータの収集を開始できます。 診断は、ロールの単一インスタンスを対象に設定することも、すべてのインスタンスを対象に設定することもできます。どちらが対象となるかは、**[診断構成]** ダイアログ ボックスをインスタンスのショートカット メニューから開くか、ロールのショートカット メニューから開くかによって決まります。 ロール ノードを構成した場合、変更はすべてのインスタンスに適用されます。 インスタンス ノードを構成した場合、変更は対象のインスタンスにのみ適用されます。

### <a name="to-set-up-diagnostics-for-a-running-cloud-service"></a>実行中のクラウド サービスの診断を構成するには
1. サーバー エクスプローラーで、**[クラウド サービス]** ノードを展開し、ノードの一覧を展開して、調べたいロールとインスタンスのどちらかまたは両方を見つけます。

    ![診断の構成](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. インスタンス ノードまたはロール ノードのショートカット メニューで **[診断の設定の更新]** を選択し、収集する診断の設定を選択します。

    構成設定については、この記事の「**診断データのソースを構成する**」を参照してください。 診断データを表示する方法については、この記事の「**診断データの表示**」を参照してください。

    サーバー エクスプローラーでデータ収集を変更した場合、その変更は、クラウド サービスを再度フル デプロイするまで有効になります。 既定の発行設定を使用する場合、変更は上書きされません。 既定の発行設定は、再度のフル デプロイを行うためではなく、既存のデプロイを更新するためのものです。 デプロイ時に設定が消去されるようにするには、発行ウィザードの **[詳細設定]** タブに移動し、**[配置の更新]** チェック ボックスをオフにします。 このチェック ボックスをオフにした状態で再デプロイすると、ロールの **[プロパティ]** エディターで行った .wadcfgx (または .wadcfg) ファイルの設定に戻ります。 デプロイを更新した場合、Azure は前の設定を保持します。

## <a name="troubleshoot-azure-cloud-service-issues"></a>Azure クラウド サービスの問題のトラブルシューティング
クラウド サービス プロジェクトで、ロールが "ビジー" 状態のままになる、リサイクルを繰り返す、内部サーバー エラーをスローするなどの問題が発生した場合、問題を診断して修正するために使用できる各種のツールと手法があります。 一般的な問題とソリューションの具体例や、エラーを診断して修正するために使用できる概念とツールの概要については、[Azure PaaS 計算診断データ](/archive/blogs/kwill/windows-azure-paas-compute-diagnostics-data)に関するページを参照してください。

## <a name="q--a"></a>Q & A
**バッファー サイズとは何ですか。その大きさはどのくらいが適切ですか。**

ローカル ファイル システムに保存できる診断データの量は、各仮想マシン インスタンスのクォータによって制限されています。 これに加えて、利用できる診断データの種類ごとにバッファー サイズを指定できます。 このバッファー サイズは、その種類のデータに対する個別のクォータのような役割を果たします。 クォータ全体とメモリ残量は、診断データの種類用のダイアログ ボックスの下部で確認できます。 バッファーのサイズを大きくしたり、データの種類を増やすには、クォータ全体を操作します。 クォータ全体を変更するには、diagnostics.wadcfg または .wadcfgx 構成ファイルを変更します。 診断データは、アプリケーションのデータと同じファイル システムに格納されます。 アプリケーションが大量のディスク領域を使用する場合は、診断クォータ全体を増加させないでください。

**転送間隔とは何ですか。その長さはどのくらいが適切ですか。**

転送間隔は、データの取り込み間隔、つまり前回の取り込みから次の取り込みまでの経過時間です。 転送間隔として指定された時間が経過するたびに、仮想マシンのローカル ファイル システムからストレージ アカウントのテーブルにデータが移動されます。 収集されたデータの量が、転送間隔の終わりを待たずにクォータを超えた場合、古いデータから順に破棄されます。 データがバッファー サイズまたは全体のクォータを超えるためにデータが失われる場合は、転送間隔を短くしてください。

**タイム スタンプには、どのタイム ゾーンが使用されますか。**

タイム スタンプは、クラウド サービスをホストしているデータ センターのローカル タイム ゾーンです。 ログ テーブルでは次の 3 つのタイム スタンプ列が使用されます。

* **PreciseTimeStamp**: イベントの ETW タイム スタンプ。 つまり、クライアントのイベントがログに記録された時刻です。
* **TIMESTAMP**: アップロード頻度境界に切り捨てられた **PreciseTimeStamp**。 たとえば、アップロード頻度が 5 分で、イベント時刻が 00:17:12 の場合、TIMESTAMP は 00:15:00 になります。
* **Timestamp**: エンティティが Azure テーブルに作成された時刻のタイム スタンプ。

**診断情報を収集するためのコストを管理するにはどうすればよいですか。**

既定の設定 (**[ログ レベル]** は **[エラー]**、**[転送間隔]** は **[1 分]**) はコストが最小となるように設計されています。 収集する診断データを増やしたり、転送間隔を短くしたりすると、コンピューティング コストが増大します。 必要以上に多くのデータを収集しないようにし、必要がなくなったらデータ収集を無効にしてください。 この記事ですでに説明したように、データ収集は、実行時も含めていつでも有効にすることができます。

**IIS から失敗した要求のログを収集するにはどうすればよいですか。**

既定では、IIS は失敗した要求のログを収集しません。 Web ロールの web.config ファイルを編集することで、失敗した要求のログを収集するように IIS を設定できます。

**OnStart など RoleEntryPoint のメソッドからトレース情報を取得できません。何か問題があるのでしょうか。**

**RoleEntryPoint** のメソッドは、IIS ではなく WAIISHost.exe のコンテキストで呼び出されます。 通常であればトレースを有効にする web.config の構成情報は適用されません。 この問題を解決するには、Web ロール プロジェクトに .config ファイルを追加し、そのファイルに **RoleEntryPoint** コードを含む出力アセンブリと同じ名前を付けます。 既定の Web ロール プロジェクトでは、.config ファイルの名前は WAIISHost.exe.config です。このファイルに次の行を追加します。

```xml
<system.diagnostics>
  <trace>
      <listeners>
          <add name “AzureDiagnostics” type=”Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener”>
              <filter type=”” />
          </add>
      </listeners>
  </trace>
</system.diagnostics>
```

**[プロパティ]** ウィンドウで、**[出力ディレクトリにコピー]** プロパティを **[常にコピーする]** に設定します。

## <a name="next-steps"></a>次のステップ
Azure の診断ログの詳細については、[Azure Cloud Services および Virtual Machines での診断の有効化](/azure/cloud-services/cloud-services-dotnet-diagnostics)に関するページと「[Azure App Service の Web アプリの診断ログの有効化](/azure/app-service/web-sites-enable-diagnostic-log)」を参照してください。
