---
title: '方法: Direct2D または JavaScript アプリで使用するためのテクスチャをエクスポートする | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 241c25fe-764e-4e1b-ad32-b1377dcbb605
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: e2b08760e567f6e000e191703695ee0703da7215
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49812141"
---
# <a name="how-to-export-a-texture-for-use-with-direct2d-or-javascipt-apps"></a>方法: Direct2D または Javascipt アプリで使用するためのテクスチャをエクスポートする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

イメージ コンテンツ パイプラインにより、Direct2D の内部レンダリング規則と互換性のあるテクスチャを生成できます。 この種のテクスチャの用途に適しているのは、Direct2D を使用するアプリや、JavaScript で作成する Windows Store アプリです。  
  
 このドキュメントでは、以下のアクティビティについて説明します。  
  
-   イメージ コンテンツ パイプラインによって処理されるようにソース イメージを構成する。  
  
-   Direct2D または JavaScript アプリで使用できるテクスチャを生成するようにイメージ コンテンツ パイプラインを構成する。  
  
    -   ブロック圧縮形式の .dds ファイルを生成する。  
  
    -   前乗算されたアルファを生成する。  
  
    -   MIPMAP の生成を無効にする。  
  
## <a name="rendering-conventions-in-direct2d"></a>Direct2D のレンダリング規則  
 Direct2D のコンテキストで使用するテクスチャは、次に示す Direct2D の内部レンダリング規則に準拠している必要があります。  
  
-   Direct2D では、前乗算されたアルファを使用することで透明性と透光性を実現します。 Direct2D と組み合わせて使用するテクスチャには、前乗算されたアルファが含まれている必要があります。この要件は、テクスチャで透明性または透光性を使用しない場合でも同様です。 前乗算されたアルファに関する詳細については、「[方法: 前乗算されたアルファを持つテクスチャをエクスポートする](../designers/how-to-export-a-texture-that-has-premultiplied-alpha.md)」を参照してください。  
  
-   テクスチャは次のいずれかのブロック圧縮形式の .dds ファイルで提供する必要があります。  
  
    -   BC1_UNORM 圧縮  
  
    -   BC2_UNORM 圧縮  
  
    -   BC3_UNORM 圧縮  
  
-   MIPMAP はサポートされていません。  
  
#### <a name="to-create-a-texture-thats-compatible-with-direct2d-rendering-conventions"></a>Direct2D のレンダリング規則に準拠したテクスチャを作成するには  
  
1. 基本的なテクスチャを作成します。 既存のイメージを読み込むか、「[方法: 基本テクスチャを作成する](../designers/how-to-create-a-basic-texture.md)」の手順に従って新しいイメージを作成します。 DDS 形式でブロック圧縮をサポートするには、100x100、128x128、256x192 など、サイズの幅と高さが 4 の倍数であるテクスチャを指定します。 MIPMAP はサポートされていないため、テクスチャは正方形である必要がなく、サイズも 2 の累乗である必要はありません。  
  
2. イメージ コンテンツ パイプラインによって処理されるようにテクスチャ ファイルを構成します。 **ソリューション エクスプローラー**で、先ほど作成したテクスチャ ファイルのショートカット メニューを開き、**[プロパティ]** をクリックします。 **[構成プロパティ]** の **[全般]** ページで、**[項目の種類]** を **[Image Content Pipeline]** (イメージ コンテンツ パイプライン) に設定します。 **[コンテンツ]** が **[はい]** に、**[ビルドから除外]** が **[いいえ]** に設定されていることを確認し、**[適用]** ボタンをクリックします。 **[イメージ コンテンツ パイプライン]** の構成プロパティ ページが表示されます。  
  
3. 出力形式を、いずれかのブロック圧縮形式に設定します。 **[構成プロパティ]** で、**[イメージ コンテンツ パイプライン]**、**[全般]** ページの順にクリックし、**[圧縮]** を **[BC3_UNORM compression (/compress:BC3_UNORM)]** (BC3_UNORM 圧縮 (/compress:BC3_UNORM)) に設定します。 要件に応じて、他の BC1、BC2、または BC3 形式を選択することもできます。 Direct2D では現在、BC4、BC5、BC6、または BC7 テクスチャはサポートされていません。 各種の BC 形式の詳細については、「[ブロック圧縮 (Direct3D 10)](http://msdn.microsoft.com/library/windows/desktop/bb694531.aspx)」を参照してください。  
  
   > [!NOTE]
   >  指定した圧縮形式により、イメージ コンテンツ パイプラインによって生成されるファイルの形式が決まります。 これは、イメージ エディターからソース イメージの **[形式]** で指定する形式とは異なります。[形式] で指定するのは、ソース イメージ ファイルがディスクに格納されるときのファイル形式 (*作業形式*) です。 通常、圧縮された作業形式は必要ありません。  
  
4. 前乗算されたアルファを使用して出力を生成するようにイメージ コンテンツ パイプラインを構成します。 **[構成プロパティ]** で、**[イメージ コンテンツ パイプライン]**、**[全般]** の順にクリックし、**[Convert to pre-multiplied alpha format]** (前乗算されたアルファ形式に変換) プロパティを **[はい (/generatepremultipliedalpha)]** に設定します。  
  
5. MIPMAP が生成されないように、イメージ コンテンツ パイプラインを構成します。 **[構成プロパティ]** で、**[イメージ コンテンツ パイプライン]**、**[全般]** ページの順にクリックし、**[MIPS の生成]** を **[いいえ]** に設定します。  
  
6. **[OK]** を選択します。  
  
   プロジェクトをビルドすると、イメージ コンテンツ パイプラインによってソース イメージが作業形式から、指定した出力形式に変換されます。同時に、前乗算されたアルファが生成されます。結果はプロジェクトの出力ディレクトリにコピーされます。



