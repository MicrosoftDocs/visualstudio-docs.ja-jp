---
title: グラフィックス診断の概要 |Microsoft Docs
ms.custom: seodec18
ms.date: 05/26/2017
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 38138e1e6997156042be21c769238d03cf4403e8
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "55014225"
---
# <a name="getting-started-with-visual-studio-graphics-diagnostics"></a>Visual Studio グラフィックス診断の使用を開始する
このセクションでは、まずグラフィックス診断を初めて使用するための準備をしてから、Direct3D アプリケーションのフレームをキャプチャして Graphics Analyzer でそれらを確認します。  
  
## <a name="requirements"></a>要件  
 Visual Studio のグラフィックス診断を使用するには、Visual Studio Enterprise、Visual Studio Professional、または Visual Studio Community を使用する必要があります。  Visual Studio のコードを含む、他のエディションでは、この機能は含まれません。
 
 [!INCLUDE[downloadvs](../includes/downloadvs_md.md)]  
  
### <a name="windows-10-prerequisites"></a>Windows の 10 の前提条件  
 Windows のオプション機能の "*グラフィック ツール*" は Windows 10 でのグラフィックス診断に必要なキャプチャと再生のインフラストラクチャを提供します。  
  
 グラフィック ツールをインストールする方法の詳細については、「[Windows 10 のグラフィック ツールをインストールする](#InstallGraphicsTools)」を参照してください。  
  
##  <a name="InstallGraphicsTools"></a> Windows 10 用のグラフィック ツールをインストールする  
 Windows 10 では、グラフィックス診断のインフラストラクチャが、"*グラフィック ツール*" と呼ばれる Windows のオプション機能によって提供されます。 この機能は、キャプチャするアプリが以前のバージョンの Windows を対象にしているかどうか、またはどのバージョンの Direct3D を使用しているかに関係なく、Windows 10 でグラフィックス情報をキャプチャおよび再生するために必要です。 グラフィック ツール機能を事前にインストールすることができます。それ以外の場合は、Visual Studio からグラフィックス診断セッションを最初に開始するときに、オンデマンドでインストールされます。  
  
#### <a name="to-install-graphics-tools-for-windows-10"></a>Windows 10 用のグラフィック ツールをインストールするには  
  
1. Search では、次のように入力します。**アプリおよび機能**を開き、**アプリと機能**設定します。
  
2. 右側にある、**アプリと機能**ダイアログ ボックスで、選択**省略可能な機能を管理する**(**アプリと機能**)。

   **[オプション機能の管理]** ダイアログが表示されます。
  
3. **[オプション機能の管理]** ダイアログで、**[機能の追加]** を選択します。 インストールできるオプション機能の一覧が表示されます。  
  
4. 機能の一覧から **[グラフィック ツール]** を選択して、**[インストール]** を選択します。  
  
   グラフィック ツールの機能は Windows 10 SDK をインストールするときにも、自動的にインストールされます。  
  
> [!TIP]
>  Windows 10 のオプションのグラフィック ツール機能は、コマンド ライン キャプチャ プログラム **dxcap.exe** など、軽量のキャプチャおよび再生機能を提供しており、開発者用ツールがインストールされていないコンピューターでサポート、テスト、および診断を行うシナリオで利用できます。 詳細については、「[コマンド ライン キャプチャ ツール](command-line-capture-tool.md)」のトピックを参照してください。  
  
## <a name="using-graphics-diagnostics-for-the-first-time"></a>グラフィックス診断を初めて使用する  
 これで、必要なものがすべて揃い、グラフィックス診断の使用を開始する準備が整いました。 以下の手順に実行します。  
  
### <a name="1---create-a-direct3d-app"></a>1 -、Direct3D アプリを作成する  
 非常に使用すると、グラフィックス診断を探索する独自の Direct3D アプリが既にあります。 場合、 それ以外の場合、次のいずれかを使用します。

- **DirectX 11 アプリ (ユニバーサル Windows)** または**DirectX 12 アプリ (ユニバーサル Windows)** Windows 10 用のプロジェクト テンプレート。
- [Direct3d12 UAP サンプル](https://code.msdn.microsoft.com/Direct3D-12-UAP-Sample-ecb1779f)Windows 10 用です。  
  
  先に進む前に、アプリをビルドできるかどうかを確認します。  
  
### <a name="2---start-a-graphics-diagnostics-session"></a>2-グラフィックス診断セッションを開始する  
 これで、最初のグラフィックス診断のセッションを開始する準備ができました。 Visual Studio のメイン メニューで、選択**デバッグ、グラフィックス、グラフィックス デバッグの開始**、キーを押すか**alt キーを押しながら f5 キー**します。 これで、グラフィックス診断の下でアプリが開始され、Visual Studio の診断セッションのウィンドウが表示されます。  
  
> [!IMPORTANT]
>  Windows 10 でアプリを実行しており、オプションのグラフィック ツール機能をまだインストールしていない場合は、今すぐインストールするよう求められます。 インストールは、Windows 10 でグラフィックス診断を使用する前に済ませておく必要があります。  
  
### <a name="3---capture-frames"></a>3 - フレームをキャプチャする  
 アプリが起動すると、すぐにフレームをキャプチャできます。  
  
#### <a name="to-capture-single-frames"></a>1 つのフレームをキャプチャするには  
  
-   Visual Studio の [グラフィックス] ツール バーまたは診断セッション ウィンドウで、**[フレームのキャプチャ]** を選択します。 または、アプリにフォーカスがある場合は、キーを押す、 **Print Screen**キーボードのキー。
  
#### <a name="to-capture-a-sequence-of-frames"></a>フレームのシーケンスをキャプチャするには  
  
- Visual Studio の診断セッション ウィンドウの **[キャプチャするフレーム]** にシーケンスでキャプチャするフレームの数を設定し、1 つのフレームをキャプチャするための前述の方法のいずれかに従ってシーケンスをキャプチャします。  
  
   再び 1 つのフレームをキャプチャするには、**[キャプチャするフレーム]** を *1* に設定します。  
  
  キャプチャが終了したら、アプリケーションを終了するか、[グラフィックス] ツールバーまたは診断セッション ウィンドウから **[停止]** ボタンをクリックします。  
  
### <a name="4---examine-captured-frames-in-the-graphics-analyzer"></a>4 - Graphics Analyzer でキャプチャされたフレームを確認する  
 これで、キャプチャしたフレームを詳しく調べる準備ができました。 フレーム分析を開始するには、診断セッション ウィンドウから確認するフレームのフレーム番号を選択します。 これで、フレームが **Graphics Analyzer** で表示され、ここでグラフィックス診断ツールを使用して、アプリがどのように Direct3D を使用しているかを調べてレンダリングの問題を追跡したり、**フレーム分析**ツールを使用して、パフォーマンスを理解したりできます。  
  
 診断セッション ウィンドウで間違ったフレームを選択した場合や、別のフレームを確認する場合は、Graphics Analyzer から新しいフレームを選択できます。 グラフィックス ログ ウィンドウの **[レンダー ターゲット]** タブで、レンダー ターゲットのイメージの下にある **[フレーム一覧]** を展開し、確認する別のフレームを選択します。  
  
 Graphics Analyzer ツールを一緒に使用する方法の詳細については、次を参照してください。、[例](graphics-diagnostics-examples.md)します。  
  
## <a name="see-also"></a>関連項目  
 [Direct3D 12 グラフィックス](/windows/desktop/direct3d12/direct3d-12-graphics)