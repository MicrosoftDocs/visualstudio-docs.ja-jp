---
title: ClickOnce アプリケーションを手動で配置する
description: コマンドライン バージョンまたはグラフィカル バージョンのマニフェスト生成および編集ツールを使用して ClickOnce 配置を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Mage.exe, manual ClickOnce deployments
- MageUI.exe, manual ClickOnce deployments
- deploying applications [ClickOnce], manual ClickOnce deployments
- ClickOnce deployment, manually
- ClickOnce deployment, SDK tools
- manual ClickOnce deployments
- manifests [ClickOnce]
ms.assetid: ccee6551-a1b9-4ca2-8845-9c1cf4ac2560
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d1555a7ef1f942e4be0b7cf929e0e1730f99d1d7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99917279"
---
# <a name="walkthrough-manually-deploy-a-clickonce-application"></a>チュートリアル: ClickOnce アプリケーションを手動で配置する
Visual Studio を使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを配置できない場合、または信頼されたアプリケーションの配置などの高度な配置機能を使用する必要がある場合は、*Mage.exe* コマンドライン ツールを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェストを作成する必要があります。 このチュートリアルでは、コマンドライン バージョン (*Mage.exe*) またはグラフィカル バージョン (*MageUI.exe*) のマニフェスト生成および編集ツールを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置を作成する方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルでは、配置を構築する前に選択する必要があるいくつかの前提条件とオプションについて説明します。

- *Mage.exe* と *MageUI.exe* をインストールします。

   *Mage.exe* と *MageUI.exe* は [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] の一部です。 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] がインストールされているか、Visual Studio に付属のバージョンの [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] が必要です。 詳細については、MSDN の [Windows SDK](https://www.microsoft.com/download/details.aspx?id=8279) に関するページを参照してください。

- 配置するアプリケーションを用意します。

   このチュートリアルでは、配置する準備ができている Windows アプリケーションがあることを前提としています。 このアプリケーションを AppToDeploy と呼びます。

- 配置の配布方法を決定します。

   配布オプションには、Web、ファイル共有、CD があります。 詳細については、「 [ClickOnce Security and Deployment](../deployment/clickonce-security-and-deployment.md)」を参照してください。

- アプリケーションで信頼レベルの昇格が必要かどうかを判断します。

   アプリケーションが完全な信頼を必要とする場合 (ユーザーのシステムへのフル アクセスなど)、*Mage.exe* の `-TrustLevel` オプションを使用してこれを設定できます。 アプリケーションのカスタム アクセス許可セットを定義する場合は、別のマニフェストからインターネットまたはイントラネット アクセス許可セクションをコピーし、ニーズに合わせて変更し、テキスト エディターまたは *MageUI.exe* を使用してアプリケーション マニフェストに追加することができます。 詳細については、「[信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)」を参照してください。

- Authenticode 証明書を取得します。

   Authenticode 証明書を使用して配置に署名する必要があります。 Visual Studio、*MageUI.exe*、または *MakeCert.exe* および *Pvk2Pfx.exe* ツールを使用して生成できます。または、証明機関 (CA) から証明書を取得できます。 信頼されたアプリケーションの配置を使用することを選択する場合は、すべてのクライアント コンピューターへの証明書の 1 回限りのインストールを実行する必要もあります。 詳細については、「 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)」を参照してください。

  > [!NOTE]
  > 証明機関から取得できる CNG 証明書を使用して配置に署名することもできます。

- アプリケーションに UAC 情報を含むマニフェストがないことを確認します。

   アプリケーションに、`<dependentAssembly>` 要素などのユーザー アカウント制御 (UAC) 情報を含むマニフェストが含まれているかどうかを確認する必要があります。 アプリケーション マニフェストを確認するには、Windows Sysinternals [Sigcheck](/sysinternals/downloads/sigcheck) ユーティリティを使用します。

   アプリケーションに UAC の詳細を含むマニフェストが含まれている場合は、UAC 情報を使用せずにアプリケーションを再構築する必要があります。 Visual Studio の C# プロジェクトの場合は、プロジェクトのプロパティを開き、[アプリケーション] タブを選択します。 **[マニフェスト]** ドロップダウン リストで、 **[マニフェストなしでアプリケーションを作成します]** を選択します。 Visual Studio の Visual Basic プロジェクトの場合は、プロジェクトのプロパティを開き、[アプリケーション] タブを選択し、 **[UAC 設定の表示]** をクリックします。 開かれたマニフェスト ファイルで、1 つの `<asmv1:assembly>` 要素内のすべての要素を削除します。

