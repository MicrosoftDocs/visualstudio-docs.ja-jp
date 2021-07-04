---
title: ネットワーク エラーまたはプロキシ エラーをトラブルシューティングする
description: ファイアウォールまたはプロキシ サーバーの内側で Visual Studio をインストールし使用するときに発生する可能性があるネットワークまたはプロキシに関連するエラーの解決策を探します。
ms.date: 10/29/2019
ms.topic: troubleshooting
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
- list of domains, locations, URLs, Visual Studio
- proxy errors, Visual Studio
ms.assetid: ''
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 5e7d54b4e7777b3569031e96760699e7c075245f
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306827"
---
# <a name="troubleshoot-network-related-errors-when-you-install-or-use-visual-studio"></a>Visual Studio をインストールまたは使用するときのネットワーク関連のエラーのトラブルシューティング

ファイアウォールまたはプロキシ サーバーの内側で Visual Studio をインストールし使用するときに発生する可能性があるネットワークまたはプロキシに関連する最も代表的なエラーの解決策を紹介します。

## <a name="error-proxy-authorization-required"></a>エラー :"プロキシ認証を要求するエラー"

このエラーは通常、ユーザーがプロキシ サーバーを経由してインターネットに接続し、Visual Studio が一部のネットワーク リソースに対して行った呼び出しをプロキシ サーバーがブロックしたときに発生します。

### <a name="to-fix-this-proxy-error"></a>このプロキシ エラーを解決するには

- Visual Studio を再起動します。 プロキシ認証のダイアログ ボックスが表示されます。 ダイアログ ボックスに入力を求めるメッセージが表示されたら、資格情報を入力します。

- Visual Studio を再起動しても問題が解決しない場合は、考えられる原因は、プロキシ サーバーが http:&#47;&#47;go.microsoft.com のアドレスに対しては資格情報を要求せず、&#42;.visualStudio.microsoft.com のアドレスに対しては資格情報を要求することです。 これらのサーバーの場合、次の URL を許可リストに追加し、Visual Studio におけるあらゆるサインイン シナリオのブロックを解除することを検討する必要があります。

  - &#42;.windows.net

  - &#42;.microsoftonline.com

  - &#42;.visualstudio.microsoft.com

  - &#42;.microsoft.com

  - &#42;.live.com

- http:&#47;&#47;go.microsoft.com を許可リストから削除すると、Visual Studio を再起動したとき、http:&#47;&#47;go.microsoft.com のアドレスとサーバー エンドポイントの両方にプロキシ認証ダイアログが表示されます。

  または

- プロキシで既定の資格情報を使用する場合は、次のアクションを実行します。

::: moniker range="vs-2017"

  1. **devenv.exe.config** (devenv.exe 構成ファイル) を、 **%ProgramFiles%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE** または **%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE** で見つけます。

  2. 構成ファイル内で、`<system.net>` ブロックを探し、次のコードを追加します。

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress="http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      `proxyaddress="<http://<yourproxy:port#>`には、使用しているネットワークの正しいプロキシ アドレスを挿入する必要があります。

     > [!NOTE]
     > 詳細については、「[&lt;defaultProxy&gt; 要素 (ネットワーク設定)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings/)」ページおよび「[&lt;proxy&gt; 要素 (ネットワーク設定)](/dotnet/framework/configure-apps/file-schema/network/proxy-element-network-settings)」ページを参照してください。

::: moniker-end

::: moniker range=">=vs-2019"

  1. **devenv.exe.config** (the devenv.exe 構成ファイル) を、 **%ProgramFiles%\Microsoft Visual Studio\2019\Enterprise\Common7\IDE** または **%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Enterprise\Common7\IDE** で見つけます。

  2. 構成ファイル内で、`<system.net>` ブロックを探し、次のコードを追加します。

      ```xml
      <defaultProxy enabled="true" useDefaultCredentials="true">
          <proxy bypassonlocal="True" proxyaddress="http://<yourproxy:port#>"/>
      </defaultProxy>
      ```

      `proxyaddress="<http://<yourproxy:port#>`には、使用しているネットワークの正しいプロキシ アドレスを挿入する必要があります。

     > [!NOTE]
     > 詳細については、「[&lt;defaultProxy&gt; 要素 (ネットワーク設定)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings/)」ページおよび「[&lt;proxy&gt; 要素 (ネットワーク設定)](/dotnet/framework/configure-apps/file-schema/network/proxy-element-network-settings)」ページを参照してください。

::: moniker-end

## <a name="error-disconnected-from-visual-studio-when-attempting-to-report-a-problem"></a>エラー :問題を報告しようとするときの "Visual Studio から切断されました"

このエラーは通常、ユーザーがプロキシ サーバーを経由してインターネットに接続し、Visual Studio が一部のネットワーク リソースに対して行った呼び出しをプロキシ サーバーがブロックしたときに発生します。

### <a name="to-fix-this-proxy-error"></a>このプロキシ エラーを解決するには

