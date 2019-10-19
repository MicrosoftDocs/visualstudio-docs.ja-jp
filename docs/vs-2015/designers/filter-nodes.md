---
title: フィルター ノード | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: f7cae2dc-e9a7-49d4-8be5-58b79868624e
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 50f34f9706e9160cedaed09467fcf73b337a8329
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72664676"
---
# <a name="filter-nodes"></a>フィルター ノード
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Shader Designer では、フィルター ノードは入力 (色やテクスチャのサンプルなど) を比喩色値に変換します。 この比喩色値は、一般的に非写実的なレンダリングや、他の視覚効果のコンポーネントとして使用されます。

## <a name="filter-node-reference"></a>フィルター ノードの参照

|ノード|説明|プロパティ|
|----------|-------------|----------------|
|**ぼかし**|ガウス関数を使用して、テクスチャのピクセルをぼかします。<br /><br /> テクスチャ内の色の詳細やノイズを軽減するために使用できます。<br /><br /> **入力:**<br /><br /> `UV`: `float2`<br /> テストするテクセルの座標。<br /><br /> **出力:**<br /><br /> `Output`: `float4`<br /> ぼかした色の値。|**テクスチャ**<br /> ぼかし適用時に使用されるサンプラーに関連付けられているテクスチャ レジスターです。|
|**再度を下げる**|指定した色の色の量を減らします。<br /><br /> 色を削除すると、色の値はグレースケール相当に近づきます。<br /><br /> **入力:**<br /><br /> `RGB`: `float3`<br /> 彩度を下げる色。<br /><br /> `Percent`: `float`<br /> 削除する色の割合。範囲 [0, 1] の正規化された値として表現されます。<br /><br /> **出力:**<br /><br /> `Output`: `float3`<br /> 再度が下げられた色。|**輝度**<br /> 赤、緑、青の色要素に対する重みです。|
|**境界の検出**|キャニー境界検出を使用して、テクスチャの境界を検出します。 境界のピクセルは白で出力されます。境界以外のピクセルは黒で出力されます。<br /><br /> テクスチャの境界を識別し、境界のピクセルを扱う他の効果を適用するために使用できます。<br /><br /> **入力:**<br /><br /> `UV`: `float2`<br /> テストするテクセルの座標。<br /><br /> **出力:**<br /><br /> `Output`: `float4`<br /> 境界にテクセルがある場合は白、それ以外の場合は黒です。|**テクスチャ**<br /> 境界検出で使用されるサンプラーに関連付けられているテクスチャ レジスターです。|
|**シャープにする**|テクスチャをシャープにします。<br /><br /> テクスチャの詳細を強調表示するために使用できます。<br /><br /> **入力:**<br /><br /> `UV`: `float2`<br /> テストするテクセルの座標。<br /><br /> **出力:**<br /><br /> `Output`: `float4`<br /> ぼかした色の値。|**テクスチャ**<br /> シャープにするときに使用されるサンプラーに関連付けられているテクスチャ レジスターです。|
