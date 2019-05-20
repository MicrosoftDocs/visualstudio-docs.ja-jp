---
ms.openlocfilehash: 69f4f4c2b55670d510652b44a203b9f0eafcc53a
ms.sourcegitcommit: 2ee11676af4f3fc5729934d52541e9871fb43ee9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65846428"
---

1. IIS 管理コンソールを閉じて、もう一度開き、UI の更新された構成オプションを表示します。

2. IIS で **[既定の Web サイト]** を右クリックして、**[展開]** > **[Web 配置による発行の有効化]** の順に選びます。

    ![Web 配置の構成](../../deployment/media/tutorial-configure-web-deploy-publishing.png)

3. **[Web 配置による発行の有効化]** ダイアログ ボックスで、この設定を確認します。

4. **[設定]** をクリックします。

    **[結果]** パネルで、出力に特定のユーザーに付与されているアクセス権が示され、*.publishsettings* のファイル拡張子が付いたファイルがダイアログ ボックスで示されている場所に作成されています。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <publishData>
      <publishProfile
        publishUrl="https://myhostname:8172/msdeploy.axd"
        msdeploySite="Default Web Site"
        destinationAppUrl="http://myhostname:80/"
        mySQLDBConnectionString=""
        SQLServerDBConnectionString=""
        profileName="Default Settings"
        publishMethod="MSDeploy"
        userName="myhostname\myusername" />
    </publishData>
    ```

    ご利用の Windows Server と IIS の構成によって、XML ファイルには異なる値が表示されます。 表示される値に関する詳細のいくつかを次に示します。

   * `publishUrl` 属性で参照されている *msdeploy.axd* ファイルは、Web 配置用に動的に作成された HTTP ハンドラー ファイルです。 (テスト目的で、通常、`http://myhostname:8172` も動作します。)
   * `publishUrl` ポートは、Web 配置の既定値であるポート 8172 に設定されます。
   * `destinationAppUrl` ポートは、IIS の既定値であるポート 80 に設定されます。
   * (後の手順で) Visual Studio でホスト名を使用してリモート ホストに接続できない場合は、ホスト名の代わりに IP アドレスでテストします。

     > [!NOTE]
     > Azure VM で実行されている IIS に発行する場合は、ネットワーク セキュリティ グループの Web 配置ポートと IIS ポートを開く必要があります。 詳細については、[IIS のインストールと実行](/azure/virtual-machines/windows/quick-create-portal#install-web-server)に関するページを参照してください。

5. Visual Studio を実行しているコンピューターにこのファイルをコピーします。