1. **feedback.exe.config** (feedback.exe の構成ファイル) を次の場所から探します: **%ProgramFiles(x86)%\Microsoft Visual Studio\Installer** または **%ProgramFiles%\Microsoft Visual Studio\Installer**。

2. 構成ファイル内に次のコードが存在するかどうかを確認します。コードが存在しない場合は、最後の `</configuration>` 行の前に追加します。

   ```xml
   <system.net>
       <defaultProxy useDefaultCredentials="true" />
   </system.net>
   ```

## <a name="error-the-underlying-connection-was-closed"></a>エラー: "接続が切断されました"

ファイアウォールが設定されたプライベート ネットワークで Visual Studio を使用する場合、Visual Studio を一部のネットワーク リソースに接続できない可能性があります。 これらのリソースには、サインインとライセンス取得のための Azure DevOps Services、NuGet、および Azure サービスが含まれます。 Visual Studio でこれらのリソースのいずれかに接続できない場合は、次のエラー メッセージが表示されることがあります。

  **基になる接続が閉じられました: 送信時に、予期しないエラーが発生しました**

Visual Studio ではトランスポート層セキュリティ (TLS) 1.2 プロトコルを使用して、ネットワーク リソースに接続します。 Visual Studio で TLS 1.2 を使用している場合、一部のプライベート ネットワーク上のセキュリティ アプライアンスによって特定のサーバー接続がブロックされます。

### <a name="to-fix-this-connection-error"></a>この接続エラーを解決するには

次の URL の接続を有効にします。

- https:&#47;&#47;management.core.windows.net

- https:&#47;&#47;app.vssps.visualstudio.com

- https:&#47;&#47;login.microsoftonline.com

- https:&#47;&#47;login.live.com

- https:&#47;&#47;go.microsoft.com

- https:&#47;&#47;graph.windows.net

- https:&#47;&#47;app.vsspsext.visualstudio.com

- &#42;.azurewebsites.net (Azure 接続の場合)

- &#42;.visualstudio.microsoft.com

- cdn.vsassets.io (コンテンツ配信ネットワーク (CDN)、コンテンツをホスト)

- &#42;.gallerycdn.vsassets.io (Azure DevOps Services の拡張機能をホスト)

- static2.sharepointonline.com (フォントなど、Visual Studio が使用する Office UI ファブリック キットのリソースをホスト)

- &#42;.nuget.org (NuGet 接続の場合)

  > [!NOTE]
  > プライベートで所有されている NuGet のサーバー URL は、このリストには含まれない場合があります。 %APPData%\Nuget\NuGet.Config で使用している NuGet のサーバーを確認できます。

## <a name="error-failed-to-parse-id-from-parent-process"></a>エラー :"親プロセスから ID を解析できませんでした"

このエラー メッセージは、ネットワーク ドライブで Visual Studio ブートストラップと response.json ファイルを使用している場合に表示されることがあります。 エラーの原因は、Windows のユーザー アカウント制御 (UAC) にあります。

このエラーが発生する理由は、次のとおりです。マップされたネットワーク ドライブまたは [UNC](/dotnet/standard/io/file-path-formats#unc-paths) 共有は、ユーザーのアクセス トークンにリンクされます。 UAC が有効な場合、2 つのユーザー [アクセス トークン](/windows/win32/secauthz/access-tokens) が作成されます。一方は管理者アクセス権 *付き* で、もう一方は管理者アクセス権 *なし* です。 ネットワーク ドライブまたは共有が作成されると、ユーザーの現在のアクセス トークンがリンクされます。 ブートストラップは、管理者として実行する必要があるため、いずれかのドライブまたは共有が管理者アクセス権付きのユーザー アクセス トークンにリンクされていない場合、ネットワーク ドライブにアクセスすることはできません。

### <a name="to-fix-this-error"></a>このエラーを修復するには

`net use` コマンドを使用するか、UAC グループ ポリシーの設定を変更することができます。 これらの回避策とその実装方法の詳細については、次の Microsoft サポート記事を参照してください。

* [Mapped drives are not available from an elevated prompt when UAC is configured to "Prompt for credentials" in Windows (UAC が Windows の [資格情報を要求する] に構成されている場合、マップされたドライブを管理者特権のプロンプトから利用できない)](https://support.microsoft.com/help/3035277/mapped-drives-are-not-available-from-an-elevated-prompt-when-uac-is-co)
* [Programs may be unable to access some network locations after you turn on User Account Control in Windows operating systems (Windows オペレーティング システムでユーザー アカウント制御を有効にした後、プログラムが一部のネットワークの場所にアクセスできない場合がある)](https://support.microsoft.com/en-us/help/937624/programs-may-be-unable-to-access-some-network-locations-after-you-turn)

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>こちらもご覧ください

* [ファイアウォールまたはプロキシ サーバーの内側に Visual Studio をインストールして使用する](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)
* [Visual Studio 管理者ガイド](visual-studio-administrator-guide.md)
* [Visual Studio のインストール](install-visual-studio.md)
