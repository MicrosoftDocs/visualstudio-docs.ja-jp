---
title: PowerShell を使用し、開発およびテスト環境に発行する
description: Visual Studio から Windows PowerShell スクリプトを使用して、開発環境とテスト環境に発行する方法について説明します。
ms.custom: SEO-VS-2020
author: ghogen
manager: jmartens
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/11/2016
ms.author: ghogen
ms.openlocfilehash: e0486e3a13b1c6b6ba421c5c0a97788f514413e1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99843957"
---
# <a name="using-windows-powershell-scripts-to-publish-to-dev-and-test-environments"></a>Windows PowerShell スクリプトを使用した開発環境およびテスト環境の発行

Visual Studio で Web アプリケーションを作成するときに、Azure への Web サイトの発行を自動化するための Windows PowerShell スクリプトを生成できます。後でこのスクリプトを使用して、Web サイトを Azure App Service の Web アプリとして、または仮想マシンとして Azure に発行できます。 Windows PowerShell スクリプトは、要件に合わせて Visual Studio エディターで編集および拡張できます。また、既存のビルド スクリプト、テスト スクリプト、発行スクリプトと統合することもできます。

これらのスクリプトを使用すると、サイトのカスタマイズされたバージョン (開発およびテスト環境とも呼ばれます) を、一時的に使用するためにプロビジョニングできます。 たとえば、テスト スイートの実行、バグの再現、バグ修正のテスト、提案された変更の試験的な適用を行うために、Azure 仮想マシンまたは Web サイトのステージング スロットで Web サイトの特定のバージョンをセットアップしたり、デモまたはプレゼンテーション用にカスタム環境をセットアップしたりできます。 プロジェクトを発行するスクリプトを作成したら、必要に応じてそのスクリプトを再実行することで、同一の環境を再作成できます。また、Web アプリケーションの独自のビルドでスクリプトを実行して、テスト用のカスタム環境を作成することもできます。

## <a name="prerequisites"></a>必須コンポーネント

* **Azure ワークロード** がインストールされた Visual Studio 2015 以降、または Visual Studio 2013 と Azure SDK 2.3 以降。 [Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads) ページをご覧ください。 (Web プロジェクトのスクリプトの生成に Azure SDK は不要です。 この機能は、クラウド サービスの Web ロールではなく、Web プロジェクトを対象としています。)
* Azure PowerShell 0.7.4 以降。 「 [Azure PowerShell のインストールと構成の方法](/powershell/azure/overview)」を参照してください。
* [Windows PowerShell 3.0](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770458(v=ws.10)) 以降。

## <a name="additional-tools"></a>その他のツール

Azure 開発のために、Visual Studio で PowerShell を使用するための他のツールとリソースが用意されています。 「 [PowerShell Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=AdamRDriscoll.PowerShellToolsforVisualStudio2015)」をご覧ください。

## <a name="generating-the-publish-scripts"></a>発行スクリプトの生成

[こちらの手順](/azure/virtual-machines/windows/classic/web-app-visual-studio)に従って新しいプロジェクトを作成するときに、Web サイトをホストする仮想マシンの発行スクリプトを生成できます。 [Azure App Service の Web アプリの発行スクリプトを生成](/azure/app-service/scripts/app-service-powershell-deploy-github)することもできます。

## <a name="scripts-that-visual-studio-generates"></a>Visual Studio によって生成されるスクリプト

Visual Studio では、**PublishScripts** というソリューション レベルのフォルダーが生成されます。このフォルダーには、2 つの Windows PowerShell ファイルが含まれます。1 つは仮想マシンまたは Web サイト用の公開スクリプト、もう 1 つはスクリプトで使用できる関数が含まれるモジュールです。 また、Visual Studio では、デプロイするプロジェクトの詳細を指定した JSON 形式のファイルも生成されます。

### <a name="windows-powershell-publish-script"></a>Windows PowerShell 発行スクリプト

発行スクリプトには、Web サイトまたは仮想マシンへのデプロイに必要な発行手順が含まれています。 Visual Studio では、Windows PowerShell の開発で構文の色を使用できます。 関数にはヘルプが用意されています。また、要件の変更に合わせて、スクリプトの関数を自由に編集できます。

