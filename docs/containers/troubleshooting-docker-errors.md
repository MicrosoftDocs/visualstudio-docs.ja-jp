---
title: Windows での Docker クライアント エラーのトラブルシューティング | Microsoft Docs
description: Visual Studio を使用して、Windows 上で Web アプリを作成し、Docker にデプロイする際に発生する問題のトラブルシューティングを行います。
ms.technology: vs-azure
author: ghogen
manager: jmartens
ms.custom: seodec18
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.devlang: dotnet
ms.topic: troubleshooting
ms.workload: multiple
ms.date: 01/27/2020
ms.author: ghogen
ms.openlocfilehash: 5f48b5c06e91b9c05e6edc7e2a1738aeb677a7ba
ms.sourcegitcommit: 69456d802203d21dabc3ae8662547a3241c24f47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2021
ms.locfileid: "110235912"
---
# <a name="troubleshoot-visual-studio-development-with-docker"></a>Docker を使用した Visual Studio 開発のトラブルシューティング

Visual Studio コンテナー ツールを使用する際、アプリケーションのビルドまたはデバッグしている間に問題が発生する可能性があります。 一般的なトラブルシューティング手順のいくつかを以下に示します。

## <a name="volume-sharing-is-not-enabled-enable-volume-sharing-in-the-docker-ce-for-windows-settings--linux-containers-only"></a>ボリューム共有が有効にならない。 Docker CE for Windows の設定でのボリューム共有の有効化 (Linux コンテナーのみ)

ファイル共有を管理する必要があるのは、Docker で Hyper-V を使用している場合だけです。 WSL 2 を使用している場合、次の手順は必要ありません。また、[ファイル共有] オプションは表示されません。 この問題を解決するには、次の操作を行います。

1. 通知領域で **[Windows 用の Docker]** を右クリックし、 **[設定]** を選択します。
1. **[リソース]**  >  **[ファイル共有]** を選択し、アクセスする必要があるフォルダーを共有します。 システム ドライブ全体を共有することは可能ですが、お勧めできません。

    :::image type="content" source="media//troubleshooting-docker-errors/docker-settings-image.png" alt-text="共有ドライブ":::

> [!TIP]
> Visual Studio 2017 バージョン 15.6 以降の Visual Studio バージョンでは、**共有ドライブ** が構成されていない場合、プロンプトが表示されます。

## <a name="unable-to-start-debugging"></a>デバッグを開始できない

理由の 1 つとして、ユーザー プロファイル フォルダーに古いデバッグ コンポーネントが残っていることが考えられます。 次のコマンドを実行してこれらのフォルダーを削除し、次回のデバッグ セッションで最新のデバッグ コンポーネントがダウンロードされるようにしてください。

- del %userprofile%\vsdbg
- del %userprofile%\onecoremsvsmon

## <a name="errors-specific-to-networking-when-debugging-your-application"></a>アプリケーションのデバッグ時のネットワークに固有のエラー

[コンテナー ホスト ネットワークのクリーンアップ](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/master/windows-server-container-tools/CleanupContainerHostNetworking)に関するページでダウンロードできるスクリプトを実行してみてください。このスクリプトにより、ホスト コンピューター上のネットワーク関連のコンポーネントが更新されます。

## <a name="mounts-denied"></a>マウントが拒否される

MacOS 用の Docker を使用している場合、フォルダー /usr/local/share/dotnet/sdk/NuGetFallbackFolder を参照するとエラーが発生する可能性があります。 Docker で [File Sharing]\(ファイル共有\) タブにフォルダーを追加します。

## <a name="docker-users-group"></a>Docker users グループ

コンテナーを使用するときに、Visual Studio で次のエラーが発生する場合があります。

```
The current user must be in the 'docker-users' group to use Docker Desktop. 
Add yourself to the 'docker-users' group and then log out of Windows.
```

Docker コンテナーを使用する許可を得るには、'docker-users' グループのメンバーである必要があります。  Windows 10 で自分自身をグループに追加するには、次の手順を行います。

1. スタート メニューから、 **[コンピューターの管理]** を開きます。
1. **[ローカル ユーザーとグループ]** を展開し、 **[グループ]** を選択します。
1. **docker-users** グループを検索し、 **[グループに追加]** を右クリックして選択します。
1. お使いのユーザー アカウントまたはアカウントを追加します。
1. いったんサインアウトしてからもう一度サインインして、変更した内容を有効にします。

また、管理者の `net localgroup` コマンド プロンプトでコマンドを使用して、ユーザーを特定のグループに追加することもできます。

```cmd
net localgroup docker-users DOMAIN\username /add
```

PowerShell では、[Add-LocalGroupMember](/powershell/module/microsoft.powershell.localaccounts/add-localgroupmember) 関数を使用します。

## <a name="low-disk-space"></a>ディスク領域不足

Docker では既定で、 *%ProgramData%/Docker/* フォルダーにイメージが格納されます。このフォルダーは通常、システム ドライブ上にあり、*C:\ProgramData\Docker\* となります。 システム ドライブの大切な領域をイメージで占有してしまわないよう、イメージ フォルダーの場所を変更できます。 そのためには次を行います。

 1. タスク バーの Docker アイコンを右クリックし、 **[設定]** を選択します。
 1. **[Docker エンジン]** を選択します。 
 1. 編集ウィンドウで `graph` プロパティ設定を追加し、Docker イメージに任意の場所を指定します。

```json
    "graph": "D:\\mypath\\images"
```

:::image type="content" source="media/troubleshooting-docker-errors/docker-daemon-settings.png" alt-text="Docker ファイル共有のスクリーンショット":::

**[適用および再起動]** をクリックします。 以上の手順で *%ProgramData%\docker\config\daemon.json* にある設定ファイルが変更されます。 以前に作成したイメージが移動されることはありません。

## <a name="container-type-mismatch"></a>コンテナーの種類の不一致

プロジェクトに Docker サポートを追加する場合は、Windows または Linux のいずれかのコンテナーを選択します。 Docker サーバー ホストがプロジェクト ターゲットと同じコンテナーの種類を実行するように構成されていない場合は、次のようなエラーが表示される可能性があります。

:::image type="content" source="media/troubleshooting-docker-errors/docker-host-config-change-linux-to-windows.png" alt-text="Docker ホストとプロジェクトの不一致のスクリーンショット":::

この問題を解決するには、次の手順を実行します。

- システム トレイの Docker for Windows アイコンを右クリックし、 **[Switch to Windows containers...]\(Windows コンテナーに切り替える...\)** または **[Switch to Linux containers...]\(Linux コンテナーに切り替える...\)** を選択します。

## <a name="microsoftdockertools-github-repo"></a>Microsoft/DockerTools GitHub リポジトリ

その他の問題が発生した場合は、[Microsoft/DockerTools](https://github.com/microsoft/dockertools/issues) の問題に関するページをご覧ください。

## <a name="see-also"></a>関連項目

- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)
