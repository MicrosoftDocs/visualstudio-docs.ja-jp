---
title: Visual Studio の変更
titleSuffix: ''
description: Visual Studio を変更する方法について、ステップ バイ ステップで説明します。
ms.custom: H1Hack27Feb2017,seodec18
ms.date: 07/31/2019
ms.topic: conceptual
helpviewer_keywords:
- modify Visual Studio
- change visual studio
- changing Visual Studio
- customize Visual Studio
ms.assetid: 3399ea7b-a291-4a9e-80a1-b861a21afa1d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: ad5b8a0c261ed967710480b0abd3a2b9d34f01ce
ms.sourcegitcommit: 5694c5236fa32ba7f5bc1236a853f725ec7557e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2019
ms.locfileid: "68681394"
---
# <a name="modify-visual-studio-by-adding-or-removing-workloads-and-components"></a>ワークロードやコンポーネントを追加または削除することで Visual Studio を変更する

::: moniker range="vs-2019"

必要なときに必要なものだけが含まれるように、Visual Studio を変更するのは簡単です。 これを行うには、Visual Studio インストーラー開き、ワークロードとコンポーネントを追加または削除します。

::: moniker-end

::: moniker range="vs-2017"

実行する作業に合わせて Visual Studio をより簡単にパーソナライズできるようになっただけでなく、Visual Studio をより簡単にカスタマイズできるようにもなりました。 これを行うには、新しい Visual Studio インストーラーを起動して、必要な変更を加えます。

::: moniker-end

ここではその方法を説明します。

## <a name="modify-workloads"></a>ワークロードの変更

 ワークロードには、使用するプログラミング言語またはプラットフォームに必要な機能が含まれています。 ワークロードを使用することで、必要に応じて、実行する作業に合わせ、Visual Studio を変更できます。

>[!IMPORTANT]
>Visual Studio をインストール、更新、または変更するには、管理アクセス許可を持つアカウントでログオンする必要があります。 詳細については、「[ユーザー アクセス許可と Visual Studio](../ide/user-permissions-and-visual-studio.md)」を参照してください。

>[!TIP]
> 次の手順では、インターネットに接続しているものとします。 前に作成した Visual Studio の[オフライン インストール](create-an-offline-installation-of-visual-studio.md)を変更する方法について詳しくは、「[ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)」ページをご覧ください。

::: moniker range="vs-2017"

1. コンピューター上で Visual Studio インストーラーを見つけます。

     たとえば、Windows 10 を実行しているコンピューター上で、 **[スタート]** を選択し、**Visual Studio インストーラー**としてリスト表示される **V** の文字までスクロールします。

     ![Visual Studio インストーラー](media/vs2017-locate-the-visual-studio-installer.PNG "Microsoft Visual Studio インストーラーの検索")

     >[!NOTE]
     >一部のコンピューターでは、Visual Studio インストーラーが **Microsoft Visual Studio インストーラー**として **"M"** の項に表示される場合があります。<br/><br/> Visual Studio インストーラーは `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe` にもあります。

1. インストーラーをクリックまたはタップして起動し、 **[変更]** を選択します。

     ![Visual Studio の起動または変更](media/modify-visual-studio.png "Visual Studio 2017 の変更")

     保留中の更新プログラムがある場合、[変更] ボタンは別の場所にあります。 この方法で、更新せずに Visual Studio を変更するならそれができます。 **[詳細]** をクリックして、 **[変更]** を選択します。

     ![Visual Studio の更新または変更](media/modify-or-update-visual-studio.png "Visual Studio 2017 の更新または変更")

1. **[ワークロード]** 画面で、インストールまたはアンインストールするワークロードを選択または選択解除します。

    ![Visual Studio 2017 のセットアップ ダイアログ](media/vs2017-modify-workloads.PNG "Visual Studio 2017 でのワークロードの選択")

1. もう一度 **[変更]** を選択します。

1. 新しいワークロードとコンポーネントがインストールされたら、 **[起動]** を選択します。

::: moniker-end

::: moniker range="vs-2019"

1. コンピューター上で Visual Studio インストーラーを見つけます。

     たとえば、Windows 10 を実行しているコンピューター上で、 **[スタート]** を選択し、**Visual Studio インストーラー**としてリスト表示される **V** の文字までスクロールします。

     ![Windows から Visual Studio インストーラーを開く](media/vs-2019/vs-installer-windows-start.png "Visual Studio インストーラーを開く")

     > [!NOTE]
     > また、Visual Studio インストーラーは次の場所にもあります。
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    続行する前に、インストーラーの更新が必要な場合があります。 その場合は、画面の指示に従います。

1. インストーラーで、インストールした Visual Studio のエディションを探し、 **[変更]** を選択します。

     ![Visual Studio の更新または変更](media/vs-2019/vs-installer-modify.png "Visual Studio 2019 の更新または変更")

1. **[ワークロード]** タブで、インストールまたはアンインストールするワークロードを選択または選択解除します。

    ![Visual Studio 2019 のセットアップ ダイアログ](media/vs-2019/vs-installer-modify-workloads.png "Visual Studio 2019 でのワークロードの選択")

1. 既定の **[ダウンロードしながらインストールする]** オプションをそのまま使用するか、または **[全部ダウンロードしてからインストールする]** オプションを使用するかを選択します。

    ![Visual Studio 2019 のセットアップ オプション](media/vs-2019/vs-installer-choose-install-or-download.png "ダウンロードしながらインストールするか、または最初にダウンロードしてからインストールするかを選択する")

    最初にダウンロードしてからインストールする場合は、[全部ダウンロードしてからインストールする] オプションが便利です。

1. **[変更]** を選択します。

1. 新しいワークロードとコンポーネントがインストールされたら、Visual Studio インストーラーで **[起動]** を選択します。

::: moniker-end

## <a name="modify-individual-components"></a>個々のコンポーネントの変更

ワークロードをインストールせずに Visual Studio のインストールをカスタマイズする場合は、Visual Studio インストーラーで **[個々のコンポーネント]** タブを選択し、必要なものを選択して、画面の指示に従います。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>関連項目

* [Visual Studio の更新](update-visual-studio.md)
* [Visual Studio のネットワーク ベース インストールを更新する](update-a-network-installation-of-visual-studio.md)
* [サービス ベースライン使用時の Visual Studio の更新](update-servicing-baseline.md)
* [ネットワーク ベースの Visual Studio 配置の更新プログラムを制御する](controlling-updates-to-visual-studio-deployments.md)
* [Visual Studio のアンインストール](uninstall-visual-studio.md)
