---
title: インストール構成をインポートまたはエクスポートする
titleSuffix: ''
description: インストール構成を .vsconfig ファイルにエクスポートし、他のユーザーと共有する方法とそれをインポートして複製する方法について説明します。
ms.date: 05/18/2019
ms.topic: how-to
f1_keywords:
- vs.about
helpviewer_keywords:
- import installation configuration
- export installation configuration
- install Visual Studio
- Visual Studio installer
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 4dcad21ce0a77e18bed0b077f731a509916e9e63
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85418822"
---
# <a name="import-or-export-installation-configurations"></a>インストール構成をインポートまたはエクスポートする

インストール構成ファイルを使用し、組織全体で Visual Studio を構成できます。 これを行うには、Visual Studio インストーラーを使用して、ワークロードとコンポーネントの情報を .vsconfig ファイルにエクスポートします。 その後、新規または既存のインストールに構成をインポートしたり、他のユーザーと共有したりすることもできます。

ここではその方法を説明します。

::: moniker range="vs-2017"

> [!NOTE]
> この機能は、Visual Studio 2017 バージョン 15.9 以降でのみ使用できます。

::: moniker-end

## <a name="export-a-configuration"></a>構成のエクスポート

以前にインストールした Visual Studio のインスタンス、または現在インストールしているインスタンスのいずれかからインストール構成ファイルをエクスポートできます。

1. Visual Studio インストーラーを開きます。

1. 製品カードで **[その他]** ボタンを選択し、 **[構成のエクスポート]** を選択します。

   ![Visual Studio インストーラーの製品カードから構成をエクスポートする](../install/media/vs-2019/vs-installer-export-config.png)

1. .vsconfig ファイルを保存する場所を参照するか入力して、 **[詳細の確認]** を選択します。

   ![Visual Studio インストーラーから構成をエクスポートする](../install/media/vs-2019/export-configuration-confirmation.png)

1. 必要なワークロードとコンポーネントがあることを確認してから、 **[エクスポート]** を選択します。

## <a name="import-a-configuration"></a>構成をインポートする

インストール構成ファイルをインポートする準備ができたら、次の手順を実行します。

1. Visual Studio インストーラーを開きます。

1. 製品カードで **[その他]** ボタンを選択し、 **[構成のインポート]** を選択します。

1. インポートする .vsconfig ファイルを見つけて、 **[詳細の確認]** を選択します。

1. 必要なワークロードとコンポーネントがあることを確認してから、 **[閉じる]** を選択します。

::: moniker range="vs-2019"

## <a name="automatically-install-missing-components"></a>不足しているコンポーネントを自動的にインストールする

**Visual Studio 2019 の新機能**:ソリューションのルート ディレクトリに .vsconfig ファイルを保存してからソリューションを開くと、不足しているコンポーネントが自動的に検出され、それらをインストールするように求められます。

![ソリューション エクスプローラーで追加のコンポーネントが提案される](../install/media/vs-2019/solution-explorer-config-file.png)

ソリューション エクスプローラーから .vsconfig ファイルを直接生成することもできます。

1. ソリューション ファイルを右クリックします。

1. **[追加]** > **[インストール構成ファイル]** を選択します。

1. .vsconfig ファイルを保存する場所を確認し、 **[詳細の確認]** を選択します。

1. 必要なワークロードとコンポーネントがあることを確認してから、 **[エクスポート]** を選択します。

::: moniker-end

> [!NOTE]
> 詳細については、「[Configure Visual Studio across your organization with .vsconfig (.vsconfig を使用して組織全体の Visual Studio を構成する)](https://devblogs.microsoft.com/setup/configure-visual-studio-across-your-organization-with-vsconfig/)」のブログ記事を参照してください。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のネットワーク インストールを作成する](create-a-network-installation-of-visual-studio.md)
* [Visual Studio のネットワーク ベース インストールを更新する](update-a-network-installation-of-visual-studio.md)
* [Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)
* [エンタープライズ展開に既定値を設定する](set-defaults-for-enterprise-deployments.md)
