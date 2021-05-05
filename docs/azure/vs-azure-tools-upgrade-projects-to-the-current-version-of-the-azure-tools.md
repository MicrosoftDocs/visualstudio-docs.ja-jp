---
title: 現行バージョンの Azure ツールにプロジェクトをアップグレードする
description: Visual Studio の Azure プロジェクトを現行バージョンの Azure Tools にアップグレードする方法について説明します。
author: ghogen
manager: jmartens
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/18/2016
ms.author: ghogen
ms.openlocfilehash: f9f806ad2d5e9d72d9459ba48c0d7c9525acb30e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99843775"
---
# <a name="how-to-upgrade-projects-to-the-current-version-of-the-azure-tools-for-visual-studio"></a>現行バージョンの Azure Tools for Visual Studio にプロジェクトをアップグレードする方法
## <a name="overview"></a>概要
現行 (1.6 より後の) バージョン の Azure Tools をインストールすると、バージョン 1.6 (2011 年 11 月) より前の Azure Tools を使用して作成されたプロジェクトはすべて、プロジェクトを開いた際に自動的にアップグレードされます。 バージョン 1.6 (2011 年 11 月) を使用してプロジェクトを作成し、まだそのバージョンがインストールされている場合は、バージョンの低い方でプロジェクトを開けば、アップグレードするかどうかの判断を先延ばしすることができます。

## <a name="how-your-project-changes-when-you-upgrade-it"></a>アップグレードしたときのプロジェクトの変化
プロジェクトが自動的にアップグレードされた場合、またはアップグレードすることを明示的に指定した場合、特定のアセンブリの現行バージョンで動作するようにプロジェクトに変更が加えられます。また、このセクションでも説明していますが、いくつかのプロパティも変更されます。 既にあるプロジェクトと新しいバージョンのツールとの互換性を確保するために、他の変更が必要になる場合は、それらの変更を手動で行う必要があります。

* より新しいバージョンの Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener.dll を参照するように、Web ロールの web.config ファイルと worker ロールの app.config ファイルが更新されます。
* Microsoft.WindowsAzure.StorageClient.dll、Microsoft.WindowsAzure.Diagnostics.dll、Microsoft.WindowsAzure.ServiceRuntime.dll の各アセンブリが新しいバージョンにアップグレードされます。
* Azure のプロジェクト ファイル (.ccproj) に格納された発行プロファイルは、.azurePubXml という拡張子で **Publish** サブディレクトリ内の別のファイルに移されます。
* 新機能と変更された機能をサポートするために、発行プロファイルのいくつかのプロパティが更新されます。 デプロイされたクラウド サービスを同時にまたは段階的にアップグレードできるため、**[AllowUpgrade]** は **[DeploymentReplacementMethod]** に置き換えられます。
* **UseIISExpressByDefault** プロパティが追加され、false に設定されたため、デバッグで使用する Web サーバーはインターネット インフォメーション サービス (IIS: Internet Information Services) から IIS Express に自動的に変更されません。 最近のバージョンのツールで作成したプロジェクトの Web サーバーは、既定では IIS Express になります。
* 既にあるプロジェクトのロールで Azure のキャッシュ機能がホストされている場合、プロジェクトをアップグレードするときにサービス構成 (.cscfg ファイル) とサービス定義 (.csdef ファイル) 内の一部のプロパティが変更されます。 プロジェクトで使用されている Azure のキャッシュ機能が NuGet パッケージである場合、プロジェクトは最新バージョンのパッケージにアップグレードされます。 web.config ファイルを開き、クライアントの構成がアップグレード処理後も適切に維持されていることを確認する必要があります。 NuGet パッケージを使用せずに、クライアント アセンブリへの参照として Azure のキャッシュ機能を追加した場合は、アセンブリが更新されません。アセンブリへの参照を新しいバージョンに手動で更新する必要があります。

> [!IMPORTANT]
> F# プロジェクトでは、Azure アセンブリへの参照を手動で更新して、これらのアセンブリの新しいバージョンを参照する必要があります。
>
>

### <a name="how-to-upgrade-an-azure-project-to-the-current-release"></a>Azure プロジェクトを現行リリースにアップグレードする方法
1. アップグレード後のプロジェクトに使用する Visual Studio 環境に、新しいバージョンの Azure Tools をインストールして、アップグレード対象のプロジェクトを開きます。 プロジェクトが 1.6 (2011 年 11 月) リリース未満の Azure Tools で作成されている場合、プロジェクトは新しいバージョンに自動的にアップグレードされます。 2011 年 11 月リリースでプロジェクトが作成され、そのバージョンがまだインストールされている場合、プロジェクトはそのバージョンで開きます。
2. [ソリューション エクスプ ローラー] で、プロジェクト ノードのショートカット メニューを開き、**[プロパティ]** を選択し、表示されるダイアログ ボックスの **[アプリケーション]** タブを選択します。

    **[アプリケーション]** タブに、プロジェクトに関連付けられたツールのバージョンが表示されます。 新しいバージョンの Azure Tools が表示された場合、そのプロジェクトは既にアップグレードされています。 タブに表示されたバージョンよりも新しいツールをインストールしている場合は、**[アップグレード]** が表示されます。
3. **[アップグレード]** ボタンをクリックして、プロジェクトを現在のバージョンのツールにアップグレードします。
4. プロジェクトをビルドし、API の変更に起因するエラーがあれば解決してください。 新しいバージョンのコードを変更する方法については、特定の API に関するドキュメントを参照してください。
