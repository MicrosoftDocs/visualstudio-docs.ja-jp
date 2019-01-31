---
title: テスト エージェントとテスト コントローラーのインストール
ms.date: 10/24/2018
ms.prod: visual-studio-dev15
ms.topic: conceptual
helpviewer_keywords:
- configure test agents, test lab
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e5c0a9078cdbe9ad84b53cd7f667dbd9e3c83d2b
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "54970488"
---
# <a name="install-test-agents-and-test-controllers"></a>テスト エージェントとテスト コントローラーのインストール

Visual Studio と Azure Test Plans または Team Foundation Server (TFS) を使用するテスト シナリオでは、テスト コントローラーは必要ありません。 Agents for Visual Studio は、Azure Test Plans または TFS と通信してオーケストレーションを処理します。 Azure Test Plans または TFS のビルド ワークフローおよびリリース ワークフローのために継続的なテストを実行するシナリオが考えられます。

また、ラボ管理ではなく[ビルドまたはリリース管理](use-build-or-rm-instead-of-lab-management.md)を使用する方がよいかどうかを検討する場合もあります。

## <a name="system-requirements"></a>システム要件

次の表では、Visual Studio 2017 のテスト エージェントまたはテスト コントローラーをインストールするためのシステム要件を示します。

| アイテム | 要件 |
| ---- | ------------ |
| **エージェント** | Windows 10<br />Windows 8、Windows 8.1<br />Windows 7 Service Pack 1<br />Windows Server 2016: Standard および Datacenter<br />Windows Server 2012 R2 |
| **コントローラー** | Windows 10<br />Windows 8、Windows 8.1<br />Windows 7 Service Pack 1<br />Windows Server 2016: Standard および Datacenter<br />Windows Server 2012 R2 |
| **.NET Framework** | .NET Framework 4.5 |

## <a name="install-the-test-controller-and-test-agents"></a>テスト コントローラーとテスト エージェントのインストール

Agents for Visual Studio 2017 は [visualstudio.microsoft.com](https://visualstudio.microsoft.com/downloads/?q=agents) からダウンロードできます。 *Agents for Visual Studio 2017* を探し、*[エージェント]* または *[コントローラー]* を選択して、*[ダウンロード]* を選択します。 ダウンロードした実行可能ファイルを実行し、テスト エージェントまたはテスト コントローラーをインストールします。

Visual Studio 2015 および Visual Studio 2013 用のエージェントは、[以前のバージョンのダウンロード](https://visualstudio.microsoft.com/vs/older-downloads/) ページからダウンロードできます。

ISO ファイル形式のインストーラーを入手できるので、仮想マシンに簡単にインストールできます。

## <a name="compatible-versions-of-tfs-microsoft-test-manager-the-test-controller-and-test-agent"></a>TFS、Microsoft Test Manager、テスト コントローラー、テスト エージェントの互換性のあるバージョン

次の表に従って、異なるバージョンの TFS、Microsoft Test Manager、テスト コントローラー、およびテスト エージェントを混在させることができます。

| TFS | Microsoft Test Manager (ラボ センターを使用する場合) | コントローラー | エージェント |
| --- | -------------------------------------- | ---------- | ----- |
| 2017: 2015 からのアップグレードまたは新規インストール | 2017 | 2017 | 2017 |
| 2017: 2015 からのアップグレードまたは新規インストール | 2017 | 2013 Update 5 | 2013 Update 5 |
| 2017: 2015 からのアップグレードまたは新規インストール | 2015 | 2013 Update 5 | 2013 Update 5 |
| 2015: 2013 からのアップグレード | 2013 | 2013 |2013 |
| 2015: 新規インストール | 2013 | 2013 | 2013 |
| 2015: 2013 からのアップグレードまたは新規インストール | 2015 | 2013 | 2013 |
| 2013 | 2015 | 2013 | 2013 |

> [!NOTE]
> TFS 2018 および Azure DevOps Services でのラボ管理シナリオは非推奨となっています。 詳細については、「[TFS 2018 のリリース ノート](/visualstudio/releasenotes/tfs2018-relnotes#--removing-support-for-lab-center-and-automated-testing-flows-in-microsoft-test-manager)」を参照してください。

## <a name="upgrade-from-visual-studio-2013-test-agents"></a>Visual Studio 2013 テスト エージェントからのアップグレード

すべての新しい自動テストシナリオでは Agents for Visual Studio を使用することをお勧めします。 ビルド パイプラインで*テスト エージェントの配置*タスクを使用して、コンピューター上にテスト エージェントをダウンロードしてインストールすることができます。

次の表は、Agents for Visual Studio 2013 でサポートされるシナリオと、Team Foundation Server (TFS) 2015 および Azure Test Plans での代替シナリオを示しています。

| Agents for Visual Studio 2013 でサポートされるシナリオ | TFS および Azure Test Plans での代替シナリオ |
| - | - |
| Visual Studio でのビルド-配置-テスト ワークフロー | ユーザーは、TFS でのビルド、配置、およびテスト シナリオで[ビルド パイプライン](/azure/devops/pipelines/index?view=vsts) (XAML ビルドではない) を使用できます。 |
| オンプレミス リモート コンピューターを使用するロード テスト (パフォーマンス テスト) | Test Controller と Test Agents 2013 Update 5 を使用して、オンプレミスでロード テストを実行します。 |
| ラボ環境を使用する Microsoft Test Manager からの自動テストのリモート実行 | 現在、このシナリオに代わるものはありません。 ビルドおよびリリース定義 (XAML ビルドではない) で機能テストの実行タスクを使用して、テストをリモートで実行することをお勧めします。 |
| 開発者による Visual Studio でのリモート テストの実行 | サポート対象から除外されました。 |
