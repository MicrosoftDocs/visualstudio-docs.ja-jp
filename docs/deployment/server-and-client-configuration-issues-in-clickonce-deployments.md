---
title: サーバー/クライアント構成に関する問題 (ClickOnce)
description: ClickOnce アプリケーションの配置に影響する可能性がある、サーバーとクライアントの構成に関する問題について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications, ClickOnce
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
- Windows applications, ClickOnce deployments
ms.assetid: 929e5fcc-dd56-409c-bb57-00bd9549b20b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 469749c28acdb90e835082dd05010102ab50e52b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99877617"
---
# <a name="server-and-client-configuration-issues-in-clickonce-deployments"></a>ClickOnce 配置でのサーバーおよびクライアント構成の問題
Windows Server でインターネット インフォメーション サービス (IIS) を使用していて、配置に、Microsoft Word ファイルなどの Windows では認識されない種類のファイルが含まれている場合は、IIS でそのファイルの送信が拒否されて、配置が成功しません。

 さらに、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] などの一部の Web サーバーや Web アプリケーション ソフトウェアには、ダウンロードできないファイルとファイルの種類の一覧が含まれています。 たとえば [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] では、すべての *Web.config* ファイルがダウンロードされないようになっています。 これらのファイルには、ユーザー名やパスワードなどの機密情報が含まれている場合があります。

 この制限のためにマニフェストやアセンブリなどのコア [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ファイルのダウンロードで問題が発生することはないはずですが、この制限により、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの一部として含まれているデータ ファイルのダウンロードが妨げられる場合があります。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] では、そのようなファイルのダウンロードを禁止するハンドラーを IIS 構成マネージャーから削除することで、このエラーを解決できます。 その他の詳細については、IIS サーバーのドキュメントを参照してください。

 一部の Web サーバーでは、 *.dll*、 *.config*、 *.mdf* などの拡張子を持つファイルがブロックされる場合があります。 Windows ベースのアプリケーションに含まれるファイルでは、通常、これらの拡張子のいくつかが使用されています。 ユーザーが、Web サーバー上のブロックされるファイルにアクセスする [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを実行しようとすると、エラーが発生します。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、すべてのファイル拡張子のブロックを解除するのではなく、 *.deploy* ファイル拡張子を持つすべてのアプリケーション ファイルが既定で発行されます。 そのため管理者に必要なのは、次の 3 つのファイル拡張子のブロックを解除するように Web サーバーを構成することだけです。

- *.application*

- *.manifest*

- *.deploy*

  ただし、[[発行オプション] ダイアログ ボックス](/previous-versions/visualstudio/visual-studio-2010/7z83t16a(v=vs.100))で **[".deploy" ファイル拡張子を使用する]** オプションをオフにすることで、このオプションを無効にできます。この場合は、アプリケーションで使用されているすべてのファイル拡張子のブロックを解除するように Web サーバーを構成する必要があります。

  たとえば、.NET Framework をインストールしていない IIS を使用している場合や、別の Web サーバー (Apache など) を使用している場合は、 *.manifest*、 *.application*、 *.deploy* を構成する必要があります。

## <a name="clickonce-and-secure-sockets-layer-ssl"></a>ClickOnce と Secure Sockets Layer (SSL)
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションは SSL 経由で正しく機能しますが、Internet Explorer で SSL 証明書に関するプロンプトが表示される場合は例外です。 このプロンプトは、サイト名が一致しない場合や証明書の有効期限が切れている場合など、証明書に何らかの問題がある場合に表示される可能性があります。 SSL 接続上で [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] を正常に機能させるには、証明書が最新であること、証明書のデータがサイトのデータと一致していることを確認してください。

## <a name="clickonce-and-proxy-authentication"></a>ClickOnce とプロキシ認証
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、.NET Framework 3.5 以降の Windows 統合プロキシ認証がサポートされています。 特定の machine.config ディレクティブは必要ありません。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、基本やダイジェストなど、他の認証プロトコルをサポートしていません。

 .NET Framework 2.0 に修正プログラムを適用して、この機能を有効にすることもできます。 詳細については、「[修正: プロキシサーバーを使用するように構成されているクライアントコンピューターに、.NET Framework 2.0 で作成した ClickOnce アプリケーションをインストールしようとすると、エラーメッセージ "プロキシ認証が必要です" が表示される](https://support.microsoft.com/help/917952/fix-error-message-when-you-try-to-install-a-clickonce-application-that)」を参照してください。

 詳細については、「[\<defaultProxy> 要素 (ネットワーク設定)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings)」を参照してください。

## <a name="clickonce-and-web-browser-compatibility"></a>ClickOnce と Web ブラウザーの互換性
 現在のところ、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] のインストールは、Internet Explorer を使用して配置マニフェストへの URL が開かれた場合にのみ起動されます。 Outlook Microsoft Office などの別のアプリケーションから URL が起動された配置が正常に起動されるのは、Internet Explorer が既定の Web ブラウザーとして設定されている場合のみです。

> [!NOTE]
> 展開プロバイダーが空白でない場合や、Microsoft .NET Framework Assistant 拡張機能がインストールされている場合は、Mozilla Firefox がサポートされます。 この拡張機能は、.NET Framework 3.5 SP1 と共にパッケージ化されています。 XBAP のサポートについては、必要なときに NPWPF プラグインがアクティブにされます。

## <a name="activate-clickonce-applications-through-browser-scripting"></a>ブラウザー スクリプトを通して ClickOnce アプリケーションをアクティブにする
 アクティブ スクリプティングを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを起動するカスタム Web ページを開発した場合は、一部のマシンでアプリケーションが起動しないことがあります。 Internet Explorer には、この動作に影響を及ぼす **[ファイルのダウンロード時に自動的にダイアログを表示]** という設定があります。 この動作に影響を及ぼすこの設定は、 **[オプション]** メニューの **[セキュリティ]** タブにあります。 これは **[ファイルのダウンロード時に自動的にダイアログを表示]** という名前で、 **[ダウンロード]** カテゴリの下に一覧表示されます。 このプロパティは、イントラネット Web ページに対しては既定で **[有効]** に、インターネット Web ページに対しては既定で **[無効]** に設定されています。 この設定が **[無効]** に設定されている場合は、プログラムによって (その URL を `document.location` プロパティに割り当てるなどして) [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをアクティブにしようとするとブロックされます。 こうした状況でユーザーがアプリケーションを起動できるのは、そのアプリケーションの URL に設定されているハイパーリンクをクリックするなど、ユーザーが開始するダウンロードを通してのみです。

## <a name="additional-server-configuration-issues"></a>サーバー構成に関するその他の問題

##### <a name="administrator-permissions-required"></a>管理者のアクセス許可が必要
 HTTP で発行しようとしている場合は、ターゲット サーバーに対する管理者アクセス許可が必要です。 IIS ではこのアクセス許可レベルが必要です。 HTTP を使用して発行しようとしていない場合は、ターゲット パスに対する書き込みアクセス許可のみが必要です。

##### <a name="server-authentication-issues"></a>サーバー認証に関する問題
 "匿名アクセス" がオフになっているリモート サーバーに対して発行すると、次の警告が表示されます。

```
"The files could not be downloaded from http://<remoteserver>/<myapplication>/.  The remote server returned an error: (401) Unauthorized."
```

> [!NOTE]
> 既定の資格情報以外の資格情報を要求するメッセージが表示される場合は、NTLM (NT Challenge/Response) 認証を正しく機能させることができます。そして、セキュリティ ダイアログボックスで、指定した資格情報を今後のセッション用に保存するかどうか確認するメッセージが表示されたら、 **[OK]** をクリックします。 ただし、この回避策は基本認証に対しては正しく機能しません。

## <a name="use-third-party-web-servers"></a>サードパーティの Web サーバーを使用する
 IIS 以外の Web サーバーから [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを配置しようとしている場合に、サーバーから、配置マニフェストやアプリケーション マニフェストなどの重要な [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ファイルについて正しくないコンテンツ タイプが返されると、問題が発生することがあります。 この問題を解決するには、サーバーに新しいコンテンツ タイプを追加する方法に関する Web サーバーのヘルプ ドキュメントを参照し、次の表に一覧で示したファイル名拡張子のマッピングをすべて確認してください。

|ファイル名の拡張子|Content type|
|-------------------------|------------------|
|`.application`|`application/x-ms-application`|
|`.manifest`|`application/x-ms-manifest`|
|`.deploy`|`application/octet-stream`|
|`.msu`|`application/octet-stream`|
|`.msp`|`application/octet-stream`|

## <a name="clickonce-and-mapped-drives"></a>ClickOnce とマップされたドライブ
 Visual Studio を使用して ClickOnce アプリケーションを発行する場合は、マップされたドライブをインストール場所として指定できません。 ただし、マニフェスト ジェネレーターとエディター (Mage.exe および MageUI.exe) を使用して、マップされたドライブからインストールするように ClickOnce アプリケーションを変更することができます。 詳細については、次を参照してください。 [Mage.exe (マニフェスト生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)と[MageUI.exe (マニフェスト生成および編集ツールのグラフィカル クライアント)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)します。

## <a name="ftp-protocol-not-supported-for-installing-applications"></a>FTP プロトコルはアプリケーションのインストールではサポートされない
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、任意の HTTP 1.1 Web サーバーまたはファイル サーバーからのアプリケーションのインストールをサポートしています。 FTP (ファイル転送プロトコル) は、アプリケーションのインストールではサポートされていません。 FTP は、アプリケーションの発行にのみ使用できます。 次の表に、これらの相違点を示します。

| URL の種類 | 説明 |
|----------| - |
| ftp:// | このプロトコルを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを発行できます。 |
| http:// | このプロトコルを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールできます。 |
| https:// | このプロトコルを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールできます。 |
| file:// | このプロトコルを使用して [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールできます。 |

## <a name="windows-xp-sp2-windows-firewall"></a>Windows XP SP2: Windows ファイアウォール
 Windows XP SP2 では、既定で Windows ファイアウォールが有効になっています。 Windows XP がインストールされているコンピューターでアプリケーションを開発している場合でも、IIS を実行しているローカル サーバーから [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを発行して実行することができます。 ただし、Windows ファイアウォールを開く場合を除き、別のコンピューターから IIS を実行しているサーバーにアクセスすることはできません。 Windows ファイアウォールの管理に関する手順については、Windows ヘルプを参照してください。

## <a name="windows-server-enable-frontpage-server-extensions"></a>Windows Server: FrontPage のサーバー拡張機能を有効にする
 HTTP を使用する Windows Web サーバーにアプリケーションを発行するには、Microsoft の FrontPage Server Extensions が必要です。

 FrontPage Server Extensions は、既定では Windows Server にインストールされていません。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を使用して、FrontPage Server Extensions と共に HTTP を使用する Windows Server の Web サーバーに発行する場合は、まず FrontPage Server Extensions をインストールする必要があります。 このインストールは、Windows Server の管理ツールであるサーバーの役割管理を使用して実行できます。

## <a name="windows-server-locked-down-content-types"></a>Windows Server: ロックダウンされたコンテンツ タイプ
 [!INCLUDE[WinXPSvr](../debugger/includes/winxpsvr_md.md)] 上の IIS では、一定の既知のコンテンツ タイプ ( *.htm*、 *.html*、 *.txt* など) を除くすべてのファイルの種類がロックダウンされます。 このサーバーを使用した [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの配置を有効にするには、種類が *.application*、 *.manifest* であるファイルと、アプリケーションで使用されるその他すべての種類のカスタム ファイルのダウンロードを許可するように IIS の設定を変更する必要があります。

 IIS サーバーを使用して配置する場合は、*inetmgr.exe* を実行し、既定の Web ページのために、新しいファイルの種類を追加します。

- *.application* および *.manifest* 拡張子については、MIME の種類を "application/x-ms-application" にする必要があります。 その他のファイルの種類については、MIME の種類は "application/octet-stream" にする必要があります。

- 拡張子が "\<em>" で MIME の種類が "application/octet-stream" である MIME の種類を作成すると、ブロックされていないファイルの種類のファイルをダウンロードできるようになります。 (ただし、 *\*.aspx* や *\*.asmx* などのブロックされるファイルの種類はダウンロードできません)。

  Windows Server で MIME の種類を構成する具体的な手順については、「[Web サイトまたはアプリケーションに MIME の種類を追加する方法](/iis/configuration/system.webserver/staticcontent/mimemap#how-to-add-a-mime-type-to-a-web-site-or-application)」を参照してください。

## <a name="content-type-mappings"></a>コンテンツ タイプのマッピング
 HTTP 経由で発行するときには、 *.application* ファイルのコンテンツ タイプ (MIME の種類とも呼ばれます) を "application/x-ms-application" にする必要があります。 サーバーに .NET Framework 2.0 がインストールされている場合、これは自動的に設定されます。 これがインストールされていない場合は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションの vroot (またはサーバー全体) に対する MIME の種類の関連付けを作成する必要があります。

 IIS サーバーを使用して配置する場合は、<em>inetmgr.</em>exe を実行し、 *.application* 拡張子のために "application/x-ms-application" という新しいコンテンツ タイプを追加します。

## <a name="http-compression-issues"></a>HTTP 圧縮に関する問題
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、HTTP 圧縮を使用するダウンロードを実行できます。これは、クライアントにストリームを送信する前に、GZIP アルゴリズムを使用してデータ ストリームを圧縮する Web サーバー テクノロジです。 クライアント (この場合は [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]) で、ファイルの読み取り前にストリームが展開されます。

 IIS を使用している場合は、HTTP 圧縮を簡単に有効にできます。 ただし、HTTP 圧縮を有効にすると、特定のファイルの種類 (つまり HTML ファイルとテキスト ファイル) に対してのみ有効になります。 アセンブリ ( *.dll*)、XML ( *.xml*)、配置マニフェスト ( *.application*)、アプリケーション マニフェスト ( *.manifest*) に対して圧縮を有効にするには、IIS で圧縮する種類の一覧に、これらのファイルの種類を追加する必要があります。 配置にファイルの種類を追加するまでは、テキスト ファイルと HTML ファイルのみが圧縮されます。

 IIS の詳細な手順については、「[HTTP 圧縮のために追加のドキュメントの種類を指定する方法](https://support.microsoft.com/help/234497)」を参照してください。

## <a name="see-also"></a>関連項目
- [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)
- [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)
- [アプリケーション配置の必要条件](../deployment/application-deployment-prerequisites.md)
