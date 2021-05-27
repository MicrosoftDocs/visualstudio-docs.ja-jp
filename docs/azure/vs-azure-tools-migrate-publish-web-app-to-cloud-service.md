---
title: クラウド サービスに Web アプリケーションを移行および発行する
description: Visual Studio を使用して、Azure クラウド サービスに Web アプリケーションを移行および発行する方法について説明します。
ms.custom: SEO-VS-2020
author: ghogen
manager: jmartens
ms.workload: azure-vs
ms.topic: how-to
ms.date: 11/10/2017
ms.author: ghogen
ms.openlocfilehash: 3154ffd50043ecc824ca44fcae86e54e511ab5bf
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844087"
---
# <a name="how-to-migrate-and-publish-a-web-application-to-an-azure-cloud-service-from-visual-studio"></a>方法: Visual Studio から Azure クラウド サービスへの Web アプリケーションの移行および発行

Azure のホスティング サービスとスケーラビリティを利用するには、Web アプリケーションを Azure クラウド サービスに 移行してデプロイします。 変更は最小限ですみます。 この記事ではクラウド サービスへのデプロイのみを説明します。App Service については、[Azure App Service での Web アプリのデプロイ](/azure/app-service/app-service-deploy-local-git)に関する記事をご覧ください。

> [!Important]
> この移行は特定の ASP.NET、WCF、および WCF ワークフロー プロジェクトでのみサポートされます。 ASP.NET Core プロジェクトではサポートされません。 「[サポートされているプロジェクト テンプレート](#supported-project-templates)」のセクションをご覧ください。

## <a name="migrate-a-project-to-cloud-services"></a>クラウド サービスにプロジェクトを移行する

1. ソリューション ノードを右クリックし、 **[追加]、[新しいプロジェクト]** の順に選択して、既存のソリューションに新しい **Azure クラウド サービス (クラシック)** プロジェクトを追加します。
1. **[新しい Microsoft Azure クラウド サービス (クラシック)]** ダイアログで、プロジェクトにロールを追加せずに [OK] をクリックします。
1. 新しく追加したクラウド サービス プロジェクトの下でロール ノードを右クリックし、 **[Add Web Role Project in solution...]\(ソリューションに Web ロール プロジェクトを追加する\)** を選択します。
1. **[ロール プロジェクトとの関連付け]** ダイアログで、Web ロールとして関連付けるプロジェクトを選択します。

   > [!Important]
   > この Web アプリケーションに必要な他のアセンブリまたはファイルがある場合は、それらのファイルのプロパティを手動で設定する必要があります。 これらのプロパティを設定する方法については、「[Include Files in the Service Package (サービス パッケージにファイルを取り込む)](vs-azure-tools-publishing-a-cloud-service.md#include-files-in-the-service-package)」をご覧ください。

### <a name="errors-and-warnings"></a>エラーと警告

警告またはエラーが発生する場合は、Azure にデプロイする前に解決すべき問題 (アセンブリの不足など) があることを示しています。

アプリケーションをビルドし、コンピューティング エミュレーターを使用してローカルで実行するか、Azure に発行すると、"指定されたパス、ファイル名、またはその両方が長すぎます。" というエラーが表示される場合があります。 このエラーは、Azure プロジェクトの完全修飾名が 146 文字を超えていることを示しています。 この問題を修正するには、パスが短くなるように別のフォルダーにソリューションを移動します。

警告をエラーとして処理する方法の詳細については、「 [Visual Studio を使用した Azure クラウド サービス プロジェクトの構成](vs-azure-tools-configuring-an-azure-project.md)」を参照してください。

### <a name="test-the-migration-locally"></a>移行をローカルでテストする

1. Visual Studio の **ソリューション エクスプローラー** で、追加されたクラウド サービス プロジェクトを右クリックし、**[スタートアップ プロジェクトに設定]** を選択します。
1. **[デバッグ] > [デバッグの開始]** (F5 キー) を選択して Azure デバッグ環境を起動します。 この環境では、特にさまざまな Azure サービスのエミュレーションを利用できます。

### <a name="use-an-azure-sql-database-for-your-application"></a>アプリケーションでの Azure SQL Database の使用

お使いの Web アプリケーションにオンプレミスの SQL Server データベースを使用する接続文字列がある場合、その代わりとして Azure SQL Database にデータベースを移行し、接続文字列を更新する必要があります。 このプロセスのガイダンスについては、次のトピックをご覧ください。

- [SQL Server データベースのクラウド内の SQL Database への移行](/azure/sql-database/sql-database-cloud-migrate)
- [.NET (C#) と Visual Studio で Azure SQL データベースに接続してデータベースに照会する](/azure/sql-database/sql-database-connect-query-dotnet-visual-studio)。

## <a name="publish-the-application-to-azure-cloud-service"></a>アプリケーションを Azure クラウド サービスに発行する

1. [Visual Studio からの Azure アプリケーションの発行またはデプロイの準備](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md)で説明しているように、必要なクラウド サービスとストレージ アカウントを Azure サブスクリプションで作成します。
1. Visual Studio でアプリケーション プロジェクトを右クリックし、**[Microsoft Azure に公開...]** を選択します ([発行...] コマンドではありません)。
1. 表示された **[Azure アプリケーションの発行]** で、アカウントを使用して Azure サブスクリプションにサインインし、**[次へ > ]** を選択します。
1. **[設定] > [共通設定]** タブで、対象のクラウド サービスおよび環境と構成を **[クラウド サービス]** ボックスの一覧から選択します。
1. **[設定] > [詳細設定]** の順に移動し、使用するストレージ アカウントを選択してから **[次へ > ]** を選択します。
1. **[診断]** で、Application Insights に情報を送信するかどうかを選択します。
1. **[次へ > ]** を選択して概要を表示し、**[発行]** を選択してデプロイを開始します。
1. Visual Studio でアクティビティ ログ ウィンドウが開かれ、進行状況を追跡できます。

    ![VST_AzureActivityLog](./media/vs-azure-tools-migrate-publish-web-app-to-cloud-service/IC744149.png)

1. (省略可能) デプロイ プロセスをキャンセルするには、アクティビティ ログの行項目を右クリックし、**[取り消して削除]** を選択します。 このコマンドによりデプロイ プロセスが停止し、Azure からデプロイ環境が削除されます。 注: このデプロイ環境をデプロイ後に削除するには、[Azure Portal](https://portal.azure.com) を使用する必要があります。
1. (省略可能) ロール インスタンスが起動すると、Visual Studio の **[サーバー エクスプローラー] > [クラウド サービス]** ノードに、デプロイ環境が自動的に表示されます。 ここから、個々のロール インスタンスの状態を確認できます。
1. デプロイ後にアプリケーションにアクセスするには、**[Azure の活動ログ]** に **[完了]** の状態と URL が表示されているときに、デプロイの横の矢印を選択します。 Azure から特定の種類の Web アプリケーションを起動する方法の詳細については、次の表をご覧ください。

## <a name="using-the-compute-emulator-and-starting-application-in-azure"></a>コンピューティング エミュレーターを使用して Azure でアプリケーションを起動する

**[デバッグ] > [デバッグの開始]** (F5 キー) を選択すると、Visual Studio デバッガーに接続されているブラウザーでアプリケーションのすべての種類を起動できます。 空の ASP.NET Web アプリケーション プロジェクトでは、まずアプリケーションに `.aspx` ページを追加し、Web プロジェクトのスタート ページとして設定する必要があります。

次の表に、Azure でアプリケーションを起動する方法の詳細を示します。

| Web アプリケーションの種類 | Azure での実行 |
| --- | --- |
| ASP.NET Web アプリケーション<br/>(MVC 2、MVC 3、MVC 4 を含みます) | **[デプロイ]** タブで **[Azure の活動ログ]** の URL を選択します。 |
| 空の ASP.NET Web アプリケーション | アプリケーションの既定の `.aspx` ページがある場合は、**[デプロイ]** タブで **[Azure の活動ログ]** の URL を選択します。 別のページに移動するには、ブラウザーに `<deployment_url>/<page_name>.aspx` の形式で URL を入力します。 |
| WCF サービス アプリケーション<br/>WCF ワークフロー サービス アプリケーション | `.svc` ファイルを WCF サービス プロジェクトのスタート ページに設定します。 次に、`<deployment_url>/<service_file>.svc` に移動します。 |
| ASP.NET 動的エンティティ<br/>ASP.NET 動的データ LINQ to SQL | 接続文字列を更新します (次のセクションで説明します)。 次に、`<deployment_url>/<page_name>.aspx` に移動します。 Linq to SQL については、Azure SQL データベースを使用する必要があります。 |

## <a name="update-a-connection-string-for-aspnet-dynamic-entities"></a>ASP.NET 動的エンティティの接続文字列の更新

1. (#Use-an-azuresql-database-for-your-application) で前述したように、ASP.NET 動的エンティティ Web アプリケーション用の SQL Azure データベースを作成します。
1. Azure Portal から、このデータベースに必要なテーブルとフィールドを追加します。
1. `web.config` ファイルで次の形式の接続文字列を指定し、ファイルを保存します。

    ```xml
    <add name="tempdbEntities"
     connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;data source=<server name>\SQLEXPRESS;initial catalog=<database name>;integrated security=True;multipleactiveresultsets=True;App=EntityFramework&quot;"
     providerName="System.Data.EntityClient"/>
    ```

    SQL Azure データベースの ADO.NET 接続文字列の *connectionString* 値を次のように更新します。

    ```xml
    <add name="tempdbEntities"
     connectionString="metadata=res://*/Model1.csdl|res://*/Model1.ssdl|res://*/Model1.msl;provider=System.Data.SqlClient;provider connection string=&quot;Server=tcp:<SQL Azure server name>.database.windows.net,1433;Database=<database name>;User ID=<user name>;Password=<password>;Trusted_Connection=False;Encrypt=True;multipleactiveresultsets=True;App=EntityFramework&quot;"
     providerName="System.Data.EntityClient"/>
    ```

## <a name="supported-project-templates"></a>サポートされているプロジェクト テンプレート

クラウド サービスに移行および発行できるアプリケーションは、次の表にあるテンプレートのいずれかを使用している必要があります。 ASP.NET Core はサポートされていません。

| テンプレート グループ | プロジェクト テンプレート |
| --- | --- |
| Web | ASP.NET Web アプリケーション (.NET Framework) |
| Web | ASP.NET MVC 2 Web アプリケーション |
| Web | ASP.NET MVC 3 Web アプリケーション |
| Web | ASP.NET MVC 4 Web アプリケーション |
| Web | 空の ASP.NET Web アプリケーション (またはサイト) |
| Web | 空の ASP.NET MVC 2 Web アプリケーション |
| Web | ASP.NET 動的データ エンティティ Web アプリケーション |
| Web | ASP.NET 動的データ LINQ to SQL Web アプリケーション |
| WCF | WCF サービス アプリケーション |
| WCF | WCF ワークフロー サービス アプリケーション |
| ワークフロー | WCF ワークフロー サービス アプリケーション |

## <a name="next-steps"></a>次のステップ

- [Visual Studio からの Azure アプリケーションの発行またはデプロイの準備](vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md)
- [名前付き認証資格情報の設定](vs-azure-tools-setting-up-named-authentication-credentials.md)
