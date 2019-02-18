---
title: 'チュートリアル: プログラムによるグラフィックス情報のキャプチャ |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 379180c21bfe1bbb36faa0ad1becad162068e698
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "55001187"
---
# <a name="walkthrough-capturing-graphics-information-programmatically"></a>チュートリアル: プログラムによるグラフィックス情報のキャプチャ
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のグラフィックス診断を使用すると、Direct3D アプリケーションからプログラムによってグラフィックス情報をキャプチャできます。  
  
 プログラムによるキャプチャは次のようなシナリオで役立ちます。  
  
-   存在するスワップチェーンをグラフィックス アプリケーションが使用しないとき (テクスチャにレンダリングするときなど)、プログラムによるキャプチャを開始します。  
  
-   アプリケーションがまったくレンダリングしないとき (DirectCompute を使用して計算を実行するときなど)、プログラムによるキャプチャを開始します。  
  
-   レンダリングの問題を予測して手動テストでキャプチャすることは難しいものの、実行時にアプリケーションの状態に関する情報を使用してプログラムで予測できるときは、 `CaptureCurrentFrame`を呼び出します。  
  
##  <a name="CaptureDX11_2"></a> Windows 10 のプログラムによるキャプチャ  
 このチュートリアルのパートでは、Windows 10 で DirectX 11.2 API を使用するアプリケーションでのプログラムによるキャプチャについて説明します。ここでは、堅牢なキャプチャ方法を使用します。
  
 このセクションでは、次のタスクを実行する方法を示します。  
  
-   プログラムによるキャプチャを使用するためにアプリケーションを準備する  
  
-   IDXGraphicsAnalysis インターフェイスを取得する  
  
-   グラフィックス情報をキャプチャする  
  
> [!NOTE]
>  プログラムによるキャプチャの以前の実装は、Remote Tools for Visual Studio をいました[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]キャプチャ機能を提供します。
  
### <a name="preparing-your-app-to-use-programmatic-capture"></a>プログラムによるキャプチャを使用するためにアプリケーションを準備する  
 アプリケーションでプログラムによるキャプチャを使用するには、必要なヘッダーをインクルードすることが必要です。 これらのヘッダーは、Windows 10 の SDK の一部です。  
  
##### <a name="to-include-programmatic-capture-headers"></a>プログラムによるキャプチャのヘッダーをインクルードするには  
  
-   IDXGraphicsAnalysis インターフェイスを定義するソース ファイルに、次のヘッダーをインクルードします。  
  
    ```cpp
    #include <DXGItype.h>  
    #include <dxgi1_2.h>  
    #include <dxgi1_3.h>  
    #include <DXProgrammableCapture.h>  
    ```  
  
    > [!IMPORTANT]
    >  ご利用の Windows 10 アプリケーションでプログラムによるキャプチャを実行するには、ヘッダー ファイル vsgcapture.h をインクルードしないでください。このファイルでサポートされているのは Windows 8.0 以前でのプログラムによるキャプチャです。 このヘッダーは DirectX 11.2 で使用することはできません。 D3d11_2.h ヘッダーが含まれる後にこのファイルが含まれる場合は、コンパイラは警告を発行します。 Vsgcapture.h が d3d11_2.h する前に含まれている場合、アプリは起動しません。  
  
    > [!NOTE]
    >  コンピューターに June 2010 DirectX SDK がインストールされており、プロジェクトのインクルード パスに `%DXSDK_DIR%includex86`が含まれている場合は、それをインクルード パスの最後に移動します。 ライブラリ パスでも同様にします。  
  
### <a name="getting-the-idxgraphicsanalysis-interface"></a>IDXGraphicsAnalysis インターフェイスを取得する  
 DirectX 11.2 からグラフィックス情報をキャプチャする前に、DXGI デバッグ インターフェイスを取得する必要があります。  
  
> [!IMPORTANT]
>  グラフィックス診断の下でアプリを実行するプログラムによるキャプチャを使用する場合もする必要があります (alt キーを押しながら f5 キーで[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]) または 、[コマンド ライン キャプチャ ツール](command-line-capture-tool.md)します。  
  
##### <a name="to-get-the-idxgraphicsanalysis-interface"></a>IDXGraphicsAnalysis インターフェイスを取得するには  
  
- 以下のコードを使用して、DXGI デバッグ インターフェイスに対して IDXGraphicsAnalysis インターフェイスをフックします。  
  
  ```cpp
  IDXGraphicsAnalysis* pGraphicsAnalysis;  
  HRESULT getAnalysis = DXGIGetDebugInterface1(0, __uuidof(pGraphicsAnalysis), reinterpret_cast<void**>(&pGraphicsAnalysis));  
  ```  
  
   確認してください、`HRESULT`によって返される[DXGIGetDebugInterface1](/windows/desktop/api/dxgi1_3/nf-dxgi1_3-dxgigetdebuginterface1)使用する前に、有効なインターフェイスを取得するために。  
  
  ```cpp
  if (FAILED(getAnalysis))  
  {  
      // Abort program or disable programmatic capture in your app.  
  }  
  ```  
  
  > [!NOTE]
  >  場合`DXGIGetDebugInterface1`返します`E_NOINTERFACE`(`error: E_NOINTERFACE No such interface supported`)、アプリがグラフィックス診断の下で実行されていることを確認 (alt キーを押しながら f5 キーで[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)])。  
  
### <a name="capturing-graphics-information"></a>グラフィックス情報をキャプチャする  
 これで、正しい `IDXGraphicsAnalysis` インターフェイスを取得できたので、 `BeginCapture` および `EndCapture` を使用してグラフィックス情報をキャプチャできます。  
  
##### <a name="to-capture-graphics-information"></a>グラフィックス情報をキャプチャするには  
  
- グラフィックス情報のキャプチャを開始するには、 `BeginCapture`を使用します。  
  
    ```cpp
    ...  
    pGraphicsAnalysis->BeginCapture();  
    ...  
    ```  
  
     `BeginCapture` が呼び出されるとキャプチャはすぐに始まり、次のフレームが開始するのを待ちません。 現在のフレームが表示されたとき、または `EndCapture`を呼び出したときにキャプチャは停止します。  
  
    ```cpp
    ...  
    pGraphicsAnalysis->EndCapture();  
    ...  
    ```  

- 呼び出し後`EndCapture`、グラフィックス オブジェクトを解放します。 
  
## <a name="next-steps"></a>次の手順  
 このチュートリアルでは、プログラムでグラフィックス情報をキャプチャする方法を示しました。 次の手順では、次のオプションを検討します。  
  
-   グラフィックス診断ツールを使用してキャプチャされたグラフィックス情報を解析する方法について学習します。 参照してください[概要](overview-of-visual-studio-graphics-diagnostics.md)します。  
  
## <a name="see-also"></a>関連項目  
 [チュートリアル: グラフィックス情報をキャプチャする](walkthrough-capturing-graphics-information.md)   
 [Capturing Graphics Information](capturing-graphics-information.md)   
 [コマンド ライン キャプチャ ツール](command-line-capture-tool.md)
