---
title: 図形とパスの描画
description: Blend for Visual Studio で XAML デザイナーの機能を使用し、パスや図形を描画し、変更し、結合します。
ms.custom: SEO-VS-2020
titleSuffix: Blend for Visual Studio
ms.date: 09/22/2020
ms.topic: conceptual
ms.assetid: d5378c59-e2e5-49f0-91f1-aa82d984a33c
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2e815b3e4959727dab282fcbe0fcd1f82890bf8b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99847350"
---
# <a name="draw-shapes-and-paths"></a>図形とパスの描画

XAML デザイナーでは、"*図形*" とはその名の示すとおりのものです。 たとえば、四角形、円、楕円などです。 *パス* は、より柔軟なバージョンの図形です。 図形の形状を変更したり、図形を結合して新しい図形を形成するといった操作ができます。

図形とパスではベクター グラフィックスを使用するため、高解像度表示に対応して拡大縮小できます。

## <a name="draw-a-shape"></a>図形の描画

図形は **[アセット]** ウィンドウにあります。

:::image type="content" source="media/blend-shapes.png" alt-text="Blend for Visual Studio のスクリーンショット。[アセット] ウィンドウに [図形] カテゴリが表示されています":::

目的の図形をアートボードにドラッグします。 次に、図形にあるハンドルを使用し、図形の拡大縮小、回転、移動、または傾斜を行います。

![ハンドル](../designers/media/84261e83-3091-4490-ab58-4218b188439e.png)

## <a name="draw-a-path"></a>パスの描画

パスは、直線と曲線が連結して一続きになったものです。 パスを使用し、**[アセット]** ウィンドウでは使用できない面白い図形を作成します。

パスの描画には直線、ペン、または鉛筆を使用します。 これらのツールは **[ツール]** ウィンドウにあります。

### <a name="draw-a-straight-line"></a>直線の描画

**[ペン]** ツールまたは **[直線]** ツールを使用します。

**ペン ツールの使用**

アートボード上で 1 回クリックし、始点を定義します。次に、再度クリックして直線の終わりを定義します。

**直線ツールの使用**

アートボード上で、直線の始点からドラッグして、終点でマウス ボタンを放します。

### <a name="draw-a-curve"></a>曲線の描画

**[ペン]** ツールを使用します。

アートボード上で 1 回クリックして、直線の始点を定義してから、ポインターをクリックし、ドラッグして目的の曲線を作成します。

パスを閉じる場合は、線上の最初の点をクリックします。

### <a name="change-the-shape-of-a-curve"></a>曲線のシェイプの変更

**[個別選択]** ツールを使用します。

図形をクリックしてから、図形の任意のポイントをドラッグして曲線の形状を変更します。

### <a name="draw-a-free-form-path"></a>フリーハンドのパスの描画

**[鉛筆]** ツールを使用します。

アートボード上で、実際の鉛筆のように自由にパスを描画できます。

### <a name="remove-part-of-a-path"></a>パスの一部の削除

**[個別選択]** ツールを使用します。

削除する部分を含むパスを選択して、 **[削除]** ボタンをクリックします。

### <a name="remove-a-point-in-a-path"></a>パス内のポイントの削除

**[選択]** ツールを使用してパスを選択します。 次に、**[ペン]** ツールを使用し、削除するポイントをクリックします。

### <a name="add-a-point-to-a-path"></a>パスへのポイントの追加

**[選択]** ツールを使用してパスを選択します。 **[ペン]** ツールを使用し、ポイントを追加するパス上の任意の場所をクリックします。

## <a name="convert-a-shape-to-a-path"></a>図形のパスへの変換

パスを変更するのと同じ方法で図形を変更するには、図形をパスに変換します。 図形を選択し、 **[フォーマット]** 、 **[パス]** 、 **[パスに変換]** の順に選択します。

**短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.png) [パスの作業: 図形をパスに変換する](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=147)。

> [!NOTE]
> **[パスに変換]** は現在のところ、最小 `TargetPlatformVersion` が 10.0.16299.0 以降の UWP アプリでは利用できません。

## <a name="combine-paths"></a>パスの結合

パスと図形を結合して 1 つのパスにすることができます。

![パスの結合](../designers/media/2df17a5d-a338-4ef4-96c5-dae51cc1ca8a.png)

|Number|アクション|
|-|-|
|![結合前の 2 つの図形](../designers/media/b1_1.png)|結合前の 2 つの図形|
|![合算](../designers/media/b1_2.png)|合算|
|![除算](../designers/media/b1_3.png)|除算|
|![交差](../designers/media/b1_4.png)|交差|
|![重複部分を除外](../designers/media/b1_5.png)|重複部分を除外|
|![減算](../designers/media/b1_6.png)|減算|

**短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.png) [パスの作業: パスを結合する](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=195)。

## <a name="create-a-compound-path"></a>複合パスの作成

複合パスを作成するときは、パスの交差している部分が減算されます。複合後のパスのビジュアル プロパティは、最背面にあったパスと同じになります。

複合パスは、作成後はいつでも分離できます。

![複合パスを分離する](../designers/media/2157a8aa-d9a7-4de4-8de5-b10d28f08a84.png)

**短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.png) [パスの作業: 複合パスを作成する](https://www.youtube.com/watch?v=Io5bC0-nH6Q)。

## <a name="create-a-clipping-path"></a>クリッピング パスの作成

クリッピング パスは、別のオブジェクトに適用するパスまたは図形です。クリッピング パスの外側のオブジェクトがマスクされて非表示になります。

![クリッピング パス](../designers/media/22471e98-a841-4f39-a3ef-36090cf5a625.png)

**短いビデオを見る:** ![インストール済みフィーチャーの構成](../designers/media/bldadminconsoleinitialconfigicon.png) [パスの作業: クリッピング パスを作成する](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=232)。
