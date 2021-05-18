---
title: ASP.NET アプリのデバッグを有効にする | Microsoft Docs
description: Visual Studio で ASP.NET および ASP.NET Core アプリのデバッグを有効にする方法について説明します。 IIS Express サーバーまたはローカル IIS サーバーでこのプロセスを実行できます。
ms.custom: SEO-VS-2020
ms.date: 10/29/2020
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging ASP.NET Web applications
- Web.config configuration file, debug mode
- debugging [Visual Studio], ASP.NET
ms.assetid: 3beed819-cece-4864-8184-bd410000973a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- aspnet
ms.openlocfilehash: 1fd620a0c7f4860421b6f8b1a15c0b708c1ba860
ms.sourcegitcommit: a0f5e7188838c5989c9cc78d99fb29bb2813501e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/11/2021
ms.locfileid: "109729261"
---
# <a name="debug-aspnet-or-aspnet-core-apps-in-visual-studio"></a>Visual Studio で ASP.NET または ASP.NET Core アプリをデバッグする

Visual Studio では、ASP.NET アプリと ASP.NET Core アプリをデバッグできます。 このプロセスは、ASP.NET と ASP.NET Core で異なります。また、IIS Express とローカル IIS サーバーのどちらで実行するかによって異なります。

>[!NOTE]
>次の手順と設定は、ローカル サーバー上のアプリのデバッグにのみ適用されます。 リモート IIS サーバー上のアプリのデバッグには **[プロセスにアタッチ]** を使用し、これらの設定を無視します。 IIS 上の ASP.NET アプリのリモート デバッグの詳細と手順については、[IIS コンピューター上の ASP.NET のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)または[リモートの IIS コンピューター上の ASP.NET Core のリモート デバッグ](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)に関するページを参照してください。

組み込みの IIS Express サーバーは Visual Studio に含まれています。 IIS Express は、ASP.NET および ASP.NET Core プロジェクトの既定のデバッグ サーバーであり、事前に構成されています。 これは最も簡単なデバッグ方法であり、最初のデバッグとテストに最適です。

アプリを実行するように構成されているローカル IIS サーバー (バージョン 8.0 以降) 上で ASP.NET または ASP.NET Core アプリをデバッグすることもできます。 ローカル IIS 上でデバッグするには、次の要件を満たす必要があります。

<a name="iis"></a>
- **ASP.NET と Web 開発ワークロード** がインストールされていない場合はインストールします (Visual Studio インストーラーを再実行し、 **[変更]** を選択して、このワークロードを追加します)。

   ::: moniker range="vs-2017"
   Visual Studio 2017 で、 **[開発時 IIS サポート]** コンポーネントを探します。 ワークロードを追加するときに、それが選択されていることを確認します。
   ::: moniker-end
- Visual Studio を管理者として実行します。
- IIS をインストールし、適切なバージョンの ASP.NET または ASP.NET Core、またはその両方を使用して正しく構成します。 IIS と ASP.NET Core の使用の詳細については、「[IIS を使用した Windows での ASP.NET Core のホスト](/aspnet/core/host-and-deploy/iis/index)」を参照してください。 ASP.NET については、[IIS と ASP.NET モジュールのインストール](/iis/application-frameworks/scenario-build-an-aspnet-website-on-iis/configuring-step-1-install-iis-and-asp-net-modules)に関する記事を参照してください。
- IIS 上でアプリがエラーなしで動作することを確認します。

## <a name="debug-aspnet-apps"></a>ASP.NET アプリをデバッグする

