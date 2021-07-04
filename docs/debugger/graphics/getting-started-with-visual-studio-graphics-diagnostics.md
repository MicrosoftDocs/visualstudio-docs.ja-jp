---
title: グラフィックス診断の使用を開始する | Microsoft Docs
description: グラフィックス診断を初めて使用するための準備をしてから、Direct3D アプリケーションのフレームをキャプチャして Graphics Analyzer でそれらを診断します。
ms.custom: SEO-VS-2020
ms.date: 06/08/2020
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 70512b4df3be7f11973af244c336b22c59c90f8f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387607"
---
# <a name="getting-started-with-visual-studio-graphics-diagnostics"></a>Visual Studio グラフィックス診断の使用を開始する
このセクションでは、まずグラフィックス診断を初めて使用するための準備をしてから、Direct3D アプリケーションのフレームをキャプチャして Graphics Analyzer でそれらを確認します。

## <a name="requirements"></a>必要条件
 Visual Studio でグラフィックス診断を使用するには、Visual Studio Enterprise、Visual Studio Professional、または Visual Studio Community を使用する必要があります。  Visual Studio Code を含むその他のエディションには、この機能は含まれていません。

 [!INCLUDE[downloadvs](../includes/downloadvs_md.md)]

### <a name="windows-10-prerequisites"></a>Windows の 10 の前提条件
 Windows のオプション機能の "*グラフィック ツール*" は Windows 10 でのグラフィックス診断に必要なキャプチャと再生のインフラストラクチャを提供します。

 グラフィック ツールをインストールする方法の詳細については、「[Windows 10 のグラフィック ツールをインストールする](#InstallGraphicsTools)」を参照してください。

## <a name="install-graphics-tools-for-windows-10"></a><a name="InstallGraphicsTools"></a> Windows 10 用のグラフィック ツールをインストールする
 Windows 10 では、グラフィックス診断のインフラストラクチャが、"*グラフィック ツール*" と呼ばれる Windows のオプション機能によって提供されます。 この機能は、キャプチャするアプリが以前のバージョンの Windows を対象にしているかどうか、またはどのバージョンの Direct3D を使用しているかに関係なく、Windows 10 でグラフィックス情報をキャプチャおよび再生するために必要です。 グラフィック ツール機能を事前にインストールすることができます。それ以外の場合は、Visual Studio からグラフィックス診断セッションを最初に開始するときに、オンデマンドでインストールされます。

#### <a name="to-install-graphics-tools-for-windows-10"></a>Windows 10 用のグラフィック ツールをインストールするには

1. [検索] に「**アプリと機能**」と入力し、 **[アプリと機能]** の設定を開きます。

2. **[アプリと機能]** の設定の右側にある **[オプション機能]** を選択します ( **[アプリと機能]** の下)。

   **[オプション機能]** の設定が表示されます。

3. **[オプション機能]** の設定で、 **[機能の追加]** を選択します。 インストールできるオプション機能の一覧が表示されます。

4. 機能の一覧から **[グラフィック ツール]** を選択して、 **[インストール]** を選択します。

   グラフィック ツールの機能は Windows 10 SDK をインストールするときにも、自動的にインストールされます。

> [!TIP]
> Windows 10 のオプションのグラフィック ツール機能は、コマンド ライン キャプチャ プログラム **dxcap.exe** など、軽量のキャプチャおよび再生機能を提供しており、開発者用ツールがインストールされていないコンピューターでサポート、テスト、および診断を行うシナリオで利用できます。 詳細については、「[コマンド ライン キャプチャ ツール](command-line-capture-tool.md)」のトピックを参照してください。

## <a name="using-graphics-diagnostics-for-the-first-time"></a>グラフィックス診断を初めて使用する
 これで、必要なものがすべて揃い、グラフィックス診断の使用を開始する準備が整いました。 以下の手順に実行します。

### <a name="1---create-a-direct3d-app"></a>1 -、Direct3D アプリを作成する

独自の Direct3D アプリが既にある場合は、グラフィックス診断を試すことができます。 それ以外の場合は、次のいずれかを使用します。

::: moniker range=">=vs-2019"
「[Direct3D ゲーム サンプル](/samples/microsoft/windows-universal-samples/simple3dgamedx/)」からサンプルをダウンロードします。
::: moniker-end
::: moniker range="vs-2017"
- Windows 10 用の **DirectX 11 アプリ (ユニバーサル Windows)** または **DirectX 12 アプリ (ユニバーサル Windows)** プロジェクト テンプレート。
- Windows 10 用の [Direct3D 12 UAP サンプル](https://code.msdn.microsoft.com/Direct3D-12-UAP-Sample-ecb1779f)。
::: moniker-end

先に進む前に、アプリをビルドして実行できることを確認します。 **[ビルド]**  >  **[ソリューションのビルド]** を選択して、エラーなしでビルドできることを確認します。 次に、 **[デバッグ]**  >  **[デバッグなしで開始]** (**Ctrl + F5** キー) を選択して、正しく実行されることを確認します。 ツールでテストするマシンによっては、サンプルのプラットフォームとデバッグ ターゲットを調整する必要があります。 たとえば、Visual Studio ホスト マシンの x64 プラットフォームに対してテストするには、[ソリューション プラットフォーム] として **[x64]** 、デバッグ ターゲットとして **[ローカル マシン]** を選択します。 

### <a name="2---start-a-graphics-diagnostics-session"></a>2-グラフィックス診断セッションを開始する
 これで、最初のグラフィックス診断のセッションを開始する準備ができました。 Visual Studio のメイン メニューで、 **[デバッグ] > [グラフィックス] > [グラフィックス デバッグの開始]** の順に選択するか、**Alt + F5** キーを押します。 これで、グラフィックス診断の下でアプリが開始され、Visual Studio の診断セッションのウィンドウが表示されます。

> [!IMPORTANT]
> Windows 10 でアプリを実行しており、オプションのグラフィック ツール機能をまだインストールしていない場合は、今すぐインストールするよう求められます。 インストールは、Windows 10 でグラフィックス診断を使用する前に済ませておく必要があります。

### <a name="3---capture-frames"></a>3 - フレームをキャプチャする
 アプリが起動すると、すぐにフレームをキャプチャできます。

#### <a name="to-capture-single-frames"></a>1 つのフレームをキャプチャするには

- Visual Studio の [グラフィックス] ツール バーまたは診断セッション ウィンドウで、 **[フレームのキャプチャ]** を選択します。 または、アプリにフォーカスがある場合は、キーボードの **Print Screen** キーを押すだけです。

#### <a name="to-capture-a-sequence-of-frames"></a>フレームのシーケンスをキャプチャするには

- Visual Studio の診断セッション ウィンドウの **[キャプチャするフレーム]** にシーケンスでキャプチャするフレームの数を設定し、1 つのフレームをキャプチャするための前述の方法のいずれかに従ってシーケンスをキャプチャします。

   再び 1 つのフレームをキャプチャするには、 **[キャプチャするフレーム]** を *1* に設定します。

  キャプチャが終了したら、アプリケーションを終了するか、[グラフィックス] ツールバーまたは診断セッション ウィンドウから **[停止]** ボタンをクリックします。

### <a name="4---examine-captured-frames-in-the-graphics-analyzer"></a>4 - Graphics Analyzer でキャプチャされたフレームを確認する
 これで、キャプチャしたフレームを詳しく調べる準備ができました。 フレーム分析を開始するには、診断セッション ウィンドウから確認するフレームのフレーム番号を選択します。 これで、フレームが **Graphics Analyzer** で表示され、ここでグラフィックス診断ツールを使用して、アプリがどのように Direct3D を使用しているかを調べてレンダリングの問題を追跡したり、**フレーム分析** ツールを使用して、パフォーマンスを理解したりできます。

 診断セッション ウィンドウで間違ったフレームを選択した場合や、別のフレームを確認する場合は、Graphics Analyzer から新しいフレームを選択できます。 グラフィックス ログ ウィンドウの **[レンダー ターゲット]** タブで、レンダー ターゲットのイメージの下にある **[フレーム一覧]** を展開し、確認する別のフレームを選択します。

 Graphics Analyzer ツールの使用方法の詳細については、[例](graphics-diagnostics-examples.md)を参照してください。

## <a name="see-also"></a>関連項目
- [Direct3D 12 グラフィックス](/windows/desktop/direct3d12/direct3d-12-graphics)