---
title: Visual Studio での Python チュートリアル、手順 0、インストール
titleSuffix: ''
description: Visual Studio で Python を使用するための中核となるチュートリアルの手順 0 (インストールの前提条件)。
ms.date: 01/28/2019
ms.topic: tutorial
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: vs-acquisition
ms.workload:
- python
- data-science
ms.openlocfilehash: ee6454a3414b8b586dc596ea25ff76066009df50
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390686"
---
# <a name="install-python-support-in-visual-studio"></a>Visual Studio での Python サポートのインストール

> [!Note]
> 現在、Python のサポートは Visual Studio for Windows でのみ使用できます。Mac と Linux では、[Visual Studio Code](https://code.visualstudio.com/docs/python/python-tutorial) を利用して Python のサポートを使うことができます。

1. Windows 用の最新の Visual Studio インストーラーをダウンロードして実行します (Python のサポートがあるのは、リリース 15.2 以降です)。 Visual Studio が既にインストールされている場合は、Visual Studio インストーラーを実行し、手順 2 へ進みます。

    > [!div class="nextstepaction"]
    > [Visual Studio Community をインストールする](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=15&rid=34347&utm_source=docs&utm_medium=clickbutton&utm_campaign=python_gettingstarted)

    >[!Tip]
    > このコミュニティ版は、個人の開発者、クラス学習、学術研究、オープン ソース開発向けです。 その他の用途には、[Visual Studio Professional](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Professional&rel=15&rid=34347&utm_source=docs&utm_medium=clickbutton&utm_campaign=python_gettingstarted) または [Visual Studio Enterprise](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Enterprise&rel=15&rid=34347&utm_source=docs&utm_medium=clickbutton&utm_campaign=python_gettingstarted) を使用してください。

1. インストーラーによって、ワークロード一覧が表示されます。これは、特定の開発分野の関連オプションのグループです。 Python の場合、**[Python 開発]** ワークロードを選択し、**[インストール]** を選択します。

    ![Visual Studio インストーラーの [Python 開発] ワークロード](media/installation-python-workload.png)

1. Python のサポートをすばやくテストするには、Visual Studio を起動し、**Alt**+**I** キーを押して **Python Interactive** ウィンドウを開き、`2+2` を入力します。 **4** という出力が表示されない場合は、手順を再確認してください。

    ![対話型ウィンドウでの Python のテスト](media/installation-interactive-test.png)

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [手順 1: Python プロジェクトの作成](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

## <a name="see-also"></a>参照

- [既存の Python インタープリターを手動で識別する](managing-python-environments-in-visual-studio.md#manually-identify-an-existing-environment)
- [Visual Studio 2015 以前の Python サポートをインストールする](installing-python-support-in-visual-studio.md)
- [インストールする場所](installing-python-support-in-visual-studio.md#install-locations)