### <a name="windows-powershell-module"></a>Windows PowerShell モジュール

Visual Studio によって生成される Windows PowerShell モジュールには、発行スクリプトで使用する関数が含まれています。 これらの Azure PowerShell 関数は、変更することを想定したものではありません。 「 [Azure PowerShell のインストールと構成の方法](/powershell/azure/overview)」を参照してください。

### <a name="json-configuration-file"></a>JSON 構成ファイル

JSON ファイルは [**構成**] フォルダーに作成されます。このファイルには、Azure にデプロイするリソースを正確に指定する構成データが含まれています。 Visual Studio によって生成されるファイルの名前は、プロジェクト名-WAWS-dev.json (Web サイトを作成した場合)、またはプロジェクト名-VM-dev.json (仮想マシンを作成した場合) です。 Web サイトの作成時に生成される JSON 構成ファイルの例を次に示します。 ほとんどの値がわかりやすく記述されています。 Web サイト名は Azure によって生成されるので、プロジェクト名と一致しない場合があります。

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```

仮想マシンを作成するときには、JSON 構成ファイルは次のようになります。 クラウド サービスは、仮想マシンのコンテナーとして作成されます。 仮想マシンには、HTTP および HTTPS 経由の Web アクセスに使用する通常のエンドポイントと、Web Deploy のエンドポイントが含まれます。Web 配置のエンドポイントにより、ローカル コンピューター、リモート デスクトップ、Windows PowerShell から Web サイトに発行できます。

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

JSON 構成を編集して、発行スクリプトの実行時の動作を変更できます。 `cloudService` セクションと `virtualMachine` セクションは必須ですが、`databases` セクションは不要であれば削除できます。 Visual Studio によって生成される既定の構成ファイルに含まれる空のプロパティは省略可能です。既定の構成ファイルで値が指定されているプロパティは必須です。

Azure に運用サイトが 1 つだけ存在するのでなく、複数のデプロイ環境 (スロット) を持つ Web サイトがある場合は、JSON 構成ファイルの Web サイト名にスロット名を含めることができます。 たとえば、**mysite** という名前の Web サイトがあり、そのスロットに **test** という名前を付けた場合、URI は `mysite-test.cloudapp.net` となります。ただし、構成ファイルで使用する正しい名前は mysite(test) です。 これが可能なのは、サブスクリプションに Web サイトとスロットが既に存在している場合に限られます。 存在していない場合は、スロットを指定せずにスクリプトを実行して Web サイトを作成し、[Azure Portal](https://portal.azure.com/) でスロットを作成してから、変更した Web サイト名でスクリプトを実行します。 Web アプリのデプロイ スロットの詳細については、「[Azure App Service の Web アプリのステージング環境を設定する](/azure/app-service/web-sites-staged-publishing)」をご覧ください。

## <a name="how-to-run-the-publish-scripts"></a>発行スクリプトの実行方法

これまでに Windows PowerShell スクリプトを一度も実行したことがない場合は、まず実行ポリシーを設定して、スクリプトを実行できるようにする必要があります。 このポリシーは、Windows PowerShell スクリプトが、スクリプトを実行するマルウェアやウイルスに対して脆弱である場合に、それらのスクリプトをユーザーが実行できないようにするためのセキュリティ機能です。

### <a name="run-the-script"></a>スクリプトを実行する

1. プロジェクトの Web 配置パッケージを作成します。 Web 配置パッケージは、Web サイトまたは仮想マシンにコピーするファイルが含まれた圧縮アーカイブ (.zip ファイル) です。 Visual Studio で、任意の Web アプリケーションの Web 配置パッケージを作成できます。

   ![Web 配置パッケージの作成](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

   詳細については、「 [方法: Visual Studio で Web 配置パッケージを作成する](/previous-versions/aspnet/dd465323(v=vs.110))」をご覧ください。 「[Customizing and extending the publish scripts](#customizing-and-extending-the-publish-scripts)」 (発行スクリプトのカスタマイズと拡張) で説明するように、Web 配置パッケージの作成を自動化することもできます。

1. **ソリューション エクスプローラー** でスクリプトのコンテキスト メニューを開き、**[PowerShell ISE で開く]** をクリックします。
1. このコンピューターで Windows PowerShell スクリプトを初めて実行した場合は、管理特権でコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

1. 次のコマンドを使用して Azure にサインインします。

    ```powershell
    Add-AzureAccount
    ```

    メッセージが表示されたら、ユーザー名とパスワードを入力します。

    スクリプトを自動化すると、この方法で Azure 資格情報を提供できなくなります。 代わりに、`.publishsettings` ファイルを使用して、資格情報を提供する必要があります。 1 回だけ、**Get-AzurePublishSettingsFile** コマンドを使用してこのファイルを Azure からダウンロードしたら、それ以降は **Import-AzurePublishSettingsFile** を使用してファイルをインポートします。 詳しい手順については、「 [Azure PowerShell のインストールおよび構成方法](/powershell/azure/overview)」をご覧ください。

1. (省略可能) Web アプリケーションを発行せずに、仮想マシン、データベース、Web サイトなどの Azure リソースを作成する場合は、**-Configuration** 引数を JSON 構成ファイルに設定した **Publish-WebApplication.ps1** コマンドを使用します。 このコマンド ラインでは、JSON 構成ファイルを使用して作成するリソースを指定します。 他のコマンド ライン引数には既定の設定を使用するため、リソースは作成されますが、Web アプリケーションは発行されません。 –Verbose オプションを使用すると、進行状況の詳細情報が得られます。

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

1. 次の例に示すように **Publish-WebApplication.ps1** コマンドを使用してスクリプトを起動し、Web アプリケーションを発行します。 サブスクリプション名、発行パッケージ名、仮想マシンの資格情報、データベース サーバーの資格情報など、他の引数の既定の設定をオーバーライドする必要がある場合は、それらのパラメーターを指定します。 **–Verbose** オプションを使用すると、発行処理の進行状況の詳細が表示されます。

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    仮想マシンを作成する場合、コマンドは次のようになります。 この例では、複数のデータベースの資格情報を指定する方法も示しています。 これらのスクリプトで作成される仮想マシンでは、SSL 証明書は信頼されたルート証明機関のものではありません。 したがって、 **–AllowUntrusted** オプションを使用する必要があります。

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    このスクリプトではデータベースを作成できますが、データベース サーバーは作成されません。 データベース サーバーを作成する場合は、Azure モジュールの **New-AzureSqlDatabaseServer** 関数を使用します。

## <a name="customizing-and-extending-the-publish-scripts"></a>発行スクリプトのカスタマイズと拡張

発行スクリプトと JSON 構成ファイルはカスタマイズできます。 **AzureWebAppPublishModule.psm1** Windows PowerShell モジュールの関数は、変更することを想定したものではありません。 別のデータベースを指定したり、仮想マシンの一部のプロパティを変更したりする場合は、JSON 構成ファイルを編集します。 プロジェクトのビルドとテストを自動化するためにスクリプトの機能を拡張する場合は、 **Publish-WebApplication.ps1** の関数スタブを実装できます。

プロジェクトのビルドを自動化するには、次のコード例に示すように、MSBuild を呼び出すコードを `New-WebDeployPackage` に追加します。 MSBuild コマンドのパスは、インストールされている Visual Studio のバージョンによって異なります。 正しいパスを取得するには、この例に示すように、 **Get-MSBuildCmd** 関数を使用します。

### <a name="to-automate-building-your-project"></a>プロジェクトのビルドを自動化するには

1. グローバル パラメーター セクションに `$ProjectFile` パラメーターを追加します。

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

1. `Get-MSBuildCmd` 関数をスクリプト ファイルにコピーします。

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

1. `New-WebDeployPackage` を次のコードで置き換え、`$msbuildCmd` を構築している行のプレースホルダーを置き換えます。 このコードは Visual Studio 2019 用です。 Visual Studio 2017 を使用している場合は、**VisualStudioVersion** プロパティを `15.0` に変更します (Visual Studio 2015 の場合は '14.0'、Visual Studio 2013 の場合は `12.0`)。

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function to build and package your web application
    ```

    Web アプリケーションをビルドするには、MsBuild.exe を使用します。 詳細については、[MSBuild コマンドライン リファレンス](../msbuild/msbuild-command-line-reference.md)を参照してください

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=16.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-the-build-command"></a>ビルド コマンドの実行を開始します。

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain the project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct the path to web deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get the full path for the web deploy zip package. This is required for MSDeploy to work
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. Web アプリでは `$Config = Read-ConfigFile $Configuration`、仮想マシンでは `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` の前に `New-WebDeployPackage` 関数を呼び出します。

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

