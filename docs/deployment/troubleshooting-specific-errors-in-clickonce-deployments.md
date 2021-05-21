---
title: エラーのトラブルシューティング (ClickOnce 配置)
description: この記事では、ClickOnce アプリケーションを配置するときに発生する可能性のある一般的なエラーについて説明し、各問題を解決するための手順を示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.ErrorPrompt.UncRequired
- Microsoft.VisualStudio.Publish.ClickOnceProvider.ErrorPrompt.NoInstallUrl
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications, ClickOnce
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
ms.assetid: 22dfe8f1-8271-4708-9c25-6bbb13920ac8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4697aa4869535d63c522ae25c978dd89bfe51697
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876174"
---
# <a name="troubleshoot-specific-errors-in-clickonce-deployments"></a>ClickOnce 配置の固有のエラーのトラブルシューティング
この記事では、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを配置するときに発生する可能性のある一般的なエラーの一覧を示し、各問題を解決するための手順を説明します。

## <a name="general-errors"></a>一般エラー

#### <a name="when-you-try-to-locate-an-application-file-nothing-occurs-or-xml-renders-in-internet-explorer-or-you-receive-a-run-or-save-as-dialog-box"></a>アプリケーション ファイルを検索しようとしても、Internet Explorer で何も実行されないか、XML が表示される、あるいは [実行] または [名前を付けて保存] ダイアログ ボックスが表示される
 このエラーは、サーバーまたはクライアントでコンテンツ タイプ (MIME の種類とも呼ばれます) が正しく登録されていないことが原因である可能性があります。

 まず、 *.application* 拡張子とコンテンツ タイプ "application/x-ms-application" を関連付けるように、サーバーが構成されていることを確認します。

 サーバーが正しく構成されている場合は、.NET Framework 2.0 がコンピューターにインストールされていることを確認します。 .NET Framework 2.0 がインストールされていてもこの問題が解決しない場合は、.NET Framework 2.0 をアンインストールしてから再インストールし、クライアントでコンテンツ タイプを再登録してみます。

#### <a name="error-message-says-unable-to-retrieve-application-files-missing-in-deployment-or-application-download-has-been-interrupted-check-for-network-errors-and-try-again-later"></a>次のようなエラー メッセージが表示される: "Unable to retrieve application. Files missing in deployment" (アプリケーションを取得できません。ファイルが配置にありません) または "Application download has been interrupted, check for network errors and try again later" (アプリケーションのダウンロードが中断されました。ネットワークエラーを確認し、後でもう一度お試しください)
 このメッセージは、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェストによって参照されている 1 つ以上のファイルをダウンロードできないことを示します。 このエラーをデバッグする最も簡単な方法は、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] でダウンロードできないことが示されている URL をダウンロードしてみることです。 考えられるいくつかの原因を次に示します。

- ログ ファイルに "(403) 禁止" または "(404) 見つかりません" が記録されている場合は、このファイルのダウンロードをブロックしないように Web サーバーが構成されていることを確認します。 詳細については、「[ClickOnce 配置でのサーバーおよびクライアント構成の問題](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md)」を参照してください。

