---
title: Visual Studio Tools for Unity の使用を開始する | Microsoft Docs
description: Visual Studio Tools for Unity をインストールして開発環境を設定する方法について説明します。
ms.date: 01/27/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: how-to
ms.assetid: 66b5b4eb-13b5-4071-98d2-87fafa4598a8
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
zone_pivot_groups: platform
ms.openlocfilehash: 706700c8343d934f7a9a5ce32f98bf96e67d4259
ms.sourcegitcommit: 07e6db4bf2966863093e3974c60c3b46e6953416
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2021
ms.locfileid: "112488846"
---
# <a name="get-started-with-visual-studio-and-unity"></a>Visual Studio と Unity の使用を開始する

> [!NOTE]
> このガイドでは、Unity Hub プログラムを使用して Unity が既にインストールされていることを前提としています。 Unity を初めて使用する場合は、Unity Learn にアクセスして、[Unity Essentials のラーニング パス](https://learn.unity.com/pathway/unity-essentials)を修了しておくことをお勧めします。

## <a name="install-unity-support-for-visual-studio"></a>Visual Studio 向けの Unity のサポートをインストールする

Visual Studio Tools for Unity は、C# などの記述とデバッグをサポートする無料の拡張機能です。 この拡張機能に含まれる内容の一覧については、[Tools for Unity の概要](./visual-studio-tools-for-unity.md)をご覧ください。

:::zone pivot="windows"

> [!NOTE]
> このインストール ガイドは Visual Studio を対象としています。 Visual Studio Code を使用している場合は、[VS Code を使用した Unity 開発に関するドキュメント](https://code.visualstudio.com/docs/other/unity)をご覧ください。

1. [Visual Studio インストーラーをダウンロード](/visualstudio/install/install-visual-studio.md)します。既にインストールされている場合は、それを実行します。
2. **[変更]** をクリックします (既にインストールされている場合)。または、 **[インストール]** をクリックして、目的のバージョンの Visual Studio をインストールします (新規インストール)。
3. **[ワークロード]** タブで、 **[ゲーム]** セクションまでスクロールし、 **[Unity によるゲーム開発]** ワークロードを選択します。

    ![インストーラーの [Unity によるゲーム開発] ワークロード ボックス](../media/vs/unity-workload.png)

:::zone-end
:::zone pivot="macos"

> [!NOTE]
> このインストール ガイドは Visual Studio for Mac を対象としています。 Visual Studio Code を使用している場合は、[VS Code を使用した Unity 開発に関するドキュメント](https://code.visualstudio.com/docs/other/unity)をご覧ください。

Tools for Unity は Visual Studio for Mac のインストールに含まれており、個別のインストール手順は必要ありません。 これは、 **[Visual Studio for Mac] > [拡張機能] > [ゲーム開発]** メニューで確認できます。 **[Visual Studio for Mac Tools for Unity]** が有効になっている必要があります。

![Visual Studio for Mac Tools for Unity が有効になった状態の拡張機能マネージャー ビュー](../media/vsm/unity-workload.png)

:::zone-end

## <a name="check-for-updates"></a>更新プログラムをチェックする

Visual Studio と Visual Studio for Mac を更新して、最新のバグ修正プログラム、機能、および Unity サポートを利用できるようにしておくことをお勧めします。 これには Unity バージョンの更新は必要ありません。

:::zone pivot="windows"

1. **[ヘルプ] > [更新プログラムの確認]** メニューをクリックします。

    ![Visual Studio 2019 の [更新プログラムの確認] メニュー](../media/vs/check-for-updates.png)

2. 利用可能な更新プログラムがある場合は、Visual Studio インストーラーに新しいバージョンが表示されます。 **[更新]** ボタンをクリックします。

:::zone-end
:::zone pivot="macos"

1. **[Visual Studio for Mac] > [更新プログラムの確認...]** メニューをクリックして、 **[Visual Studio の更新]** ダイアログを開きます。
2. 利用可能な更新プログラムがある場合は、 **[インストール]** ボタンをクリックします。

:::zone-end

## <a name="configure-unity-to-use-visual-studio"></a>Visual Studio を使用するように Unity を構成する

既定では、Visual Studio または Visual Studio for Mac をスクリプト エディターとして使用するように Unity を構成しておく必要があります。 Unity エディターからこれを確認したり、外部スクリプト エディターを特定のバージョンの Visual Studio に変更したりできます。

:::zone pivot="windows"

1. Unity エディターで、 **[Edit]\(編集\) > [Preferences]\(ユーザー設定\)** メニューを選択します。
2. 左側にある **[External Tools]\(外部ツール\)** タブを選択します。
3. **[External Script Editor]\(外部スクリプト エディター\)** ドロップダウン リストでは、使用する Visual Studio のバージョンを選択できます。 ドロップダウン リストから **[Browse...]\(参照...\)** をクリックして、一覧にないバージョンを追加することもできます。

    ![Windows 上の Unity エディターの [External Tools]\(外部ツール\) ユーザー設定メニュー](../media/vs/preferences-external-tools.png)

4. **[Browse...]\(参照...\)** を選択した場合は、Visual Studio インストール ディレクトリの中の **Common7/IDE** ディレクトリに移動し、**devenv.exe** を選択します。 次に、 **[Open]\(開く\)** をクリックします。
5. **[External Script Editor]\(外部スクリプト エディター\)** の一覧から Visual Studio を選択した後、 **[Editor Attaching]\(エディターのアタッチ\)** チェックボックスがオンになっていることを確認します。
6. **[Preferences]\(ユーザー設定\)** ダイアログを閉じて、構成プロセスを完了します。

:::zone-end
:::zone pivot="macos"

1. Unity エディターで、 **[Unity]\(Unity\) > [Preferences]\(ユーザー設定\)** メニューを選択します。
2. 左側にある **[External Tools]\(外部ツール\)** タブを選択します。
3. **[External Script Editor]\(外部スクリプト エディター\)** ドロップダウン リストでは、使用する Visual Studio のバージョンを選択できます。 ドロップダウン リストから **[Browse...]\(参照...\)** をクリックして、一覧にないバージョンを追加することもできます。

    ![macOS 上の Unity エディターの [External Tools]\(外部ツール\) ユーザー設定メニュー](../media/vsm/preferences-external-tools.png)

4. **[Preferences]\(ユーザー設定\)** ダイアログを閉じて、構成プロセスを完了します。

:::zone-end

## <a name="next-steps"></a>次のステップ

 Visual Studio で Unity プロジェクトを操作およびデバッグする方法については、「[Visual Studio Tools for Unity を使用する](using-visual-studio-tools-for-unity.md)」をご覧ください。
