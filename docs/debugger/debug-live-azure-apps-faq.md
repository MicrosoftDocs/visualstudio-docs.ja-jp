---
title: スナップショットのデバッグに関する FAQ | Microsoft Docs
description: Visual Studio でスナップショット デバッガーを使用してライブ Azure アプリケーションをデバッグするときに発生する問題についてよく寄せられる質問 (FAQ) を一覧にまとめています。
ms.custom: SEO-VS-2020
ms.date: 11/07/2017
ms.topic: reference
helpviewer_keywords:
- debugger
ms.assetid: 944f1eb0-a74b-4d28-ae2b-a370cd869add
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5276127f0d6755b9fdabdfa965b5c1b8c4d94823
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2020
ms.locfileid: "97727204"
---
# <a name="frequently-asked-questions-for-snapshot-debugging-in-visual-studio"></a>Visual Studio でのスナップショットのデバッグについてよく寄せられる質問

スナップショット デバッガーを使用してライブ Azure アプリケーションをデバッグするときに考えられる質問の一覧を以下に示します。

#### <a name="what-is-the-performance-cost-of-taking-a-snapshot"></a>スナップショットの取得にはどのようなパフォーマンス コストがかかりますか?

スナップショット デバッガーがアプリのスナップショットをキャプチャすると、アプリのプロセスはフォークされ、フォークされたコピーは中断されます。 スナップショットをデバッグする場合、デバッグ対象はプロセスのフォークされたコピーです。 このプロセスにかかる時間はわずか 10 から 20 ミリ秒ですが、アプリのヒープ全体はコピーされません。 代わりに、ページ テーブルのみがコピーされ、書き込み時にコピーするページが設定されます。 ヒープ上のアプリのオブジェクトの一部が変更された場合は、それぞれのページがコピーされます。 各スナップショットのメモリ内コストが小さい理由はこのためです (ほとんどのアプリケーションでは数百キロバイト程度)。

#### <a name="what-happens-if-i-have-a-scaled-out-azure-app-service-multiple-instances-of-my-app"></a>スケールアウトされた Azure App Service (アプリの複数のインスタンス) があるとどうなりますか?

アプリのインスタンスが複数ある場合、スナップポイントはすべてのインスタンスに適用されます。 指定した条件で最初にヒットしたスナップポイントでのみ、スナップショットが作成されます。 複数のスナップポイントがある場合、後のスナップショットは最初のスナップショットを作成したものと同じインスタンスから取得されます。 出力ウィンドウに送信されたログポイントには、1 つのインスタンスのメッセージのみが表示されますが、アプリケーション ログに送信されたログポイントではすべてのインスタンスからメッセージが送信されます。

#### <a name="how-does-the-snapshot-debugger-load-symbols"></a>スナップショット デバッガーがシンボルを読み込む方法を教えてください。

スナップショット デバッガーを使用するには、ローカルのアプリケーションまたは Azure App Service にデプロイされているアプリケーションに一致するシンボルが必要です (埋め込みの PDB は現在サポートされていません)。スナップショット デバッガーでは、Azure App Service からシンボルが自動的にダウンロードされます。 Visual Studio 2017 バージョン 15.2 以降、Azure App Service にデプロイすると、アプリのシンボルもデプロイされます。

#### <a name="does-the-snapshot-debugger-work-against-release-builds-of-my-application"></a>スナップショット デバッガーはアプリケーションのリリース ビルドに対して動作しますか?

はい。スナップショット デバッガーはリリース ビルドに対して動作するように設計されています。 スナップポイントが関数に配置されると、その関数はデバッグ バージョンに再コンパイルされ、デバッグ可能になります。 スナップショット デバッガーを停止すると、関数はリリース ビルドのバージョンに戻ります。

#### <a name="can-logpoints-cause-side-effects-in-my-production-application"></a>ログポイントが運用アプリケーションに副作用を及ぼす可能性はありますか?

いいえ。アプリに追加したログ メッセージは仮想的に評価されます。 アプリケーションに副作用を引き起こすことはありません。 ただし、ログポイントでは一部のネイティブ プロパティにアクセスできない場合があります。

#### <a name="does-the-snapshot-debugger-work-if-my-server-is-under-load"></a>サーバーに負荷がかかっていてもスナップショット デバッガーは機能しますか?

はい。スナップショットのデバッグは、サーバーに負荷がかかっていても機能します。 サーバーの空きメモリが少ない状況になると、スナップショット デバッガーが調整され、スナップショットがキャプチャされなくなります。

#### <a name="how-do-i-uninstall-the-snapshot-debugger"></a>スナップショット デバッガーをアンインストールする方法を教えてください。

App Service からスナップショット デバッガー サイト拡張機能をアンインストールするには、次の手順を実行します。

