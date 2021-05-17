---
description: アプリケーションの MSI パッケージは、多くの場合、Visual Studio Installer Projects 拡張機能を使用して作成されます。
title: Visual Studio Installer Projects と .NET Core 3.1
titleSuffix: ''
ms.date: 08/18/2020
ms.topic: conceptual
helpviewer_keywords:
- installer projects
- installer projects, .NETCore
author: MSLukeWest
ms.author: lukewest
manager: MSLukeWest
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 5a78c1cf4f7b1562408e0a3fb598075f2c114fc0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102171241"
---
# <a name="visual-studio-installer-projects-extension-and-net-core-31"></a>Visual Studio Installer Projects 拡張機能 と .NET Core 3.1

アプリケーションの MSI パッケージは、多くの場合、Visual Studio Installer Projects 拡張機能を使用して作成されます。

この拡張機能はこちらでダウンロードできます。[Visual Studio Installer Projects](https://marketplace.visualstudio.com/items?itemName=VisualStudioClient.MicrosoftVisualStudio2017InstallerProjects)

## <a name="update-for-net-core"></a>.NET Core の更新
.NET Core には、2 つの異なる発行モデルがあります。

- フレームワーク依存の展開

- 自己完結型アプリケーションにランタイムを含める。

これらの展開戦略の詳細については、「[.NET Core アプリケーションの発行の概要](/dotnet/core/deploying/)」を参照してください。

### <a name="workflow-changes-for-net-core-31"></a>.NET Core 3.1 のワークフローの変更

1. .NET Core 3.1 プロジェクトの正しい出力を取得するには、 **[プライマリ出力]** ではなく **[Publish Items]\(発行項目\)** を選択します。  このダイアログを表示するには、プロジェクトのコンテキスト メニューから **[追加]**  >  **[プロジェクト出力]** の順に選択します。

    ![[プロジェクト出力グループの追加] ダイアログの [Publish Items]\(発行項目\) 出力グループ](../deployment/media/installer-projects-net-core-publish-items-output.png "発行項目を選択する")

2. 自己完結型のインストーラーを作成するには、適切なプロパティが設定された発行プロファイルの相対パスを使用して、セットアップ プロジェクトの **[Publish Items]\(発行項目\)** ノードの **[PublishProfilePath]** プロパティを設定します。

    ![[Publish Items]\(発行項目\) プロジェクト出力アイテムでの発行プロファイルの設定](../deployment/media/installer-projects-net-core-publish-profile.png "発行プロファイルを設定する")

### <a name="prerequisites-for-net-core-31"></a>.NET Core 3.1 の前提条件

フレームワークに依存する .NET Core 3.1 アプリに必要なランタイムをインストーラーでインストールできるようにする場合は、[前提条件](../deployment/application-deployment-prerequisites.md)を使用してこれを実現できます。  インストーラー プロジェクトの [プロパティ] ダイアログボックスで、 **[前提条件]** ダイアログを開くと、次のエントリが表示されます。

![[前提条件] ダイアログの .NET Core 項目](../deployment/media/installer-projects-net-core-prerequisites.png ".NET Core の前提条件")

コンソール アプリケーションの場合は、 **[.NET Core ランタイム...]** オプションを選択する必要があります。WPF/WinForms アプリケーションの場合は、 **[.NET デスクトップ ランタイム...]** を選択する必要があります。

>[!NOTE]
>これらの項目は、Visual Studio 2019 Update 7 リリース以降で提供されています。

## <a name="see-also"></a>関連項目

- [[必須コンポーネント] ダイアログ ボックス](../ide/reference/prerequisites-dialog-box.md)
- [アプリケーション配置の必要条件](../deployment/application-deployment-prerequisites.md)
