---
title: Bitmap 要素 | Microsoft Docs
description: Bitmap 要素では、ビットマップを定義します。 ビットマップは、リソースまたはファイルのどちらかから読み込まれます。 この記事には例が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Bitmaps
- Bitmaps element (VSCT XML schema)
ms.assetid: edcd7891-f4e7-416d-809d-5e2eed9f17e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c8f3daf25a3ffe025bcdef65dbaa6def942d0fb4
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903321"
---
# <a name="bitmap-element"></a>Bitmap 要素
ビットマップを定義します。 ビットマップは、リソースまたはファイルのどちらかから読み込まれます。

## <a name="syntax"></a>構文

```
<Bitmap guid="guidImages" href="images\MyImage.bmp" usedList="bmp1, bmp2, bmp3" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 GUID/ID コマンド識別子の GUID。<br /><br /> ビットマップの guid 属性は、どの VSPackage またはその他のコマンド グループにも関連付けられていません。  これはビットマップ定義に対して一意である必要があり、他のどの目的にも使用できません。|
|resID|GUID/ID コマンド識別子の ID。 resID または href 属性のどちらかが必要です。<br /><br /> resID 属性は、コマンド テーブルのマージ中に読み込まれるビットマップ ストリップを決定する整数のリソース ID です。  コマンド テーブルが読み込まれているときに、このリソース ID で指定されたビットマップが同じモジュールのリソースから読み込まれます。|
|usedList|resID 属性が存在する場合に必要です。 ビットマップ ストリップ内の使用可能な画像を選択します。|
|href|ビットマップのパス。 resID または href 属性のどちらかが必要です。<br /><br /> このインクルード パスは、生成されたバイナリに埋め込まれている指定された画像ファイルのために検索されます。  コマンド テーブルのマージ中に、画像がコピーされ、追加のリソース検索または読み込みは必要ありません。  usedList 属性が存在しない場合は、このストリップ内のすべての画像が使用可能になります。 **注:** 画像は、 *.bmp*、 *.png*、 *.gif* などの複数の形式のいずれかで指定できます。  以前のバージョンのコンパイラでは、部分的な透明度に関するアルファ情報を持つ 32 ビットのビットマップ画像をサポートしていませんでした。 これらのバージョンでの回避策として、 *.png* 形式を使用してください。|
|条件|省略可能。 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)に関するページを参照してください。|

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Bitmaps 要素](../extensibility/bitmaps-element.md)|Bitmap 要素をグループ化します。|

## <a name="example"></a>例

```
<Bitmap guid="guidWidgetIcons" href="WidgetToolbarIcons_32.bmp" />
<Bitmap guid="guidWidgetIcons2" resID="IDBMP_WIDGETICONS"
  usedList="1, 2, 3, 4"/>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