1. 次の例に示すように、`$Project` 引数を渡して、カスタマイズしたスクリプトをコマンド ラインから起動します。

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    アプリケーションのテストを自動化するには、 `Test-WebApplication`にコードを追加します。 **Publish-WebApplication.ps1** で、これらの関数が呼び出されている行のコメントを必ず解除してください。 これを実装しない場合は、Visual Studio でプロジェクトを手動でビルドし、発行スクリプトを実行して Azure に発行できます。

## <a name="publishing-function-summary"></a>発行関数の概要
Windows PowerShell コマンド プロンプトで使用できる関数のヘルプを取得するには、 `Get-Help function-name`コマンドを使用します。 ヘルプには、パラメーターのヘルプと例が含まれています。 スクリプト ソース ファイル **AzureWebAppPublishModule.psm1** と **Publish-WebApplication.ps1** にも、同じヘルプ テキストが含まれています。 スクリプトとヘルプは、Visual Studio の言語でローカライズされています。

**AzureWebAppPublishModule**

| 関数名 | 説明 |
| --- | --- |
| Add-AzureSQLDatabase |新しい Azure SQL データベースを作成します。 |
| Add-AzureSQLDatabases |Visual Studio によって生成される JSON 構成ファイルの値から Azure SQL データベースを作成します。 |
| Add-AzureVM |Azure 仮想マシンを作成し、デプロイされた VM の URL を返します。 この関数は、前提条件を設定してから、 **New-AzureVM** 関数 (Azure モジュール) を呼び出して新しい仮想マシンを作成します。 |
| Add-AzureVMEndpoints |新しい入力エンドポイントを仮想マシンに追加し、新しいエンドポイントを持つ仮想マシンを返します。 |
| Add-AzureVMStorage |現在のサブスクリプションに新しい Azure ストレージ アカウントを作成します。 アカウントの名前は "devtest" で始まり、その後に一意の英数字の文字列が続きます。 この関数は、新しいストレージ アカウントの名前を返します。 新しいストレージ アカウントの場所またはアフィニティ グループを指定します。 |
| Add-AzureWebsite |指定された名前と場所を使用して Web サイトを作成します。 この関数は、Azure モジュールの **New-AzureWebsite** 関数を呼び出します。 指定された名前の Web サイトがサブスクリプションにまだ含まれていない場合、この関数はその Web サイトを作成し、Web サイト オブジェクトを返します。 それ以外の場合は `$null`を返します。 |
| Backup-Subscription |現在の Azure サブスクリプションを、スクリプト スコープ内の `$Script:originalSubscription` 変数に保存します。 この関数は、現在の Azure サブスクリプション (`Get-AzureSubscription -Current` によって取得) とそのストレージ アカウント、およびこのスクリプトによって変更されたサブスクリプション (`$UserSpecifiedSubscription` 変数に格納) とそのストレージ アカウントをスクリプト スコープ内に保存します。 値を保存することで、現在の状態が変わった場合に、`Restore-Subscription` などの関数を使用して、現在の元のサブスクリプションとストレージ アカウントを現在の状態に復元できます。 |
| Find-AzureVM |指定された Azure 仮想マシンを取得します。 |
| Format-DevTestMessageWithTime |メッセージの先頭に日付と時刻を追加します。 この関数は、エラー ストリームと詳細ストリームに書き込まれるメッセージを対象としています。 |
| Get-AzureSQLDatabaseConnectionString |Azure SQL データベースに接続するための接続文字列をアセンブルします。 |
| Get-AzureVMStorage |指定された場所またはアフィニティ グループの最初のストレージ アカウントの名前を "devtest *" という名前パターン (大文字と小文字を区別しない) で返します。"devtest*" ストレージ アカウントが場所またはアフィニティ グループと一致しない場合、そのアカウントは無視されます。 場所またはアフィニティ グループを指定します。 |
| Get-MSDeployCmd |MsDeploy.exe ツールを実行するためのコマンドを返します。 |
| New-AzureVMEnvironment |JSON 構成ファイル内の値と一致する、サブスクリプション内の仮想マシンを検出または作成します。 |
| Publish-WebPackage |MsDeploy.exe と Web 発行パッケージの .ZIP ファイルを使用して、リソースを Web サイトにデプロイします。 この関数では出力は生成されません。 MSDeploy.exe の呼び出しに失敗した場合は、例外がスローされます。 さらに詳しい出力を取得するには、 **-Verbose** オプションを使用します。 |
| Publish-WebPackageToVM |パラメーター値を検証してから、 **Publish-WebPackage** 関数を呼び出します。 |
| Read-ConfigFile |JSON 構成ファイルを検証し、選択した値のハッシュ テーブルを返します。 |
| Restore-Subscription |現在のサブスクリプションを元のサブスクリプションにリセットします。 |
| Test-AzureModule |インストールされている Azure モジュールのバージョンが 0.7.4 以降の場合は、 `$true` を返します。 モジュールがインストールされていないか以前のバージョンの場合は、 `$false` を返します。 この関数にはパラメーターはありません。 |
| Test-AzureModuleVersion |Azure モジュールのバージョンが 0.7.4 以降の場合は、 `$true` を返します。 モジュールがインストールされていないか以前のバージョンの場合は、 `$false` を返します。 この関数にはパラメーターはありません。 |
| Test-HttpsUrl |入力 URL を System.Uri オブジェクトに変換します。 URL が絶対 URL で、スキームが https の場合は、 `$True` を返します。 URL が相対 URL の場合、スキームが https でない場合、または入力文字列を URL に変換できない場合は、 `$false` を返します。 |
| Test-Member |プロパティまたはメソッドがオブジェクトのメンバーである場合は、 `$true` を返します。 それ以外の場合、`$false` を返します。 |
| Write-ErrorWithTime |現在の時刻が先頭に付加されたエラー メッセージを書き込みます。 この関数は、 **Format-DevTestMessageWithTime** 関数を呼び出して先頭に時刻を付加してから、メッセージをエラー ストリームに書き込みます。 |
| Write-HostWithTime |現在の時刻が先頭に付加されたメッセージをホスト プログラムに書き込みます (**Write-Host**)。 ホスト プログラムへの書き込み結果はさまざまです。 Windows PowerShell をホストするほとんどのプログラムが、これらのメッセージを標準出力に書き込みます。 |
| Write-VerboseWithTime |現在の時刻が先頭に付加された詳細メッセージを書き込みます。 この関数は **Write-Verbose** を呼び出すので、**Verbose** パラメーターを指定してスクリプトを実行した場合、または **VerbosePreference** 設定が **Continue** に設定されている場合にのみ、メッセージが表示されます。 |

**Publish-WebApplication**

| 関数名 | 説明 |
| --- | --- |
| New-AzureWebApplicationEnvironment |Web サイトや仮想マシンなどの Azure リソースを作成します。 |
| New-WebDeployPackage |この関数は実装されていません。 この関数にコマンドを追加すると、プロジェクトをビルドできます。 |
| Publish-AzureWebApplication |Azure に Web アプリケーションを発行します。 |
| Publish-WebApplication |Visual Studio Web プロジェクト用の Web アプリ、仮想マシン、SQL データベース、ストレージ アカウントを作成し、デプロイします。 |
| Test-WebApplication |この関数は実装されていません。 この関数にコマンドを追加すると、アプリケーションをテストできます。 |

## <a name="next-steps"></a>次のステップ
PowerShell スクリプトの詳細については、「[Windows PowerShell を使用したスクリプト](/powershell/scripting/overview)」をお読みください。また、「[スクリプト センター](https://azure.microsoft.com/documentation/scripts/)」で他の Azure PowerShell スクリプトもご覧ください。