- アプリケーションでクライアント コンピューターの前提条件が必要かどうかを判断します。

   Visual Studio から配置される [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションでは、前提条件のインストール ブートストラップ (*setup.exe*) を配置に含めることができます。 このチュートリアルでは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置に必要な 2 つのマニフェストを作成します。 [Generatebootstrapper タスク](../msbuild/generatebootstrapper-task.md)を使用して、前提条件ブートストラップを作成できます。

### <a name="to-deploy-an-application-with-the-mageexe-command-line-tool"></a>Mage.exe コマンドライン ツールを使用してアプリケーションを配置するには

1. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置ファイルを格納するディレクトリを作成します。

2. 作成した配置ディレクトリで、バージョン サブディレクトリを作成します。 アプリケーションを初めて配置する場合は、バージョン サブディレクトリに **1.0.0.0** という名前を指定します。

   > [!NOTE]
   > 配置のバージョンは、アプリケーションのバージョンとは異なる場合があります。

3. 実行可能ファイル、アセンブリ、リソース、およびデータ ファイルを含むすべてのアプリケーション ファイルをバージョン サブディレクトリにコピーします。 必要に応じて、追加のファイルを含む追加のサブディレクトリを作成できます。

4. [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] または Visual Studio コマンド プロンプトを開き、バージョン サブディレクトリに移動します。

5. *Mage.exe* を呼び出して、アプリケーション マニフェストを作成します。 次のステートメントでは、Intel x86 プロセッサで実行するようにコンパイルされるコード用のアプリケーション マニフェストを作成します。

   ```cmd
   mage -New Application -Processor x86 -ToFile AppToDeploy.exe.manifest -name "My App" -Version 1.0.0.0 -FromDirectory .
   ```

   > [!NOTE]
   > 現在のディレクトリを示す、ドット (.) を `-FromDirectory` オプションの後に含めるようにしてください。 ドットを含めない場合は、アプリケーション ファイルのパスを指定する必要があります。

6. Authenticode 証明書でアプリケーション マニフェストに署名します。 *mycert.pfx* を証明書ファイルのパスに置き換えます。 *passwd* を、証明書ファイルのパスワードに置き換えます。

   ```cmd
   mage -Sign AppToDeploy.exe.manifest -CertFile mycert.pfx -Password passwd
   ```

   Visual Studio および Windows SDK で配布される .NET Framework 4.6.2 SDK 以降では、*mage.exe* は CNG と Authenticode 証明書を使用してマニフェストに署名します。 Authenticode 証明書の場合と同じコマンドライン パラメーターを使用します。

7. 配置ディレクトリのルートに移動します。

8. *Mage.exe* を呼び出して、配置マニフェストを生成します。 既定では、*Mage.exe* によって [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置がインストール済みのアプリケーションとしてマークされ、オンラインとオフラインの両方で実行できるようになります。 ユーザーがオンラインの場合のみアプリケーションを使用できるようにするには、`-Install` オプションを値 `false` で使用します。 既定値を使用し、ユーザーが Web サイトまたはファイル共有からアプリケーションをインストールする場合は、`-ProviderUrl` オプションの値が Web サーバーまたは共有上のアプリケーション マニフェストの場所を指していることを確認します。

   ```cmd
   mage -New Deployment -Processor x86 -Install true -Publisher "My Co." -ProviderUrl "\\myServer\myShare\AppToDeploy.application" -AppManifest 1.0.0.0\AppToDeploy.exe.manifest -ToFile AppToDeploy.application
   ```

9. Authenticode または CNG 証明書を使用して、配置マニフェストに署名します。

    ```cmd
    mage -Sign AppToDeploy.application -CertFile mycert.pfx -Password passwd
    ```

10. 配置ディレクトリ内のすべてのファイルを、配置先またはメディアにコピーします。 これには、Web サイトまたは FTP サイトのフォルダー、ファイル共有、または CD-ROM を指定できます。

11. アプリケーションをインストールするために必要な URL、UNC、または物理メディアをユーザーに提供します。 URL または UNC を提供する場合は、配置マニフェストの完全なパスをユーザーに与える必要があります。 たとえば、AppToDeploy が AppToDeploy ディレクトリ内の http://webserver01/ に配置される場合、完全な URL パスは http://webserver01/AppToDeploy/AppToDeploy.application になります。

### <a name="to-deploy-an-application-with-the-mageuiexe-graphical-tool"></a>MageUI.exe グラフィカル ツールを使用してアプリケーションを配置するには

1. [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 配置ファイルを格納するディレクトリを作成します。

2. 作成した配置ディレクトリで、バージョン サブディレクトリを作成します。 アプリケーションを初めて配置する場合は、バージョン サブディレクトリに **1.0.0.0** という名前を指定します。

   > [!NOTE]
   > 配置のバージョンは、アプリケーションのバージョンとは異なる可能性があります。

3. 実行可能ファイル、アセンブリ、リソース、およびデータ ファイルを含むすべてのアプリケーション ファイルをバージョン サブディレクトリにコピーします。 必要に応じて、追加のファイルを含む追加のサブディレクトリを作成できます。

4. *MageUI.exe* グラフィカル ツールを起動します。

   ```cmd
   MageUI.exe
   ```

5. メニューから **[ファイル]** 、 **[新規作成]** 、 **[アプリケーション マニフェスト]** の順に選択して、新しいアプリケーション マニフェストを作成します。

6. 既定の **[名前]** タブで、この配置の名前とバージョン番号を入力します。 また、アプリケーションのビルド対象である **プロセッサ** (x86 など) を指定します。

7. **[ファイル]** タブを選択し、 **[アプリケーション ディレクトリ]** テキスト ボックスの横にある省略記号 ( **...** ) ボタンを選択します。 **[フォルダーの参照]** ダイアログ ボックスが表示されます。

8. アプリケーション ファイルが含まれているバージョン サブディレクトリを選択し、 **[OK]** を選択します。

9. インターネット インフォメーション サービス (IIS) から配置する場合は、 **[作成時に .deploy 拡張子を持たないすべてのファイルに拡張子を追加する]** チェック ボックスがオンにします。

10. **[設定]** ボタンをクリックして、すべてのアプリケーション ファイルをファイル一覧に追加します。 アプリケーションに複数の実行可能ファイルが含まれる場合は、 **[ファイルの種類]** ドロップダウン リストから **[エントリ ポイント]** を選択して、この配置のメインの実行可能ファイルをスタートアップ アプリケーションとしてマークします。 (アプリケーションに実行可能ファイルが 1 つだけ含まれている場合は、*MageUI.exe* によってマークされます。)

11. **[必要なアクセス許可]** タブを選択し、アプリケーションでアサートする必要がある信頼レベルを選択します。 既定値は **FullTrust** です。これはほとんどのアプリケーションに適しています。

12. **[ファイル]** メニューから **[名前を付けて保存]** を選択します。 [署名オプション] ダイアログ ボックスが開き、アプリケーション マニフェストに署名するよう求められます。

13. ファイル システムにファイルとして保存されている証明書がある場合は、 **[証明書ファイルで署名する]** オプションを使用し、省略記号 ( **...** ) ボタンを使用してファイル システムから証明書を選択します。 次に、証明書のパスワードを入力します。

     または

     お使いのコンピューターからアクセスできる証明書ストアに証明書が保持されている場合は、 **[保存された証明書で署名する]** オプションを選択し、提供された一覧から証明書を選択します。

14. **[OK]** を選択して、アプリケーション マニフェストに署名します。 **[名前を付けて保存]** ダイアログ ボックスが表示されます。

15. **[名前を付けて保存]** ダイアログ ボックスで、バージョン ディレクトリを指定し、 **[保存]** を選択します。

16. メニューから **[ファイル]** 、 **[新規作成]** 、 **[配置マニフェスト]** を選択して、配置マニフェストを作成します。

17. **[名前]** タブで、この配置の名前とバージョン番号 (この例では **1.0.0.0**) を指定します。 また、アプリケーションのビルド対象である **プロセッサ** (x86 など) を指定します。

18. **[説明]** タブを選択し、 **[パブリッシャー]** と **[製品]** の値を指定します。 ( **[製品]** は、アプリケーションがオフラインで使用するためにクライアント コンピューターにインストールされるときに、Windows の [スタート] メニューでアプリケーションに表示される名前です。)

19. **[配置オプション]** タブを選択し、 **[開始場所]** テキスト ボックスで、Web サーバーまたは共有上のアプリケーション マニフェストの場所を指定します。 たとえば、 *\\\myServer\myShare\AppToDeploy.application* です。

20. 前の手順で *.deploy* 拡張子を追加した場合は、ここでも **[.deploy ファイル名拡張子を使用する]** を選択します。

21. **[更新オプション]** タブを選択し、このアプリケーションが更新される頻度を指定します。 <xref:System.Deployment.Application.UpdateCheckInfo> を使用して更新プログラムをアプリケーション自体で確認する場合は、 **[このアプリケーションの更新プログラムを確認する]** チェック ボックスをオフにします。

22. **[アプリケーション参照]** タブを選択し、 **[マニフェストの選択]** ボタンをクリックします。 開くダイアログ ボックスが表示されます。

23. 先ほど作成したアプリケーション マニフェストを選択し、 **[開く]** を選択します。

24. **[ファイル]** メニューから **[名前を付けて保存]** を選択します。 **[署名オプション]** ダイアログ ボックスが開き、配置マニフェストに署名するよう求められます。

25. ファイル システムにファイルとして保存されている証明書がある場合は、 **[証明書ファイルで署名する]** オプションを使用し、省略記号 ( **...** ) ボタンを使用してファイル システムから証明書を選択します。 次に、証明書のパスワードを入力します。

     または

     お使いのコンピューターからアクセスできる証明書ストアに証明書が保持されている場合は、 **[保存された証明書で署名する]** オプションを選択し、提供された一覧から証明書を選択します。

26. **[OK]** をクリックして、配置マニフェストに署名します。 **[名前を付けて保存]** ダイアログ ボックスが表示されます。

27. **[名前を付けて保存]** ダイアログ ボックスで、1 つ上のディレクトリである配置のルートに移動し、 **[保存]** を選択します。

28. 配置ディレクトリ内のすべてのファイルを、配置先またはメディアにコピーします。 これには、Web サイトまたは FTP サイトのフォルダー、ファイル共有、または CD-ROM を指定できます。

29. アプリケーションをインストールするために必要な URL、UNC、または物理メディアをユーザーに提供します。 URL または UNC を提供する場合は、配置マニフェストの完全なパスをユーザーに与える必要があります。 たとえば、AppToDeploy が AppToDeploy ディレクトリ内の http://webserver01/ に配置される場合、完全な URL パスは http://webserver01/AppToDeploy/AppToDeploy.application になります。

## <a name="next-steps"></a>次のステップ
 アプリケーションの新しいバージョンを配置する必要がある場合は、新しいバージョンにちなんだ名前の新しいディレクトリ (たとえば、1.0.0.1) を作成し、新しいディレクトリに新しいアプリケーション ファイルをコピーします。 次に、前述の手順に従って、新しいアプリケーション マニフェストを作成して署名し、配置マニフェストを更新して署名する必要があります。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では上位バージョンのみが更新されるので、*Mage.exe* `-New` および `-Update` 呼び出しの両方で同じ上位バージョンを指定するように注意してください。最も左の整数が最も重要です。 *MageUI.exe* を使用した場合は、配置マニフェストを開き、 **[アプリケーション参照]** タブを選択し、 **[マニフェストの選択]** ボタンをクリックし、更新されたアプリケーション マニフェストを選択することで、配置マニフェストを更新できます。

## <a name="see-also"></a>関連項目
- [Mage.exe (マニフェストの生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [MageUI.exe (マニフェスト生成および編集ツールのグラフィカル クライアント)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
