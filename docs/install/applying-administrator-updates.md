---
title: Microsoft Endpoint Configuration Manager を使用して Visual Studio に管理者向け更新プログラムを適用する
titleSuffix: ''
description: Visual Studio に管理者向け更新プログラムを適用する方法について説明します。
ms.date: 04/16/2021
ms.custom: ''
ms.topic: overview
ms.assetid: 9a3fdb28-db3d-4970-bc17-7417a985f0fb
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: c18c460ebcffdba93279aafec2f3d76503ab2383
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307688"
---
# <a name="applying-administrator-updates-that-use-microsoft-endpoint-configuration-manager"></a>Microsoft Endpoint Configuration Manager を使用して管理者向け更新プログラムを適用する

このドキュメントでは、Visual Studio 管理者向け更新プログラムのさまざまな種類と特性について説明します。 以下に、組織全体に配布する方法と時期、使用可能な構成オプション、およびレポートを表示してトラブルシューティングを行う方法について説明します。 管理者向け更新プログラムを使用するための前提条件の詳細については、[管理者向け更新プログラムの有効化](../install/enabling-administrator-updates.md)に関するページを参照してください。 管理者向け更新プログラムは、Visual Studio が既にコンピューターにインストールされていることを前提としています。 管理者向け更新プログラムを適用しても、まったく新しいインストールが開始されるわけではありません。

## <a name="understanding-visual-studio-administrator-updates"></a>Visual Studio 管理者向け更新プログラムについて

Microsoft カタログおよび WSUS で使用される Microsoft Update に発行される Visual Studio 管理者向け更新プログラム パッケージには、Configuration Manager で Visual Studio 更新プログラムをダウンロードしてクライアント コンピューターに配布するために必要な情報が含まれています。 IT 管理者が組織全体に配布する更新プログラムを決定するために必要な情報も含まれています。 これは、ネットワーク レイアウトのメンテナンスを容易にするためにも使用できます。 Visual Studio 管理者更新プログラム パッケージには、製品の新規インストールを実行するために十分な情報は含まれず、Content Delivery Network に発行される実際の製品バイナリも含まれません。 Visual Studio 管理者向け更新プログラムは、Visual Studio の通常の更新プログラムと同様に累積的です。 製品バージョン番号やリリース日がより新しい Visual Studio 更新プログラムはすべて、より古い下位のバージョンのスーパーセットであると見なすことができます。

Visual Studio 管理者向け更新プログラムは、サポート対象の Visual Studio サービス バージョンに適用されます。 特定の期間中に Visual Studio のどのサービス ベースラインがサポートされているかの詳細については、「[Visual Studio の製品ライフサイクルとサービス](/visualstudio/productinfo/vs-servicing-vs)」を参照してください。 Visual Studio のサポートされているサービス ベースラインはすべて安全に維持されます。  

## <a name="types-and-characteristics-of-administrator-updates"></a>管理者向け更新プログラムの種類と特性

Visual Studio には、次の 3 種類の管理者向け更新プログラムがあります。

