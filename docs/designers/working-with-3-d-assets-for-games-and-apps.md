---
title: "ゲームとアプリケーション用の 3D アセットの操作 | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vs.graphics"
ms.assetid: 910d673b-c884-4eeb-9928-0e89f3d38cb6
caps.latest.revision: 24
caps.handback.revision: 24
author: "BrianPeek"
ms.author: "brpeek"
manager: "ghogen"
---
# ゲームとアプリケーション用の 3D アセットの操作
[!INCLUDE[vs2017banner](../code-quality/includes/vs2017banner.md)]

このドキュメントでは、DirectX ベースのゲームおよびアプリケーション向けの 3\-D モデル、テクスチャ、シェーダーの作成または変更に使用できる、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のツールについて説明します。  
  
## Visual Studio における DirectX アプリケーションの開発  
 DirectX アプリケーションは、通常、プログラミング ロジック、DirectX API、および HLSL \(High Level Shading Language\) プログラムを、オーディオおよび 3\-D ビジュアル アセットと組み合わせることによって、リッチで対話型のマルチメディア エクスペリエンスを提供します。  [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] には、イメージとテクスチャ、3\-D モデル、シェーダーなどの操作を行うために使用できるツールが用意されています。そのため、別のツールを使用するために IDE を終了する必要がありません。  Visual Studio のツールは、*プレースホルダー* アセットの作成に特に適しています。プレースホルダーを使用すると、稼動準備のできたアセットをコミッションする前にコードのテストやプロトタイプの構築を行ったり、稼動準備のできたアセットをアプリケーションのデバッグ時に検査および変更したりすることができます。  
  
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で使用できるアセットの種類に関する詳細を以下に示します。  
  
### イメージおよびテクスチャ  
 イメージとテクスチャは、ゲームやアプリケーションに色と視覚的なディテールを与えます。  3\-D グラフィックスでは、さまざまな用途に対応した、さまざまな形式、種類、および形状のテクスチャが使用されます。  たとえば、通常のマップには、3\-D モデルの精細な光源を生成するためのピクセル単位の表面法線があり、キューブ マップには、スカイボックス化、反射、球状テクスチャ マッピングなどのための全方向テクスチャがあります。  テクスチャは、さまざまな精細度のレンダリングを効率的に行うための MIP マップを備えており、さまざまなチャネルと順序の色をサポートしています。  テクスチャはさまざまな圧縮形式で格納できます。圧縮形式は専用グラフィックス メモリの占有率が低いため、GPU はテクスチャに効率的にアクセスできるようになります。  
  
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のイメージ エディターを使用すると、さまざまな一般的な種類や形式のイメージとテクスチャを操作できます。  
  
### 3\-D モデル  
 3\-D モデルは、ゲームやアプリケーションで空間と図形を作成します。  3\-D モデルでは、3\-D 空間内の各ポイント \(*頂点*とも呼ばれる\) の位置をインデックス化データと共にエンコードするなどして、そのモデルの形状を表す線や三角形が定義されます。  これらの頂点には、色の情報、法線ベクター、アプリケーションに固有の属性など、追加のデータを関連付けることができます。  オブジェクトのサーフェイスの外観を計算するためにどのシェーダーを使用し、どのテクスチャを適用するかなど、オブジェクト全体の属性もモデルごとに定義できます。  
  
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のモデル エディターを使用すると、さまざまな一般的な形式の 3\-D モデルを操作できます。  
  
### シェーダー  
 シェーダーとは、グラフィックス プロセッシング ユニット \(GPU\) 上で実行される、ドメインに固有の小容量プログラムのことです。  シェーダーは、3\-D モデルを画面上の図形に変換する方法と、それらの図形を構成する各ピクセルに色を指定する方法を決定します。  シェーダーを作成して、ゲームまたはアプリケーション内のオブジェクトに適用することにより、そのオブジェクトに独自の外観を持たせることができます。  
  
 グラフ ベースのシェーダー デザイン ツールである [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のシェーダー デザイナーを使用すると、HLSL プログラミングに関する知識がなくてもカスタムの視覚効果を作成できます。  
  
> [!NOTE]
>  DirectX プログラミングの開始方法の詳細については、「[DirectX Graphics and Gaming \(DirectX のグラフィックスとゲーム\)](http://go.microsoft.com/fwlink/p/?LinkId=224633)」を参照してください。  DirectX ベースのアプリケーションをデバッグする方法の詳細については、「[グラフィックス診断 \(DirectX グラフィックスのデバッグ\)](../debugger/visual-studio-graphics-diagnostics.md)」を参照してください。  
  
## DirectX のバージョンの互換性  
 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、2\-D および 3\-D アセットのレンダリングに DirectX が使用されます。  DirectX 11 のレンダラーと Windows Advanced Rasterization Platform \(WARP\) ソフトウェアのレンダラーのいずれかを選択できます。  DirectX 11 のレンダラーを使用すると、DirectX 11 および DirectX 10 の各 GPU 上でハードウェア アクセラレータによる高性能レンダリングを実行できます。  WARP レンダラーを使用すると、最新式のグラフィックス ハードウェアを搭載していないコンピューターからグラフィックス ハードウェアを内蔵しているコンピューターまで、多様な種類のコンピューターとアセットが確実に連動するようになります。  WARP の詳細については、「[Windows Advanced Rasterization Platform \(WARP\) Guide \(Windows Advanced Rasterization Platform \(WARP\) ガイド\)](http://go.microsoft.com/fwlink/p/?LinkId=224634)」を参照してください。  
  
## 関連トピック  
  
|タイトル|説明|  
|----------|--------|  
|[テクスチャおよびイメージの使用](../designers/working-with-textures-and-images.md)|[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を使用してイメージとテクスチャを操作する方法について説明します。|  
|[3\-D モデルの操作](../designers/working-with-3-d-models.md)|[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を使用して 3\-D モデルを操作する方法について説明します。|  
|[シェーダーの操作](../designers/working-with-shaders.md)|[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のシェーダー デザイナーを使用してカスタム シェーダー効果を作成および変更する方法について説明します。|  
|[ゲームまたはアプリケーションでの 3\-D アセットの使用](../designers/using-3-d-assets-in-your-game-or-app.md)|イメージ エディター、モデル エディター、またはシェーダー デザイナーを使用して作成したアセットをゲームまたはアプリケーションで使用する方法について説明します。|