1. Visual Studio の Cloud Explorer または Azure portal のいずれかを使用して App Service を無効にします。
1. App Service の Kudu サイト (つまり yourappservice.**scm**.azurewebsites.net) にアクセスし、 **[サイト拡張機能]** に移動します。
1. スナップショット デバッガー サイト拡張機能の [X] をクリックして削除します。

#### <a name="why-are-ports-opened-during-a-snapshot-debugger-session"></a>スナップショット デバッガー セッション中にポートが開かれるのはなぜですか?

Azure で取得されたスナップショットをデバッグするために、スナップショット デバッガーでは一連のポートを開く必要があります。これらは、リモート デバッグに必要なポートと同じです。 [ポートの一覧については、こちらを参照してください](../debugger/remote-debugger-port-assignments.md)。

#### <a name="how-do-i-disable-the-remote-debugger-extension"></a>リモート デバッガー拡張機能を無効にするにはどうすればよいですか。

App Services の場合:
1. App Service の Azure portal を使用してリモート デバッガー拡張機能を無効にします。
2. Azure portal > アプリケーション サービス リソース ブレード > *[アプリケーション設定]*
3. *[デバッグ]* セクションに移動し、 *[リモート デバッグ]* の *[オフ]* ボタンをクリックします。

AKS の場合:
1. [Docker イメージ上の Visual Studio スナップショット デバッガー](https://github.com/Microsoft/vssnapshotdebugger-docker)に対応するセクションを削除するように Dockerfile を更新します。
2. 変更した Docker イメージをリビルドして再配置します。

仮想マシンまたは仮想マシン スケール セットの場合、リモート デバッガー拡張機能、証明書、KeyVault、および InBound NAT プールを次のように削除します。

1. リモート デバッガー拡張機能を削除します

   仮想マシンおよび仮想マシン スケール セットのリモート デバッガーを無効にする方法はいくつかあります。

      - Cloud Explorer を使用してリモート デバッガーを無効にします

         - Cloud Explorer > 仮想マシン リソース > [デバッグを無効にする] (Cloud Explorer の仮想マシン スケール セットには、[デバッグを無効にする] は存在しません)。

      - PowerShell スクリプトまたはコマンドレットを使用してリモート デバッガーを無効にします

         仮想マシンの場合:

         ```powershell
         Remove-AzVMExtension -ResourceGroupName $rgName -VMName $vmName -Name Microsoft.VisualStudio.Azure.RemoteDebug.VSRemoteDebugger
         ```

         仮想マシン スケール セットの場合:

         ```powershell
         $vmss = Get-AzVmss -ResourceGroupName $rgName -VMScaleSetName $vmssName
         $extension = $vmss.VirtualMachineProfile.ExtensionProfile.Extensions | Where {$_.Name.StartsWith('VsDebuggerService')} | Select -ExpandProperty Name
         Remove-AzVmssExtension -VirtualMachineScaleSet $vmss -Name $extension
         ```

      - Azure portal を使用してリモート デバッガーを無効にします
         - Azure portal > 仮想マシンまたは仮想マシン スケール セットのリソース ブレード > [拡張機能]
         - Microsoft.VisualStudio.Azure.RemoteDebug.VSRemoteDebugger 拡張機能をアンインストールします

         > [!NOTE]
         > 仮想マシン スケール セット - ポータルでは、DebuggerListener ポートを削除できません。 Azure PowerShell を使用する必要があります。 詳細については、以下を参照してください。

2. 証明書と Azure KeyVault を削除します

   仮想マシンまたは仮想マシン スケール セット用にリモート デバッガー拡張機能をインストールすると、クライアントとサーバーの両方の証明書が作成され、Azure 仮想マシンおよび仮想マシン スケール セットのリソースに対して Visual Studio クライアントが認証されます。

   - クライアント証明書

      この証明書は、Cert:/CurrentUser/My/ にある自己署名証明書です

      ```
      Thumbprint                                Subject
      ----------                                -------

      1234123412341234123412341234123412341234  CN=ResourceName
      ```

      この証明書をマシンから削除する方法の 1 つは、PowerShell を使用することです

      ```powershell
      $ResourceName = 'ResourceName' # from above
      Get-ChildItem -Path Cert:\CurrentUser\My | Where-Object {$_.Subject -match $ResourceName} | Remove-Item
      ```

   - サーバー証明書
      - 対応するサーバー証明書の拇印は、Azure KeyVault のシークレットとしてデプロイされています。 Visual Studio では、仮想マシンまたは仮想マシン スケール セット リソースに対応するリージョン内で、MSVSAZ* というプレフィックスが付いた KeyVault の検索または作成が試みられます。 そのため、そのリージョンにデプロイされたすべての仮想マシンまたは仮想マシン スケール セットのリソースでは、同じ KeyVault が共有されます。
      - サーバー証明書の拇印のシークレットを削除するには、Azure portal に移動し、リソースをホストしているリージョンと同じリージョン内で MSVSAZ* KeyVault を見つけます。 おそらく `remotedebugcert<<ResourceName>>` というラベルが付けられているシークレットを削除します
      - また、PowerShell を使用してリソースからサーバー シークレットを削除する必要があります。

      仮想マシンの場合:

      ```powershell
      $vm.OSProfile.Secrets[0].VaultCertificates.Clear()
      Update-AzVM -ResourceGroupName $rgName -VM $vm
      ```

      仮想マシン スケール セットの場合:

      ```powershell
      $vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Clear()
      Update-AzVmss -ResourceGroupName $rgName -VMScaleSetName $vmssName -VirtualMachineScaleSet $vmss
      ```

3. すべての DebuggerListener InBound NAT プールを削除します (仮想マシン スケール セットのみ)

   リモート デバッガーによって、スケール セットのロード バランサーに適用される DebuggerListener in-bound NAT プールが導入されます。

   ```powershell
   $inboundNatPools = $vmss.VirtualMachineProfile.NetworkProfile.NetworkInterfaceConfigurations.IpConfigurations.LoadBalancerInboundNatPools
   $inboundNatPools.RemoveAll({ param($pool) $pool.Id.Contains('inboundNatPools/DebuggerListenerNatPool-') }) | Out-Null

   if ($LoadBalancerName)
   {
      $lb = Get-AzLoadBalancer -ResourceGroupName $ResourceGroup -name $LoadBalancerName
      $lb.FrontendIpConfigurations[0].InboundNatPools.RemoveAll({ param($pool) $pool.Id.Contains('inboundNatPools/DebuggerListenerNatPool-') }) | Out-Null
      Set-AzLoadBalancer -LoadBalancer $lb
   }
   ```

#### <a name="how-do-i-disable-snapshot-debugger"></a>スナップショット デバッガーを無効にするにはどうすればよいですか。

App Service の場合:
1. App Service の Azure portal でスナップショット デバッガーを無効にします。
2. Azure portal > アプリケーション サービス リソース ブレード > *[アプリケーション設定]*
3. Azure portal で次のアプリ設定を削除し、変更を保存します。
   - INSTRUMENTATIONENGINE_EXTENSION_VERSION
   - SNAPSHOTDEBUGGER_EXTENSION_VERSION

   > [!WARNING]
   > [アプリケーション設定] を変更すると、アプリの再起動が開始されます。 [アプリケーション設定] の詳細については、「[Azure portal で App Service アプリを構成する](/azure/app-service/web-sites-configure)」を参照してください。

AKS の場合:
1. [Docker イメージ上の Visual Studio スナップショット デバッガー](https://github.com/Microsoft/vssnapshotdebugger-docker)に対応するセクションを削除するように Dockerfile を更新します。
2. 変更した Docker イメージをリビルドして再配置します。

仮想マシンまたは仮想マシン スケール セットの場合:

スナップショット デバッガーを無効にするには、いくつかの方法があります。
- Cloud Explorer > 仮想マシンまたは仮想マシン スケール セット リソース > [診断を無効にする]

- Azure portal > 仮想マシンまたは仮想マシン スケール セットのリソース ブレード > [拡張機能] > Microsoft.Insights.VMDiagnosticsSettings 拡張機能のアンインストール

- [Az PowerShell](/powershell/azure/overview) の PowerShell コマンドレット

   仮想マシン:

   ```powershell
      Remove-AzVMExtension -ResourceGroupName $rgName -VMName $vmName -Name Microsoft.Insights.VMDiagnosticsSettings
   ```

   仮想マシン スケール セット:

   ```powershell
      $vmss = Get-AzVmss -ResourceGroupName $rgName -VMScaleSetName $vmssName
      Remove-AzVmssExtension -VirtualMachineScaleSet $vmss -Name Microsoft.Insights.VMDiagnosticsSettings
   ```

## <a name="see-also"></a>関連項目

- [Visual Studio でのデバッグ](../debugger/index.yml)
- [スナップショット デバッガーを使用してライブ ASP.NET アプリをデバッグする](../debugger/debug-live-azure-applications.md)
- [スナップショット デバッガーを使用して、Azure Virtual Machines と Azure Virtual Machine Scale Sets 上のライブ ASP.NET アプリをデバッグする](../debugger/debug-live-azure-virtual-machines.md)
- [スナップショット デバッガーを使用してライブ ASP.NET Azure Kubernetes をデバッグする](../debugger/debug-live-azure-kubernetes.md)
- [スナップショットのデバッグに関するトラブルシューティングと既知の問題](../debugger/debug-live-azure-apps-troubleshooting.md)