- *.config* ファイルがサーバーによってブロックされている場合は、この記事の後にある「.config ファイルを含む [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールしようとしたときのダウンロード エラー」セクションを参照してください。

- 配置マニフェストの `deploymentProvider` の URL でアクティブ化に使用された URL とは異なる場所が参照されているためにこのエラーが発生したかどうかを確認します。

- すべてのファイルがサーバーに存在することを確認します。[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] のログで、見つからなかったファイルが示されているはずです。

- ネットワーク接続に問題があるかどうかを確認します。ダウンロード中にクライアント コンピューターがオフラインになった場合、このメッセージを受け取る可能性があります。

#### <a name="download-error-when-you-try-to-install-a-clickonce-application-that-has-a-config-file"></a>.config ファイルを含む ClickOnce アプリケーションをインストールしようとしたときのダウンロード エラー
 Visual Basic の Windows ベースのアプリケーションには、既定で App.config ファイルが含まれています。 Windows Server 2003 ではセキュリティ上の理由から *.config* ファイルのインストールがブロックされるため、そのオペレーティング システムを使用している Web サーバーからインストールしようとすると、問題が発生します。 *.config* ファイルをインストールできるようにするには、 **[公開オプション]** ダイアログ ボックスで **[".deploy" ファイル拡張子を使用する]** をクリックします。

 また、.application、.manifest、.deploy ファイルに対して、コンテンツ タイプ (MIME の種類とも呼ばれます) を適切に設定する必要もあります。 詳細については、お使いの Web サーバーのドキュメントを参照してください。

 詳細については、「[ClickOnce 配置でのサーバーおよびクライアント構成の問題](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md)」の「Windows Server: ロックダウンされたコンテンツ タイプ」を参照してください。

#### <a name="error-message-application-is-improperly-formatted-log-file-contains-xml-signature-is-invalid"></a>エラー メッセージ: "アプリケーションは正しくフォーマットされていません"、ログ ファイルの内容: "XML 署名が無効です"
 マニフェスト ファイルを更新し、再度署名したことを確認します。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を使用してアプリケーションを再発行するか、Mage を使用してアプリケーションに再度署名します。

#### <a name="you-updated-your-application-on-the-server-but-the-client-does-not-download-the-update"></a>サーバーでアプリケーションを更新したが、クライアントで更新プログラムがダウンロードされない
 この問題は、次のいずれかのタスクを完了することで解決できる場合があります。

- 配置マニフェストで `deploymentProvider` の URL を調べます。 `deploymentProvider` で示されているのと同じ場所にあるビットを更新していることを確認します。

- 配置マニフェストで更新間隔を確認します。 この間隔が 6 時間ごとに 1 回などの定期的な間隔に設定されている場合、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] による更新プログラムのスキャンは、この間隔が経過するまで行われません。 アプリケーションが起動するたびに更新プログラムをスキャンするよう、マニフェストを変更することができます。 更新間隔の変更は、開発時に更新プログラムがインストールされていることを確認するための便利なオプションですが、アプリケーションのアクティブ化の速度が低下します。

- [スタート] メニューでもう一度アプリケーションを起動してみてください。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] によりバックグラウンドで更新プログラムが検出されている可能性がありますが、インストールを求めるメッセージは次のアクティブ化のときに表示されます。

#### <a name="during-update-you-receive-an-error-that-has-the-following-log-entry-the-reference-in-the-deployment-does-not-match-the-identity-defined-in-the-application-manifest"></a>更新中に、次のようなログ エントリのエラーが発生する: "配置内の参照が、アプリケーション マニフェスト内で定義された ID と一致していません"
 このエラーは、配置マニフェストとアプリケーション マニフェストを手動で編集し、1 つのマニフェスト内のアセンブリの ID の説明が他のマニフェストと同期しなくなったことが原因で発生する可能性があります。 アセンブリの ID は、その名前、バージョン、カルチャ、公開キー トークンで構成されます。 マニフェストで ID の説明を調べて、相違を修正してください。

#### <a name="first-time-activation-from-local-disk-or-cd-rom-succeeds-but-subsequent-activation-from-start-menu-does-not-succeed"></a>ローカル ディスクまたは CD-ROM からの初回のアクティブ化は成功するが、その後の [スタート] メニューからのアクティブ化は成功しない
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、アプリケーションの更新プログラムを受け取るために、配置プロバイダーの URL が使用されています。 URL が示している場所が正しいことを確認します。

#### <a name="error-cannot-start-the-application"></a>エラー: "アプリケーションを起動できません"
 このエラー メッセージは、通常、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ストアへのこのアプリケーションのインストールに問題があることを示しています。 アプリケーションでエラーが発生したか、ストアが破損しています。 ログ ファイルを見ると、エラーの発生箇所がわかる場合があります。

 次のようにする必要があります。

- 配置マニフェストの ID、アプリケーション マニフェストの ID、およびメイン アプリケーションの EXE の ID がすべて、一意であることを確認します。

- ファイル パスが 100 文字を超えていないことを確認します。 アプリケーションに含まれるファイル パスが長すぎる場合は、格納できる最大パスの制限を超えている可能性があります。 パスを短くして再インストールしてみてください。

#### <a name="privatepath-settings-in-application-config-file-are-not-honored"></a>アプリケーション構成ファイルの PrivatePath の設定が適用されない
 PrivatePath (Fusion プローブ パス) を使用するには、アプリケーションで完全な信頼のアクセス許可を要求する必要があります。 完全な信頼を要求するようにアプリケーション マニフェストを変更してから、再試行してください。