IIS Express が既定値であり、事前に構成されています。 ローカル IIS 上でデバッグする場合は、[ローカル IIS デバッグの要件](#iis)を満たしていることを確認します。

1. Visual Studio の **ソリューション エクスプローラー** で ASP.NET プロジェクトを選択し、 **[プロパティ]** アイコンをクリックするか、**Alt**+**Enter** キーを押すか、右クリックして **[プロパティ]** を選択します。

1. **[Web]** タブを選択します。

1. **[プロパティ]** ペインの **[サーバー]** で次のようにします。
   - IIS Express の場合は、ドロップダウンから **[IIS Express]** を選択します。
   - ローカル IIS の場合は、次のようにします。
     1. ドロップダウンから **[ローカル IIS]** を選択します。
     1. IIS でアプリをまだ設定していない場合は、 **[プロジェクトの URL]** フィールドの横にある **[仮想ディレクトリの作成]** を選択します。

1. **[デバッガー]** で **[ASP.NET]** を選択します。

   ![ASP.NET のデバッガー設定](media/dbg-aspnet-enable-debugging2.png "ASP.NET のデバッガー設定")

1. **[ファイル]**  >  **[選択されたファイルを上書き保存]** を選択して (または、**Ctrl**+**S** キーを押して) 変更を保存します。

1. アプリをデバッグするには、プロジェクトで、一部のコードにブレークポイントを設定します。 Visual Studio ツールバーで、構成が **[デバッグ]** に設定されていること、目的のブラウザーがエミュレーター フィールドの **[IIS Express (\<Browser name>)]** または **[ローカル IIS (\<Browser name>)]** に表示されていることを確認します。

1. デバッグを開始するには、ツール バーで **[IIS Express (\<Browser name>)]** または **[ローカル IIS (\<Browser name>)]** を選択し、 **[デバッグ]** メニューから **[デバッグの開始]** を選択するか、**F5** キーを押します。 デバッガーはブレークポイントで一時停止します。 デバッガーがブレークポイントにヒットしない場合は、「[デバッグのトラブルシューティング](#troubleshoot-debugging)」を参照してください。

## <a name="debug-aspnet-core-apps"></a>ASP.NET Core アプリをデバッグする

IIS Express が既定値であり、事前に構成されています。 ローカル IIS 上でデバッグする場合は、[ローカル IIS デバッグの要件](#iis)を満たしていることを確認します。

1. Visual Studio の **ソリューション エクスプローラー** で ASP.NET Core プロジェクトを選択し、 **[プロパティ]** アイコンをクリックするか、**Alt**+**Enter** キーを押すか、右クリックして **[プロパティ]** を選択します。

1. **[デバッグ]** タブを選択します。

1. **[プロパティ]** ペインの **[プロファイル]** の横で次のようにします。
   - IIS Express の場合は、ドロップダウンから **[IIS Express]** を選択します。
   - ローカル IIS の場合は、ドロップダウンからアプリ名を選択するか、 **[新規]** を選択して新しいプロファイル名を作成し、 **[OK]** を選択します。

1. **[起動]** の横にあるドロップダウンから **[IIS Express]** または **[IIS]** を選択します。

1. **[ブラウザーの起動]** が選択されていることを確認します。

1. **[環境変数]** の下に、 **[開発]** の値の **ASPNETCORE_ENVIRONMENT** が存在することを確認します。 そうでない場合は、 **[追加]** を選択して追加します。

   ![ASP.NET Core のデバッガー設定](../debugger/media/dbg-aspnet-enable-debugging3.png "ASP.NET Core のデバッガー設定")

1. **[ファイル]**  >  **[選択されたファイルを上書き保存]** を使用するか、**Ctrl**+**S** キーを押して変更を保存します。

1. アプリをデバッグするには、プロジェクトで、一部のコードにブレークポイントを設定します。 Visual Studio のツールバーで、構成が **[デバッグ]** に設定され、エミュレーター フィールドに **IIS Express** または新しい IIS プロファイル名が表示されることを確認します。

1. デバッグを開始するには、ツールバーで **[IIS Express]** または **\<IIS profile name>** を選択し、 **[デバッグ]** メニューから **[デバッグの開始]** を選択するか、**F5** キーを押します。 デバッガーはブレークポイントで一時停止します。 デバッガーがブレークポイントにヒットしない場合は、「[デバッグのトラブルシューティング](#troubleshoot-debugging)」を参照してください。

## <a name="troubleshoot-debugging"></a>デバッグのトラブルシューティング

ローカル IIS のデバッグがブレークポイントまで進まない場合は、以下の手順に従ってトラブルシューティングしてください。

1. IIS から Web アプリを起動し、正常に動作することを確認します。 Web アプリを実行したままにします。

2. Visual Studio から **[デバッグ] > [プロセスにアタッチ]** を選択するか **Ctrl**+**Alt**+**P** キーを押して、ASP.NET または ASP.NET Core プロセス (通常は **w3wp.exe** または **dotnet.exe**) に接続します。 詳細については、[プロセスへのアタッチ](attach-to-running-processes-with-the-visual-studio-debugger.md)と [ASP.NET プロセス名を確認する方法](how-to-find-the-name-of-the-aspnet-process.md)に関するページを参照してください。

**[プロセスにアタッチ]** を使用すると接続してブレークポイントにヒットできても、 **[デバッグ]**  >  **[デバッグの開始]** または **F5** キーを使用すると失敗する場合は、プロジェクトのプロパティの設定が誤っている可能性があります。 HOSTS ファイルを使用する場合は、それも正しく構成されていることを確認します。

## <a name="configure-debugging-in-the-webconfig-file"></a>web.config ファイルでデバッグを構成する

ASP.NET プロジェクトには、既定で *web.config* ファイルがあり、デバッグ設定など、アプリ構成と起動情報の両方が含まれています。 *web.config* ファイルをデバッグ用に正しく構成する必要があります。 前のセクションの **[プロパティ]** 設定によって *web.config* ファイルは更新されますが、手動で構成することもできます。

> [!NOTE]
> ASP.NET Core プロジェクトには、最初は *web.config* ファイルが含まれていませんが、アプリの構成と起動情報には *appsettings.json* と *launchSettings.json* ファイルが使用されます。 アプリを配置すると、プロジェクトに 1 つまたは複数の *web.config* ファイルが作成されますが、通常、デバッグ情報は含まれていません。

> [!TIP]
> 配置プロセスによって *web.config* 設定が更新される場合があるため、デバッグを試みる前に、*web.config* がデバッグ用に構成されていることを確認します。

***web.config* ファイルをデバッグ用に手動で構成するには:**

1. Visual Studio で、ASP.NET プロジェクトの *web.config* ファイルを開きます。

2. *web.config* は XML ファイルなので、タグでマークされた入れ子のセクションが含まれます。 `configuration/system.web/compilation` セクションを見つけます。 (`compilation` 要素が存在しない場合は作成します)。

3. `compilation` 要素の `debug` 属性が `true` に設定されていることを確認します (`compilation` 要素に `debug` 属性が含まれていない場合は、それを追加して `true` に設定します)。

   既定の IIS Express サーバーではなくローカル IIS を使用している場合は、`compilation` 要素の `targetFramework` 属性値が IIS サーバー上のフレームワークと一致していることを確認します。

   *web.config* ファイルの `compilation` 要素は、次の例のようになります。

   > [!NOTE]
   > この例は部分的な *web.config* ファイルです。 通常、`configuration` 要素と `system.web` 要素にはその他の XML セクションがあります。また、`compilation` 要素には他の属性と要素が含まれる場合もあります。

   ```xml
   <configuration>
      ...
      <system.web>
          <compilation  debug="true"  targetFramework="4.6.1" ... >
             ...
          </compilation>
      </system.web>
   </configuration>
   ```

*web.config* ファイルに変更が加えられると、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] によってその変更が自動的に検出され、新しい構成設定が適用されます。 変更を有効にするためにコンピューターまたは IIS サーバーを再起動する必要はありません。

Web サイトには、複数の仮想ディレクトリとサブディレクトリを含めて、それぞれに *web.config* ファイルを格納することができます。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] アプリには、URL パスの上位レベルにある *web.config* ファイルから構成設定が継承されます。 階層的な *web.config* ファイル設定は、階層内でそれらの下位にあるすべての [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] アプリに適用されます。 階層の下位にある *web.config* ファイルに別の構成を設定すると、上位のファイルの設定は上書きされます。

たとえば、<em>www.microsoft.com/aaa/web.config</em> で `debug="true"` を指定した場合、*aaa* フォルダーまたは *aaa* のサブフォルダーにあるすべてのアプリには、その設定が継承されます。ただし、それらのアプリのいずれかによって独自の *web.config* ファイルで設定が上書きされる場合を除きます。

## <a name="publish-in-debug-mode-using-the-file-system"></a>ファイル システムを使用してデバッグ モードで発行する

IIS にアプリを発行するには、さまざまな方法があります。 これらの手順は、ファイル システムを使用してデバッグの発行プロファイルを作成して配置する方法を示しています。 これを行うには、Visual Studio を管理者として実行している必要があります。

> [!IMPORTANT]
> コードを変更するかリビルドする場合は、これらの手順を繰り返して再発行する必要があります。

1. Visual Studio で、プロジェクトを右クリックし、 **[発行]** を選択します。

3. **[IIS、FTP、その他]** を選択し、 **[発行]** をクリックします。

    ![Visual Studio の [発行先を選択] ダイアログのスクリーンショット。 IIS、FTP、Web 配置が選択され、[発行] ボタンが強調表示されています。](media/dbg-aspnet-local-iis.png)

4. **[CustomProfile]** ダイアログの **[発行方法]** で、 **[ファイル システム]** を選択します。

5. **[ターゲットの場所]** では **[参照]** ( **...** ) を選択します。

   - ASP.NET の場合は **[ローカル IIS]** を選択し、アプリ用に作成した Web サイトを選択して、 **[開く]** を選択します。

     ![ASP.NET を IIS に発行する](media/dbg-aspnet-local-iis1.png "ASP.NET を IIS に発行する")

   - ASP.NET Core の場合は、 **[ファイル システム]** を選択し、アプリ用に設定したフォルダーを選択してから、 **[開く]** を選択します。

1. **[次へ]** を選択します。

1. **[構成]** で、ドロップ ダウンから **[デバッグ]** を選択します。

1. **[保存]** を選択します。

1. **[発行]** ダイアログで、**CustomProfile** (または作成したプロファイルの名前) が表示され、**LastUsedBuildConfiguration** が **[デバッグ]** に設定されていることを確認します。

1. **[発行]** を選びます。

    ![[発行] ダイアログのスクリーンショット。CustomProfile アプリが選択され、[発行] ボタンが強調表示され、LastBuildConfiguration に [デバッグ] が設定されています。](media/dbg-aspnet-local-iis-select-site.png)

> [!IMPORTANT]
> デバッグ モードにすると、アプリのパフォーマンスは大幅に低下します。 最高のパフォーマンスを得るには、*web.config* で `debug="false"` を設定し、運用アプリを配置するとき、またはパフォーマンス測定を行うときに [リリース ビルド] を指定します。

## <a name="see-also"></a>関連項目
- [ASP.NET のデバッグ : システム要件](aspnet-debugging-system-requirements.md)
- [方法: ユーザー アカウントでワーカー プロセスを実行する](how-to-run-the-worker-process-under-a-user-account.md)
- [方法: ASP.NET プロセスの名前を見つける](how-to-find-the-name-of-the-aspnet-process.md)
- [配置した Web アプリケーションのデバッグ](debugging-deployed-web-applications.md)
- [チュートリアル: Web フォームのデバッグ](walkthrough-debugging-a-web-form.md)
- [方法: ASP.NET の例外をデバッグする](how-to-debug-aspnet-exceptions.md)
- [Web アプリケーションをデバッグする: エラーとトラブルシューティング](debugging-web-applications-errors-and-troubleshooting.md)
