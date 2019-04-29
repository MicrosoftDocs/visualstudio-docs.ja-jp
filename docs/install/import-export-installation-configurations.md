---
title: インストール構成をインポートまたはエクスポートする
titleSuffix: ''
description: Visual Studio の構成のインポート/エクスポート機能を使用する方法について説明します
ms.date: 04/19/2019
ms.topic: conceptual
f1_keywords:
- vs.about
helpviewer_keywords:
- import installation configuration
- export installation configuration
- install Visual Studio
- Visual Studio installer
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: facbbf5903d683ea3a13bdd875dfe2b6c63b6367
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786406"
---
# <a name="import-or-export-installation-configurations"></a>インストール構成をインポートまたはエクスポートする

インストール構成ファイルを使用して、組織全体で Visual Studio を構成できます。 これを行うには、Visual Studio インストーラーを使用して、ワークロードとコンポーネントの情報を .vsconfig ファイルにエクスポートします。 それから、新規または既存のインストールに構成をインポートできます。

ここではその方法を説明します。

::: moniker range="vs-2017"

> [!NOTE]
> この機能は、Visual Studio 2017 バージョン 15.9 以降でのみ使用できます。

::: moniker-end

## <a name="export-a-configuration"></a>構成のエクスポート

以前にインストールした Visual Studio のインスタンス、または現在インストールしているインスタンスのいずれかからインストール構成ファイルをエクスポートできます。

1. Visual Studio インストーラーを開きます。

1. 製品カードで **[その他]** ボタンを選択し、**[構成のエクスポート]** を選択します。

   ![Visual Studio インストーラーの製品カードから構成をエクスポートする](../install/media/vs-2019/vs-installer-export-config.png)

1. .vconfig ファイルを保存する場所を参照するか入力して、**[詳細の確認]** を選択します。

   ![Visual Studio インストーラーから構成をエクスポートする](../install/media/vs-2019/export-configuration-confirmation.png)

1. 必要なワークロードとコンポーネントがあることを確認してから、**[エクスポート]** を選択します。

## <a name="import-a-configuration"></a>構成をインポートする

インストール構成ファイルをインポートする準備ができたら、次の手順を実行します。

1. Visual Studio インストーラーを開きます。

1. 製品カードで **[その他]** ボタンを選択し、**[構成のインポート]** を選択します。

1. インポートする .vconfig ファイルを見つけて、**[詳細の確認]** を選択します。

1. 必要なワークロードとコンポーネントがあることを確認してから、**[閉じる]** を選択します。

::: moniker range="vs-2019"

## <a name="automatically-install-missing-components"></a>不足しているコンポーネントを自動的にインストールする

**Visual Studio 2019 の新機能**:ソリューションのルート ディレクトリに .vsconfig ファイルを保存してからソリューションを開くと、不足しているコンポーネントが自動的に検出され、それらをインストールするように求められます。

![ソリューション エクスプローラーで追加のコンポーネントが提案される](../install/media/vs-2019/solution-explorer-config-file.png)

ソリューション エクスプローラーから .vsconfig ファイルを直接生成することもできます。

1. ソリューション ファイルを右クリックします。

1. **[追加]**>**[インストール構成ファイル]** を選択します。

1. .vsconfig ファイルを保存する場所を確認し、**[詳細の確認]** を選択します。

1. 必要なワークロードとコンポーネントがあることを確認してから、**[エクスポート]** を選択します。

::: moniker-end

> [!NOTE]
> 詳細については、「[Configure Visual Studio across your organization with .vsconfig (.vsconfig を使用して組織全体の Visual Studio を構成する)](https://devblogs.microsoft.com/setup/configure-visual-studio-across-your-organization-with-vsconfig/)」のブログ記事を参照してください。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio のネットワーク インストールを作成する](create-a-network-installation-of-visual-studio.md)
* [Visual Studio のネットワーク ベース インストールを更新する](update-a-network-installation-of-visual-studio.md)
* [Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)
* [エンタープライズ展開に既定値を設定する](set-defaults-for-enterprise-deployments.md)
