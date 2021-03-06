---
title: フォルダーに発行する
description: Visual Studio for Mac を使用してフォルダーに Web アプリを発行する方法。
ms.date: 11/09/2020
helpviewer_keywords:
- deployment, website, console, publish
ms.assetid: e963fb4b-6d32-4d45-86bb-ef7e4d3028b0
author: sayedihashimi
ms.author: sayedha
manager: unniravindranathan
ms.prod: visual-studio-mac
ms.topic: how-to
ms.openlocfilehash: 99127416b6a488cd7e795b3c4a1888ff103c8029
ms.sourcegitcommit: f9ed9c4c6c166ef9826feb21dcb9c4d47ed14e1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2021
ms.locfileid: "102607393"
---
# <a name="publish-to-a-folder-using-visual-studio-for-mac"></a>Visual Studio for Mac を使用してフォルダーに発行する

発行ツールを使用することで、フォルダーに .NET Core コンソールまたは ASP.NET Core アプリを発行することができます。

## <a name="prerequisites"></a>必須コンポーネント

- .NET Core を有効にしてインストールされた [Visual Studio 2019 for Mac](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs4mac2019)。
- .NET Core コンソール、または ASP.NET Core プロジェクト。 プロジェクトをまだ用意していない場合は、[新しいプロジェクトを作成](./create-new-projects.md)することができます。

## <a name="publish-to-folder"></a>フォルダーに発行する

Visual Studio for Mac では、発行ツールを使用して、フォルダーに .NET Core プロジェクトを発行することができます。 フォルダーに発行したら、ファイルを別の環境に転送することができます。 フォルダーに発行するには、次の手順を行います。

 1. [ソリューション] ウィンドウで、プロジェクトを右クリックして、 **[発行]** を選択します。

    ![[発行] コンテキスト メニュー](media/publish-context-menu.png)

 2. このプロジェクトが既に発行されている場合は、メニューに発行プロファイルが表示されます。 その発行プロファイルを選択して、発行プロセスを開始します。

 3. このプロジェクトをフォルダーに初めて発行する場合は、 **[Publish to Folder]\(フォルダーに発行する\)** を選択します。

    ![[Publish to Folder]\(フォルダーに発行する\) コンテキスト メニュー](media/publish-to-folder-context-menu.png)

 4. **[Publish to Folder]\(フォルダーに発行する\)** ダイアログが表示されます。 このダイアログでは、プロジェクトの発行先のフォルダーをカスタマイズできます。 **[参照]** ボタンを使用してこれを行うことも、パスに貼り付けることもできます。

 5. **[発行]** をクリックすると、いくつかのことが行われます。 まず、発行プロファイルが作成されます。 発行プロファイルは、発行プロセス中にプロジェクトにインポートされる MSBuild ファイルです。 これには、発行プロセス中に使用されるプロパティが含まれています。 これらのファイルは、`Properties/PublishProfiles` に格納され、拡張子 `.pubxml` が付けられます。 次に、発行プロセスが開始されます。 Visual Studio for Mac のステータス バーを注視することで、進行状況を監視できます。

    ![発行状態が表示されている IDE ステータス バー](media/publish-to-folder-status-bar.png)

 6. 発行が正常に完了すると、発行フォルダーに対して Finder ウィンドウが開きます。 発行プロファイルが作成されたので、[発行] コンテキスト メニューにそれが表示されるようになります。

    ![フォルダー プロファイルを含む [発行] コンテキスト メニュー](media/publish-context-menu-with-folder-profile.png)

 7. 同じ設定を使用してプロジェクトを再び発行するには、[発行] コンテキスト メニューでそのプロファイルをクリックしてください。

## <a name="customize-publish-options"></a>発行オプションのカスタマイズ

発行プロファイル ([発行] コンテキスト メニューに表示される) の名前を変更するには、発行プロファイル ファイルの名前を変更します。 ファイルの拡張子 (`.pubxml`) は決して変更しないでください。

発行フォルダーのパスを変更するには、発行プロファイルを開き、`publishUrl` 値を編集します。

使用されるビルド構成を変更するには、発行プロファイル内の `LastUsedBuildConfiguration` プロパティを変更します。

## <a name="see-also"></a>関連項目
 - [dotnet publish](https://docs.microsoft.com/dotnet/core/tools/dotnet-publish)
 - [Visual Studio を使用して Web サイトに Web アプリを発行する](https://docs.microsoft.com/visualstudio/deployment/quickstart-deploy-to-a-web-site?view=vs-2019)