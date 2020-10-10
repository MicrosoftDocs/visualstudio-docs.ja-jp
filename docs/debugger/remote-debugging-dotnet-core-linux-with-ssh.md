---
title: Linux で .NET Core をリモート デバッグする | Microsoft Docs
ms.date: 02/26/2020
ms.topic: conceptual
helpviewer_keywords:
- remote debugging, linux
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 23bc0fa990a79b1855ec382f42248a0f847c3c9c
ms.sourcegitcommit: 3d64bfb9bf85395357effe054db9a9afaa0be5ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/29/2020
ms.locfileid: "78200867"
---
# <a name="remote-debug-net-core-on-linux-using-ssh"></a>SSH を使用して Linux で .NET Core をリモート デバッグする

Visual Studio 2017 以降では、Linux で実行されている .NET Core プロセスに SSH 経由でアタッチできます。 この記事では、デバッグのセットアップ方法とデバッグ方法について説明します。

## <a name="prerequisites"></a>必須コンポーネント

Visual Studio コンピューターでは、**ASP.NET と Web 開発**ワークロードまたは **.NET Core クロスプラットフォーム開発**ワークロードのいずれかをインストールする必要があります。

Linux サーバーでは、SSH サーバーをインストールする必要があります。curl または wget で解凍してインストールします。 たとえば、Ubuntu では、以下を実行して行うことができます。

``` cmd
sudo apt-get install openssh-server unzip curl
```

## <a name="build-and-deploy-the-application"></a>アプリケーションをビルドしてデプロイする

デバッグ用にアプリケーションを準備するには:

- アプリケーションをビルドするときに、デバッグ構成の使用を検討します。 デバッグ コンパイルされたコードより、リテール コンパイルされたコード (リリース構成) をデバッグする方が非常に困難です。 リリース構成を使用する必要がある場合は、まず [マイ コードのみ] を無効にします。 この設定を無効にするには、 **[ツール]**  >  **[オプション]**  >  **[デバッグ]** の順に選択し、 **[マイ コードのみを有効にする]** をオフにします。

- [ポータブル PDB](https://github.com/OmniSharp/omnisharp-vscode/wiki/Portable-PDBs) (既定の設定) を生成するようにプロジェクトが構成されていることを確認し、PBD が DLL と同じ場所にあることを確認します。 Visual Studio でこれを構成するには、プロジェクトを右クリックし、 **[プロパティ]**  >  **[ビルド]**  >  **[詳細]**  >  **[デバッグ情報]** を選択します。

デバッグする前に、いくつかの方法を使用してアプリを配置できます。 たとえば、次のように操作できます。

- ソースをターゲット コンピューターにコピーし、Linux コンピューター上で ```dotnet build``` を使用してビルドします。

- Windows でアプリをビルドし、ビルド成果物を Linux コンピューターに転送します。 (ビルド成果物は、アプリケーション自体、依存する可能性のあるランタイム ライブラリ、および *.deps.json* ファイルで構成されます)。

## <a name="attach-the-debugger"></a>デバッガーをアタッチします。

コンピューターの構成が完了したら、Linux コンピューターでアプリケーションを開始しすると、デバッガーをアタッチする状態になります。

1. Visual Studio で、 **[デバッグ]**  >  **[プロセスにアタッチ]** と選択します。

1. **[接続の種類]** の一覧で、 **[SSH]** を選択します。

1. **[接続ターゲット]** を、ターゲット コンピュータの IP アドレスまたはホスト名に変更します。

1. デバッグするプロセスを見つけます。

   コードは、一意のプロセス名または dotnet という名前のプロセスで実行されます。 対象のプロセスを見つけるには、 **[タイトル]** 列を確認します。この列には、プロセスのコマンド ライン引数が表示されます。

   次の例では、SSH トランスポート経由のリモート Linux マシンからのプロセスの一覧が、 **[プロセスにアタッチ]** ダイアログ ボックスに表示されています。

   ![Linux プロセスにアタッチする](media/remote-debug-linux-over-ssh-attach.png)

1. **[アタッチ]** をクリックします。

1. 表示されるダイアログ ボックスで、デバッグするコードの種類を選択します。 **[マネージド (Unix 用 .NET Core)]** を選択します。

1. Visual Studio のデバッグ機能を使用して、アプリをデバッグします。

   次の例では、リモート Linux マシンで実行されているコード内のブレークポイントで Visual Studio デバッガーが停止していることがわかります。

   ![ブレークポイントに到達する](media/remote-debug-linux-over-ssh-hit-breakpoint.png)
