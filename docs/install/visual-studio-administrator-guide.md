---
title: Visual Studio 管理者ガイド
titleSuffix: ''
description: エンタープライズ環境で Visual Studio を展開する方法について説明します。
ms.date: 04/06/2021
ms.custom: seodec18
ms.topic: overview
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
ms.assetid: 4af353f5-6cfd-4ebe-bcfb-f42306e451a0
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: ba41c545c2af2e0490ef0410fde7849706123940
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306710"
---
# <a name="visual-studio-administrator-guide"></a>Visual Studio 管理者ガイド

エンタープライズ環境では、システム管理者は一般的に、ネットワーク共有またはシステム管理ソフトウェアを使用してエンドユーザーにインストールを展開します。 エンタープライズ展開をサポートするために、Visual Studio セットアップ エンジンを設計しました。このエンジンにより、システム管理者はネットワーク インストールの場所を作成し、インストールの既定値を事前に構成したり、インストール プロセス中にプロダクト キーを展開したり、ロールアウトが成功した後に製品の更新プログラムを管理したりできます。

この管理者ガイドでは、ネットワーク環境でエンタープライズ展開を行うためのシナリオ ベースのガイダンスを示します。

## <a name="before-you-begin"></a>始める前に

組織全体に Visual Studio を展開する前に、いくつかの意思決定を行い、作業を完了する必要があります。

::: moniker range=">=vs-2019"

* 各ターゲット コンピューターで[最小インストール要件](/visualstudio/releases/2019/system-requirements/)が満たされていることを確認します。

::: moniker-end

::: moniker range="vs-2017"

* 各ターゲット コンピューターで[最小インストール要件](/visualstudio/productinfo/vs2017-system-requirements-vs/)が満たされていることを確認します。

::: moniker-end