#### <a name="during-uninstall-a-message-appears-saying-failed-to-uninstall-application"></a>アンインストール中に 次のようなメッセージが表示される: "アプリケーションのアンインストールに失敗しました"
 このメッセージは、通常、アプリケーションが既に削除されているか、ストアが破損していることを示します。 **[OK]** をクリックすると、 **[プログラムの追加と削除]** のエントリが削除されます。

#### <a name="during-installation-a-message-appears-that-says-that-the-platform-dependencies-are-not-installed"></a>インストールの間に、プラットフォームの依存関係がインストールされていないというメッセージが表示される
 アプリケーションの実行に必要な前提条件が、GAC (グローバル アセンブリ キャッシュ) にありません。

## <a name="publishing-with-visual-studio"></a>Visual Studio での発行

#### <a name="publishing-in-visual-studio-fails"></a>Visual Studio での発行が失敗する
 ターゲットとしているサーバーに発行する権限があることを確認します。 たとえば、管理者としてではなく、通常のユーザーとしてターミナル サーバー コンピューターにログインしている場合は、ローカル Web サーバーへの発行に必要な権限を持っていない可能性があります。

 URL を使用して発行する場合は、発行先のコンピューターで FrontPage Server Extensions が有効になっていることを確認します。

#### <a name="error-message-unable-to-create-the-web-site-site-the-components-for-communicating-with-frontpage-server-extensions-are-not-installed"></a>エラー メッセージ: Web サイト '\<site>' を作成できません。 FrontPage Server Extensions と通信するためのコンポーネントがインストールされていません。
 発行元のコンピューターに Microsoft Visual Studio Web オーサリング コンポーネントがインストールされていることを確認します。 Express ユーザーの場合、このコンポーネントは既定ではインストールされません。 詳細については、「[http://go.microsoft.com/fwlink/?LinkId=102310](https://support.microsoft.com/help/945358)」を参照してください。

#### <a name="error-message-could-not-find-file-microsoftwindowscommon-controls-version6000-culture-publickeytoken6595b64144ccf1df-processorarchitecture-typewin32"></a>エラー メッセージ: ファイル 'Microsoft.Windows.Common-Controls, Version=6.0.0.0, Culture=*, PublicKeyToken=6595b64144ccf1df, ProcessorArchitecture=\*, Type=win32' が見つかりませんでした
 このエラー メッセージは、Visual スタイルを有効にして WPF アプリケーションを発行しようとすると表示されます。 この問題を解決するには、「[方法: Visual スタイルが有効になっている WPF アプリケーションを公開する](../deployment/how-to-publish-a-wpf-application-with-visual-styles-enabled.md)」を参照してください。

## <a name="using-mage"></a>Mage の使用

#### <a name="you-tried-to-sign-with-a-certificate-in-your-certificate-store-and-a-received-blank-message-box"></a>証明書ストアの証明書を使用して署名しようとしたら、空のメッセージ ボックスを受け取った
 **[署名]** ダイアログ ボックスで、次のことを行う必要があります。

- **[Sign with a stored certificate]\(保存された証明書で署名する\)** を選択します。

- 一覧から証明書を選択します。最初の証明書は、既定では選択されていません。

#### <a name="clicking-the-dont-sign-button-causes-an-exception"></a>[Don't Sign]\(署名しない\) ボタンをクリックすると、例外が発生する
 この問題は既知のバグです。 すべての [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] マニフェストに署名する必要があります。 いずれかの署名オプションを選択し、 **[OK]** をクリックします。

## <a name="additional-errors"></a>その他のエラー
 次の表では、クライアント コンピューターのユーザーが [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションをインストールするときに受け取る可能性のある一般的なエラー メッセージを示します。 各エラー メッセージと共に、最も可能性の高いエラーの原因の説明も示します。

| エラー メッセージ | 説明 |
| - | - |
| アプリケーションを起動できません。 アプリケーションの発行元に問い合わせてください。<br /><br /> アプリケーションを起動できません。 サポートが必要な場合はアプリケーションのベンダーにお問い合わせください。 | これらは、アプリケーションを起動できず、その他の特定の理由が見つからない場合に発生する、一般的なエラー メッセージです。 多くの場合、アプリケーションが破損しているか、[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ストアが破損していることを意味します。 |
| 続行できません。 アプリケーションは正しくフォーマットされていません。 サポートが必要な場合はアプリケーションの発行元にお問い合わせください。<br /><br /> アプリケーションの検証に失敗しました。 続行できません。<br /><br /> アプリケーション ファイルを取得できません。 配置に壊れているファイルがあります。 | 配置内のいずれかのマニフェスト ファイルの構文が正しくありません。または、対応するファイルと照合できないハッシュが含まれています。 このエラーは、アセンブリ内に埋め込まれているマニフェストが破損していることを示している場合もあります。 配置を再作成してアプリケーションを再コンパイルするか、手作業によりマニフェストでエラーを見つけて修正します。 |
| アプリケーションを取得できません。 認証エラーです。<br /><br /> アプリケーションのインストールに失敗しました。 サーバー上にアプリケーション ファイルが見つかりません。 アプリケーションの発行元または管理者に問い合わせてください。 | アクセスするための権限がないため、配置内の 1 つ以上のファイルをダウンロードできません。 これは、Web サーバーから 403 禁止エラーが返されたことが原因である可能性があります。これは、配置内のいずれかのファイルが、Web サーバーによって保護されたファイルとして扱われる拡張子で終わっている場合に発生することがあります。 また、アプリケーションのファイルが含まれているディレクトリにアクセスするために、ユーザー名とパスワードが必要である可能性があります。 |
| アプリケーションをダウンロードできません。 アプリケーションに必要なファイルが不足しています。 アプリケーションのベンダーまたはシステム管理者に問い合わせてください。 | アプリケーション マニフェストに列記されている 1 つ以上のファイルがサーバーに見つかりません。 配置のすべての依存ファイルをアップロードしたことを確認してから、操作をやり直してください。 |
| アプリケーションのダウンロードに失敗しました。 ネットワーク接続を確認するか、システム管理者またはネットワーク サービス プロバイダーに問い合わせてください。 | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は、サーバーへのネットワーク接続を確立できません。 サーバーが利用可能かどうか、およびネットワークの状態を確認します。 |
| URLDownloadToCacheFile に失敗しました。HRESULT: '\<number>'。 '\<file>' をダウンロードしようとしてエラーが発生しました。 | ユーザーが配置先のコンピューターで Internet Explorer の高度なセキュリティ オプション [保護付き/保護なしのサイト間を移動する場合に警告する] を設定していて、インストールされている ClickOnce アプリケーションのセットアップ URL がセキュリティで保護されていないサイトからセキュリティで保護されているサイト (またはその逆) にリダイレクトされる場合、Internet Explorer の警告によってそれが中断されるため、インストールが失敗します。<br /><br /> このエラーを解決するには、次のいずれかのタスクを行います。<br /><br /> - セキュリティ オプションをオフにします。<br />- セキュリティ モードが変更されるような方法でセットアップ URL がリダイレクトされないようにします。<br />- リダイレクトを完全に削除し、実際のセットアップ URL をポイントします。 |
| ハード ディスクへの書き込み中にエラーが発生しました。 ディスクに十分な空き領域がない可能性があります。 アプリケーションのベンダーまたはシステム管理者に問い合わせてください。 | これは、アプリケーションを格納するためのディスク領域が不足していることを示している可能性がありますが、アプリケーション ファイルをドライブに保存しようとしているときの、より一般的な I/O エラーを示している場合もあります。 |
| アプリケーションを起動できません。 ディスクに十分な空き領域がありません。 | ハード ディスクがいっぱいです。 領域をクリアしてから、アプリケーションをもう一度実行してください。 |
| 同時に読み込みを試行している、配置されたライセンス認証の数が多すぎます。 | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] により、同時に開始できる異なるアプリケーションの数が制限されています。 これは、主に、ローカル環境の [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] サービスに対するサービス拒否攻撃を防ぐために役立ちます。同じアプリケーションを短時間に何度も起動しようとするユーザーには、アプリケーションのインスタンスが 1 つだけ提供されます。 |
| Shortcuts cannot be activated over the network. (ネットワーク経由でショートカットをアクティブ化することはできません。) | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションへのショートカットは、ローカル ハード ディスク上でのみ開始できます。 リモート サーバー上のショートカット ファイルを指す URL を開くことによって、開始することはできません。 |
| アプリケーションは大きすぎて、一部の信頼が与えられた状態でオンラインで実行することはできません。 アプリケーションのベンダーまたはシステム管理者に問い合わせてください。 | 部分信頼で実行されるアプリケーションは、オンライン アプリケーション クォータ (既定では 250 MB) の半分より大きくすることはできません。 |

## <a name="see-also"></a>こちらもご覧ください
- [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
- [ClickOnce 配置のトラブルシューティング](../deployment/troubleshooting-clickonce-deployments.md)
- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)