* **セキュリティ更新プログラム** は、すべての Visual Studio エディション (Enterprise、Professional、Community など) に適用され、限定的で対象を絞った互換性のあるサービス レベルの変更が含まれます。 セキュリティ更新プログラムは、クライアントをそれ以降のマイナー バージョンに上げるものではなく、既に特定のマイナー バージョン レベルにあるクライアントに対して、セキュリティの脆弱性に対する修正を提供するように設計されます。 セキュリティ更新プログラムには、少なくとも 1 つのセキュリティ修正プログラムが含まれますが、セキュリティ修正プログラムは、クライアント コンピューターにインストールされているコンポーネントまたはワークロードに適用される場合もあれば、されない場合もあります。 たとえば、.NET コンポーネント内のセキュリティの脆弱性を修正でき、その更新プログラムにセキュリティ更新プログラムのラベルを付けることはできますが、これは、C++ コンポーネントのみがインストールされているクライアント コンピューターには実際には意味のある影響はありません。 セキュリティ更新プログラムには、その他の信頼性の修正や、その他の必要なコンポーネントの更新が含まれる場合もあります。 セキュリティ更新プログラムは、[Microsoft Update カタログ](https://www.catalog.update.microsoft.com/Home.aspx) (MUC) と [Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus) の両方に発行され、"セキュリティ更新プログラム" として分類されます。
* **機能更新プログラム** を使用して、IT 管理者は、組織内のコンピューターを Visual Studio のより新しいマイナー バージョンに上げることができます。 機能更新プログラムが適用されるのは、Enterprise、Professional、Build Tools SKU など、企業でよく見られる Visual Studio のエディションのみです。 すべての機能更新プログラムは、"機能パック" として Microsoft Update カタログに発行され、必要に応じて手動で [Microsoft Update カタログから Configuration Manager にインポート](/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)できます。 機能更新プログラムは累積的であり、追加の品質および以前のセキュリティ修正プログラムが含まれます。 サービス ベースラインを維持し、機能更新プログラムが特定のクライアントに配信されないようにクライアント コンピューターを構成する方法については、後述の[構成オプション](#understanding-configuration-options)に関するセクションを参照してください。
* **品質更新プログラム** は、企業内でよく見られる Visual Studio のエディションにのみ適用され、限定的で対象を絞った互換性のあるサービス レベル変更が含まれます。 品質更新プログラムは、クライアントをそれ以降のマイナー バージョンに上げるものではなく、特定のマイナー バージョン レベルに既にあるクライアントに対して、パフォーマンスと信頼性の修正や、その他の必要なコンポーネントの更新プログラムを提供するように設計されます。 品質更新プログラムはセキュリティ更新プログラムと共に蓄積されます。したがってセキュリティ修正プログラムが単独で既にリリースされている場合にのみ、そのセキュリティ修正が含まれます。 品質更新プログラムは、"更新プログラム" として Microsoft Update カタログに発行され、必要に応じて手動で [Configuration Manager にインポート](/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)することもできます。

### <a name="decoding-the-titles-of-administrator-updates"></a>管理者向け更新プログラムのタイトルをデコードする

各管理者更新プログラムのタイトルは、適用可能なバージョン範囲と、更新プログラムの結果のバージョンの両方を表します。たとえば、次のように入力します。

::: moniker range="vs-2017"

* "セキュリティ更新プログラム" として分類されている **Visual Studio 2017 バージョン 15.9.0 から 15.9.35 の更新プログラム** は、クライアント上のバージョン 15.9.0 から 15.9.35 までのすべての Visual Studio 2017 エディションに適用され、これらのクライアント エディションが 15.9.35 に更新されます。
* "機能パック" として分類されている **Visual Studio 2017 バージョン 15.0.0 から 15.9.0 の更新プログラム** は、クライアント上の 15.0.0 から 15.9.0 までの製品バージョン範囲全体を企業が使用するためにライセンス供与される Visual Studio 2017 エディションに適用され、これらのクライアント エディションが 15.9.0 に更新されます。 この機能パックを適用すると、基本的にはクライアントがセキュリティ更新プログラムを受信できるようになります。 
* 単に "更新プログラム" として分類されている **Visual Studio 2017 バージョン 15.9.0 から 15.9.37 の更新プログラム** は、クライアント上のバージョン 15.9.0 から 15.9.37 までを企業が使用するためにライセンス供与される Visual Studio 2017 に適用され、これらのクライアント エディションが 15.9.37 に更新されます。

::: moniker-end

::: moniker range="vs-2019"

* "セキュリティ更新プログラム" として分類されている **Visual Studio 2019 バージョン 16.7.0 から 16.7.12 の更新プログラム** は、クライアント上のバージョン 16.7.0 から 16.7.12 までのすべての Visual Studio 2019 エディションに適用され、これらのクライアント エディションが 16.7.12 に更新されます。  
* "機能パック" として分類されている **Visual Studio 2019 バージョン 16.0.0 から 16.9.0 の更新プログラム** はクライアント上の 16.0.0 から 16.9.0 までの製品バージョン範囲全体を企業が使用するためにライセンス供与される Visual Studio 2019 エディションに適用され、これらのクライアント エディション (それより前のサービス ベースラインで維持するように構成されていない) が 16.9.0 に更新されます。 
* 単に "更新プログラム" として分類されている **Visual Studio 2019 バージョン 16.8.0 から 16.8.7 の更新プログラム** は、クライアント上のバージョン 16.8.0 から 16.8.7 までを企業が使用するためにライセンス供与された Visual Studio 2019 に適用され、これらのクライアント エディションが 16.8.7 に更新されます。

::: moniker-end

::: moniker range=">=vs-2022"

::: moniker-end

## <a name="using-configuration-manager-to-deploy-visual-studio-updates"></a>Configuration Manager を使用して Visual Studio 更新プログラムを展開する

### <a name="understanding-configuration-options"></a>構成オプションについて

互換性を持たせ、組織の展開の設定と要件に合わせられるように Visual Studio 管理者向け更新プログラムの調整に使用できる構成オプションがいくつかあります。 最も一般的な構成オプションを以下に示します。 サポートされているすべての管理者向け更新プログラムの動作の完全な一覧については、「[コマンドライン パラメーターを使用して Visual Studio をインストールする](../install/use-command-line-parameters-to-install-visual-studio.md)」を参照し、"更新プログラム" アクションに対応しているものについてのみ目を通してください。

* **[管理者向け更新プログラムのオプトイン](../install/enabling-administrator-updates.md#encoding-administrator-intent-on-the-client-machines)** : クライアント コンピューターが管理者向け更新プログラムを受け取るには、このレジストリ キーが必要です。 これはコンピューター全体に適用される 1 つのキーで、ボックスにインストールされている Visual Studio のすべてのインスタンスに適用されます。
* **Visual Studio ユーザーによるオプトアウト**: Visual Studio ユーザーはコンピューター全体の **AdministratorUpdatesOptOut** レジストリ キーを別に使用して、Visual Studio の管理者向け更新プログラムの受信を "*オプトアウト*" できます。 このキーの目的は、コンピューターへの自動的な更新プログラムの適用を超えた制御を Visual Studio ユーザーに可能にすることです。 管理者向け更新プログラムをブロックするようにクライアント コンピューターを構成するには、 **AdministratorUpdatesOptOut** REG_DWORD キーを  **1** に設定します。 このキーがない、または値  **0** が設定されている場合は、Visual Studio ユーザーが Visual Studio の管理者向け更新プログラムの受け取りを希望していることを意味します。
    ユーザーの設定をエンコードするための  **AdministratorUpdatesOptOut**  キーの方が、IT 管理者の意図をエンコードする  **AdministratorUpdatesEnabled**  キーよりも優先されることに注意してください。  **AdministratorUpdatesOptOut**  が  **1** に設定されている場合は、 **AdministratorUpdatesEnabled** キーが  **1** に設定されていても、更新プログラムはクライアントでブロックされます。このアクションは、IT 管理者が、どの開発者がオプトアウトを選択したかにアクセスして監視でき、だれのニーズがより重要かを双方で検討できることを前提としています。IT 管理者は、どちらのキーも必要に応じていつでも変更できます。
* **更新済みの製品ビットの場所**: ほとんどの場合、クライアント コンピューターにより、Microsoft CDN を使用して、更新された製品ビットがインターネットからダウンロードされます。 このシナリオでは、クライアント コンピューターがインターネットにアクセスできる必要があります。 ただし、一部の企業は、クライアント コンピューターに対して、ビットのインストールと更新を内部ネットワーク レイアウトの場所からのみに制限しています。 内部ネットワークの場所にある更新済みのビットを使用して管理者向け更新プログラムを適用できるようにするには、管理者向け更新プログラムが正常に展開される前に、次の条件を満たす必要があります。 
  * クライアント コンピューターが、どこかの時点で、そのネットワーク レイアウトの場所からブートストラップを事前に実行しておく必要があります。 元のクライアントのインストールがネットワーク レイアウトのブートストラップを使用して行われるのが理想的ですが、同じネットワークの場所で更新されたブートストラップを使用して更新プログラムをインストールすることもできます。 どちらの操作でも、クライアント コンピューター上に特定のレイアウトの場所との接続が埋め込まれます。
  * ネットワーク レイアウトの場所 (クライアントの接続先) を、管理者向け更新プログラムを展開する[更新済みの製品ビットを含むように更新する](../install/update-a-network-installation-of-visual-studio.md)必要があります。

::: moniker range=">=vs-2019"

* **サービス ベースラインの持続性**: 前述したように、管理者向け機能更新プログラムによって、Visual Studio のインストールが製品のより新しいマイナー バージョンに上げられます。 ただし、Visual Studio ユーザーが特定の安定したセキュリティで保護されたサービス ベースライン レベルを維持する必要があり、そのコンピューターをより新しいマイナー バージョンに上げるタイミングを制御したい場合があります。 クライアント コンピューターをサービス ベースラインで維持し、それに送信される望ましくない管理者向け機能更新プログラムを無視するように構成するには、**BaselineStickinessVersions2019** Reg_SZ データ値を作成し、クライアント コンピューターがスナップして維持できる希望のベースラインを表す文字列に設定する必要があります。 文字列には、**16.7.0** などの使用可能なサービス ベースライン バージョンを含めることができます。  
     `BaselineStickinessVersions2019` レジストリ値の形式が正しくない場合は、そのコンピューターへのすべての管理者向け機能更新プログラムのインストールがブロックされます。 また、[Visual Studio 機能更新プログラムのサポート期間](/visualstudio/productinfo/vs-servicing-vs)にも注意してください。 さらに、`BaselineStickinessVersions2019` キーの有無、または値にかかわらず、有効期間が終了している管理者向け機能更新プログラムを適用することは技術的に可能ですが、それらはサポート外で、安全でない可能性があるため、お勧めしません。

::: moniker-end

* **Visual studio が使用されている場合でも更新プログラムを強制的に実行する**: 更新プログラムをインストールする前に、Visual Studio が閉じられている必要があります。 Visual Studio が開いているか、使用されている場合、更新プログラムのインストールは中止されます。 Visual Studio が閉じていることを保証する簡単な方法は、コンピューターの再起動直後に更新プログラムを適用するように Confirmation Manager を構成することです。 `--force` パラメーターを使用して、Visual Studio を強制的にシャットダウンすることもできます。 Visual Studio を強制的に閉じると作業内容が失われる可能性があるため、注意して使用してください。 既定のシステム コンテキストで管理者向け更新プログラムを実行すると、`–-force` フラグは無視されるため、ユーザー コンテキストで実行されるように管理者向け更新プログラムを構成する必要があります。

### <a name="methods-for-configuring-an-administrator-update"></a>管理者更新プログラムを構成する方法

管理者向け更新プログラムを構成するには、レジストリ キー、クライアント コンピューター上の構成ファイル、Configuration Manager 展開パッケージ自体の変更という 3 つの主要な方法があります。   

* **レジストリ キー**: [エンタープライズ展開への既定値の設定](../install/set-defaults-for-enterprise-deployments.md)に関する記事で説明されているように、管理者向け更新プログラムにより、Visual Studio の標準の場所のいずれかで特定のレジストリ キーが検索されます。 レジストリ キーによって制御されるオプションは、**AdministratorUpdatesOptOut** Reg_DWORD、**AdministratorUpdatesOptOut** Reg_DWORD、**BaselineStickinessVersions2019** Reg_SZ などの項目です。 レジストリ キーの値を作成および設定するには、クライアント コンピューターでの管理者アクセスが必要です。

* **構成ファイル**: いくつかの設定は、オプションの構成ファイルでクライアント コンピューターに保存できます。これにより、1 回設定するだけで、今後のすべての管理者向け更新プログラムに適用されるという利点があります。 構成ファイルのアプローチは、レジストリ キーのように動作し、コンピューター全体に適用されます。これは、クライアント コンピューターにインストールされている Visual Studio のすべてのインストールに適用されることを意味します。 構成ファイルの標準の場所は、`C:\ProgramData\Microsoft\VisualStudio\updates.config` です。 ただし、別の場所を使用してファイルを保存する場合は、**UpdateConfigurationFile** という名前の Reg_SZ レジストリ キーを作成し、このキーの値を構成ファイルのパスに設定します。 このレジストリ キーは、[エンタープライズ展開への既定値の設定](../install/set-defaults-for-enterprise-deployments.md)に関する記事で説明されているように、Visual Studio のレジストリの任意の場所に配置できます。 カスタム構成ファイルの場所にレジストリ値を追加することを選択した場合は、そのファイルが検索されます。ファイルが存在しない場合は、例外がスローされ、更新は失敗します。

     JSON 形式の構成ファイルは、オプション `installerUpdateArgs` をサポートしています。これは、Visual Studio インストーラーに渡すことができるその他のスイッチをコンマで区切った文字列の配列です。 ファイルの内容に無効なフィールドまたはサポートされていないオプションが含まれている場合、更新は失敗します。 詳細については、「[コマンド ライン パラメーターを使用して Visual Studio をインストールする](../install/use-command-line-parameters-to-install-visual-studio.md)」を参照してください。

   構成ファイルの例を次に示します。

  ```json
  "installerUpdateArgs" : ["--quiet", "--noWeb"], 
  "checkPendingReboot" :  "true" 
  ```

* **SCCM で管理者向け更新プログラム パッケージを手動で更新する**: SCCM で個々の管理者向け更新プログラム パッケージのコマンドライン パラメーターを手動で変更することもできます。

## <a name="verification-reports-and-troubleshooting-error-codes"></a>検証、レポート、およびトラブルシューティングのエラー コード

### <a name="determining-that-visual-studio-was-updated"></a>Visual Studio が更新されたことを確認する

次のいずれかの方法を使用して、管理者更新プログラムが正しくインストールされたことを確認できます。

* クライアント コンピューターで、Visual Studio を起動して、 **[ヘルプ]**  > **[バージョン情報]** を選択し、バージョン番号が目的の更新プログラムのタイトルに含まれる最後の番号と一致していることを確認します。
* コンピューター上のさまざまなバージョンの Visual Studio を識別するには、クライアント コンピューターで **vswhere** ツールを使用します。 詳細については、「 [Visual Studio インスタンスの検出および管理用のツール](../install/tools-for-managing-visual-studio-instances.md)」を参照してください。
* 管理更新プログラムが試行されるたびに、更新操作の進行状況をキャプチャする複数のログ ファイルがクライアント コンピューターの `%temp%` ディレクトリに生成されます。フォルダーを日付で並べ替えて、管理更新プログラム、ブートストラッパー、Visual Studio インストーラー、およびセットアップ エンジンについて、それぞれ  `dd_updatedriver`、 `dd_bootstrapper`、 `dd_client`、 `dd_setup`  で始まるファイルを検索します。これらのログ ファイルに、更新プログラムが正常に適用されたことを示す 0 が含まれていることを確認します。 これらのログ ファイルは、構成ファイルが使用されていることを確認するためにも使用できます。 詳細については、[Visual Studio ログ収集ツール](https://www.microsoft.com/download/details.aspx?id=12493)に関するページをご覧ください。

### <a name="error-codes-and-conditions"></a>エラー コードと条件

>[!IMPORTANT]
> 更新プログラムをインストールする前に、Visual Studio が閉じられている必要があることに注意してください。 Visual Studio が開いているか、使用されている場合、更新プログラムのインストールはキャンセルされます。

管理更新プログラムにより、次のリターン コードが返される場合があります。  

| エラー コード | 定義                                                                                                                                                                                                  |
|------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0          | 管理更新プログラムが正常にインストールされました。                                                                                                                                                       |
| 1001       | Visual Studio インストーラーまたは関連するセットアップ プロセスが実行されています。 更新プログラムは適用されていません。                                                                                                                   |
| 1002       | Visual Studio インストーラーが一時停止しました。 更新プログラムは適用されていません。                                                                                                                                               |
| 1003       | Visual Studio が実行されています。 更新プログラムは適用されていません。 この状態は、`--force` フラグを使用して却下できます。                                                                                              |
| 1004       | インターネットが検出されませんでした。更新プログラムから、更新されたファイルを保持しているインターネット上の場所にアクセスできませんでした。 更新プログラムは適用されていません。                                                                          |
| 1005       |  **AdministratorUpdatesEnabled**  レジストリ値が **0** に設定されているか、まったく設定されていません。 更新プログラムは適用されていません。                                                                                            |
| 1006       |  **AdministratorUpdatesOptOut**  レジストリ値が **1** に設定されています。 更新プログラムは適用されていません。 このキーは、管理者が更新してはいけないクライアント コンピューターを対象としています。                     |
| 1007       | Visual Studio インストーラーがインストールされていません。                                                                                                                                                               |
| 1008       | **BaselineStickinessVersions2019** レジストリ値が読み取り可能な形式ではありません。 このレジストリ値には、ビルド番号が明示的に 0 に設定された **すべて** または有効なバージョン (例: X.Y.0) が含まれている必要があります。 |
| 3010       | システムの再起動が必要です。更新プログラムが適用されていない可能性があります。 コンピューターを再起動し、更新プログラムを再試行してください。                                                                                |
| その他      | 更新プログラムの適用中にエラーが発生しました。更新プログラムは適用されていません。                                                                                                                                   |

クライアント エラー コードの完全な一覧については、「 [コマンド ライン パラメーターを使用して Visual Studio をインストールする](use-command-line-parameters-to-install-visual-studio.md)」を参照してください。

## <a name="feedback-and-support"></a>フィードバックとサポート

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

次の方法を使用して、Visual Studio の管理者向け更新プログラムに関するフィードバックを提供したり、更新プログラムに影響する問題を報告したりできます。

* 「[Visual Studio のインストールとアップグレードの問題のトラブルシューティング](../install/troubleshooting-installation-issues.md)」ガイダンスをご覧ください。
* [Visual Studio セットアップ Q&A フォーラム](/answers/topics/vs-setup.html)でコミュニティに質問してください。
* [Visual Studio のサポート ページ](https://visualstudio.microsoft.com/vs/support/)にアクセスし、ご自分の問題がよくあるご質問に記載されているかどうかを確認します。  チャット ヘルプの [[サポート リンク]](https://visualstudio.microsoft.com/vs/support/#talktous) ボタンを選択することもできます。
* 管理者向け更新プログラムの適用エクスペリエンスに関して、Visual Studio チームに[機能に関するフィードバックを提供するか、問題を報告](https://aka.ms/vs/wsus/feedback)してください。
* 組織の Microsoft のテクニカル アカウント マネージャーにお問い合わせください。

## <a name="see-also"></a>関連項目

* [管理者の更新を有効にする](../install/enabling-administrator-updates.md)
* [Visual Studio 管理者ガイド](../install/visual-studio-administrator-guide.md)
* [Visual Studio の製品ライフサイクルとサービス](/visualstudio/productinfo/vs-servicing-vs)
* [Visual Studio 2019 リリース ノート](/visualstudio/releases/2019/release-notes)
* [Visual Studio 2017 リリース ノート](/visualstudio/releasenotes/vs2017-relnotes)
* [Visual Studio のインストール](../install/install-visual-studio.md)
* [コマンド ライン パラメーターを使用して Visual Studio をインストールする](../install/use-command-line-parameters-to-install-visual-studio.md)
* [Visual Studio インスタンスの検出および管理用のツール](../install/tools-for-managing-visual-studio-instances.md)
* [Visual Studio のネットワーク インストールを作成する](../install/create-a-network-installation-of-visual-studio.md)
* [応答ファイルの設定を定義する方法](../install/automated-installation-with-response-file.md)
* [ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](../install/controlling-updates-to-visual-studio-deployments.md)
* [Microsoft Update カタログのよく寄せられる質問](https://www.catalog.update.microsoft.com/faq.aspx)
* [Microsoft Endpoint Configuration Manager (SCCM) のドキュメント](/mem/configmgr)
* [Microsoft カタログから Configuration Manager に更新プログラムをインポートする](/mem/configmgr/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog)
* [Windows Server Update Services (WSUS) のドキュメント](/windows-server/administration/windows-server-update-services/get-started-windows-server-update-services-wsus)