* サービス ニーズについて決定します。

  会社がある機能セットを長く使用する必要があるが、定期的なサービス更新を取得する場合、サービス ベースラインの使用を計画します。 詳細については、「[Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing#support-options-for-enterprise-and-professional-customers)」ページの「***Enterprise および Professional のお客様向けのサポート オプショ***」セクション、および「[サービス ベースライン使用時の Visual Studio の更新](update-servicing-baseline.md)」ページをご覧ください。

* 更新モデルについて決定します。

  個々のクライアント コンピューターにはどこから製品更新プログラムを取得させますか。 具体的には、クライアントに更新プログラムをインターネットから取得させるか、全社的なローカル共有から取得させるかを決定します。 次に、ローカル共有を使用する場合、個々のユーザーが自分のクライアントを更新できるのか、管理者にプログラムでクライアントを更新してもらうのかを決定します。 クライアント コンピューターで元のインストールが行われる前にこうした決定が行われていることが望まれます。 詳細については、「[Visual Studio のネットワーク ベース インストールを作成する](../install/create-a-network-installation-of-visual-studio.md)」をご覧ください。

  ネットワーク インストール レイアウトを Visual Studio の最新の更新プログラムのインストール ポイントとして使用できるように、また、クライアント ワークステーションに既に配置されているインストールを保持するために、最新の製品の更新プログラムを使って Visual Studio のネットワーク インストール レイアウトを更新できます。 詳細については、「[Visual Studio のネットワーク ベース インストールを更新する](../install/update-a-network-installation-of-visual-studio.md)」をご覧ください。

  エンタープライズ展開ツールを利用する組織は、Visual Studio 更新プログラムは Microsoft Update カタログと Windows Server Update Services で入手できるという事実を最大限に活用できます。 詳細については、[管理者向け更新を有効にする](../install/enabling-administrator-updates.md)と[管理者の更新を適用する](../install/applying-administrator-updates.md)方法に関するページを参照してください。

  インターネットに接続されていないコンピューターの場合、オフラインの Visual Studio インスタンスを更新する最も簡単かつ迅速な方法は、最小限のレイアウトを作成することです。 詳細については、「[最小限のオフライン レイアウトを使用して Visual Studio を更新する](update-minimal-layout.md)」をご覧ください。

::: moniker range=">=vs-2019"

* 会社に必要な[ワークロードとコンポーネント](workload-and-component-ids.md?view=vs-2019&preserve-view=true)を決定します。

* (スクリプト ファイルの詳細管理を簡単にする) [応答ファイル](automated-installation-with-response-file.md?view=vs-2019&preserve-view=true)を使用するかどうかを決定します。

::: moniker-end

::: moniker range="vs-2017"

* 会社に必要な[ワークロードとコンポーネント](workload-and-component-ids.md?view=vs-2017&preserve-view=true)を決定します。

* (スクリプト ファイルの詳細管理を簡単にする) [応答ファイル](automated-installation-with-response-file.md?view=vs-2017&preserve-view=true)を使用するかどうかを決定します。

::: moniker-end

* グループ ポリシーを有効にするかどうかと、個々のコンピューターで顧客フィードバックを無効にするように Visual Studio を構成するかどうかを決定します。

::: moniker range=">=vs-2019"

## <a name="step-1---download-visual-studio-product-files"></a>手順 1 - Visual Studio 製品ファイルをダウンロードする

* インストールする[ワークロードとコンポーネントを選択します](workload-and-component-ids.md?view=vs-2019&preserve-view=true)。

* [Visual Studio 製品ファイルのネットワーク共有を作成します](create-a-network-installation-of-visual-studio.md?view=vs-2019&preserve-view=true)。

## <a name="step-2---build-an-installation-script"></a>手順 2 - インストール スクリプトを作成する

* インストールを制御するために[コマンド ライン パラメーター](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019&preserve-view=true)を使用するインストール スクリプトを作成します。

  >[!NOTE]
  > [応答ファイル](automated-installation-with-response-file.md?view=vs-2019&preserve-view=true)を使用することでスクリプトを簡素化できます。 既定のインストール オプションを含む応答ファイルを必ず作成してください。

* (任意) インストール スクリプトの一部として[ボリューム ライセンスのプロダクト キーを適用](automatically-apply-product-keys-when-deploying-visual-studio.md?view=vs-2019&preserve-view=true)し、ユーザーがソフトウェアを個別にアクティブにする必要がないようにします。

* (任意) ネットワーク レイアウトを更新し、[エンドユーザーに製品の更新プログラムを配信するタイミングと場所を制御](controlling-updates-to-visual-studio-deployments.md?view=vs-2019&preserve-view=true)します。

* (任意) 他のバージョンまたはインスタンスと共有されている一部のパッケージがインストールされている場所、[パッケージがキャッシュされる場所](set-defaults-for-enterprise-deployments.md?view=vs-2019&preserve-view=true)、[パッケージがキャッシュされるかどうか](disable-or-move-the-package-cache.md?view=vs-2019&preserve-view=true)など、Visual Studio の展開に影響を与えるレジストリ ポリシーを設定します。

* (任意) グループ ポリシーを設定します。 個々のコンピューターで[顧客フィードバックを無効にするように Visual Studio を構成する](../ide/visual-studio-experience-improvement-program.md)こともできます。

## <a name="step-3---deploy-updates"></a>手順 3 - 更新プログラムの展開

任意の配置テクノロジを使用し、スクリプトをターゲットの開発者ワークステーションで実行します。

* 手順 1 で使用したコマンドを定期的に実行して更新されたコンポーネントを追加し、Visual Studio の[最新の更新プログラムを適用してネットワークの場所を更新](update-a-network-installation-of-visual-studio.md?view=vs-2019&preserve-view=true)します。

  更新スクリプトを使用して Visual Studio を更新できます。 それを行うには、[`update`](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019&preserve-view=true) コマンドライン パラメーターを使用します。

  System Center Configuration Manager のようなツールを使用し、Windows Server Update Services または Microsoft Update カタログから Visual Studio 更新プログラムを展開できます。  詳細については、[管理者の更新を適用する](applying-administrator-updates.md)方法に関するページを参照してください。 

## <a name="step-4---optional-use-visual-studio-tools-to-verify-installation"></a>手順 4 - (省略可能) Visual Studio ツールを使用し、インストールの有効性を検証する

クライアント コンピューターに[インストールされている Visual Studio インスタンスを検出して管理する](tools-for-managing-visual-studio-instances.md?view=vs-2019&preserve-view=true)ために役立つ複数のツールが用意されています。

## <a name="advanced-configuration"></a>詳細な構成

既定では、Visual Studio をインストールすると、エラー リスト F1 やコード リンクの Bing 検索でカスタムの型を含めることができます。 ポリシーによって次のレジストリ キーの値を変更することで、検索メカニズムでユーザーが定義したカスタムの型を含められないように Visual Studio を構成できます。

**“PutCustomTypeInBingSearch” DWORD 0**

レジストリは、プライベート レジストリ ハイブの *Software\Microsoft\VisualStudio\16.0_{InstanceId}\Roslyn\Internal\Diagnostics\* にあります。 レジストリ ハイブを開く方法については、「[Visual Studio インスタンスのレジストリの編集](tools-for-managing-visual-studio-instances.md?view=vs-2019&preserve-view=true#editing-the-registry-for-a-visual-studio-instance)」を参照してください。

::: moniker-end

::: moniker range="vs-2017"

## <a name="step-1---download-visual-studio-product-files"></a>手順 1 - Visual Studio 製品ファイルをダウンロードする

* インストールする[ワークロードとコンポーネントを選択します](workload-and-component-ids.md?view=vs-2017&preserve-view=true)。

* [Visual Studio 製品ファイルのネットワーク共有を作成します](create-a-network-installation-of-visual-studio.md?view=vs-2017&preserve-view=true)。

## <a name="step-2---build-an-installation-script"></a>手順 2 - インストール スクリプトを作成する

* インストールを制御するために[コマンド ライン パラメーター](use-command-line-parameters-to-install-visual-studio.md?view=vs-2017&preserve-view=true)を使用するインストール スクリプトを作成します。

  >[!NOTE]
  > [応答ファイル](automated-installation-with-response-file.md?view=vs-2017&preserve-view=true)を使用することでスクリプトを簡素化できます。 既定のインストール オプションを含む応答ファイルを必ず作成してください。

* (任意) インストール スクリプトの一部として[ボリューム ライセンスのプロダクト キーを適用](automatically-apply-product-keys-when-deploying-visual-studio.md?view=vs-2017&preserve-view=true)し、ユーザーがソフトウェアを個別にアクティブにする必要がないようにします。

* (任意) ネットワーク レイアウトを更新し、[エンドユーザーに製品の更新プログラムを配信するタイミングと場所を制御](controlling-updates-to-visual-studio-deployments.md?view=vs-2017&preserve-view=true)します。

* (任意) 他のバージョンまたはインスタンスと共有されている一部のパッケージがインストールされている場所、[パッケージがキャッシュされる場所](set-defaults-for-enterprise-deployments.md?view=vs-2019&preserve-view=true)、[パッケージがキャッシュされるかどうか](disable-or-move-the-package-cache.md?view=vs-2017&preserve-view=true)など、Visual Studio の展開に影響を与えるレジストリ ポリシーを設定します。

* (任意) グループ ポリシーを設定します。 個々のコンピューターで[顧客フィードバックを無効にするように Visual Studio を構成する](../ide/visual-studio-experience-improvement-program.md)こともできます。

## <a name="step-3---deploy-updates"></a>手順 3 - 更新プログラムの展開

任意の配置テクノロジを使用し、スクリプトをターゲットの開発者ワークステーションで実行します。

* 手順 1 で使用したコマンドを定期的に実行して更新されたコンポーネントを追加し、Visual Studio の[最新の更新プログラムを適用してネットワークの場所を更新](update-a-network-installation-of-visual-studio.md?view=vs-2017&preserve-view=true)します。

  更新スクリプトを使用して Visual Studio を更新できます。 それを行うには、[`update`](use-command-line-parameters-to-install-visual-studio.md?view=vs-2019&preserve-view=true) コマンドライン パラメーターを使用します。

  System Center Configuration Manager のようなツールを使用し、Windows Server Update Services または Microsoft Update カタログから Visual Studio 更新プログラムを展開できます。 詳細については、[管理者向け更新プログラムを適用する](applying-administrator-updates.md)方法に関するページを参照してください。

## <a name="step-4---optional-use-visual-studio-tools-to-verify-installation"></a>手順 4 - (省略可能) Visual Studio ツールを使用し、インストールの有効性を検証する

クライアント コンピューターに[インストールされている Visual Studio インスタンスを検出して管理する](tools-for-managing-visual-studio-instances.md?view=vs-2017&preserve-view=true)ために役立つ複数のツールが用意されています。

## <a name="advanced-configuration"></a>詳細な構成

既定では、Visual Studio をインストールすると、エラー リスト F1 やコード リンクの Bing 検索でカスタムの型を含めることができます。 ポリシーによって次のレジストリ キーの値を変更することで、検索メカニズムでユーザーが定義したカスタムの型を含められないように Visual Studio を構成できます。

**“PutCustomTypeInBingSearch” DWORD 0**

レジストリは、プライベート レジストリ ハイブの `Software\Microsoft\VisualStudio\15.0_{InstanceId}\Roslyn\Internal\Diagnostics\` ディレクトリにあります。 レジストリ ハイブを開く方法については、「[Visual Studio インスタンスのレジストリの編集](tools-for-managing-visual-studio-instances.md?view=vs-2017&preserve-view=true#editing-the-registry-for-a-visual-studio-instance)」を参照してください。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [管理者の更新を有効にする](enabling-administrator-updates.md)
* [管理者の更新を適用する](applying-administrator-updates.md)
* [コマンド ライン パラメーターの例](command-line-parameter-examples.md)
* [Visual Studio オフライン インストールに必要な証明書をインストールする](install-certificates-for-visual-studio-offline.md)
* [インストール構成をインポートまたはエクスポートする](import-export-installation-configurations.md)
* [Visual Studio セットアップ アーカイブ](https://devblogs.microsoft.com/setup/tag/vs2017/)
* [Visual Studio の製品ライフサイクルとサービス](/visualstudio/releases/2019/servicing/)
* [同期自動読み込みの設定](../extensibility/synchronously-autoloaded-extensions.md)
