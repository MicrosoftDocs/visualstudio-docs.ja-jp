---
title: Icon 要素 | Microsoft Docs
description: Visual Studio IDE 拡張機能で使用されるアイコンを表す Icon 要素について説明します。使用されるビットマップの属性や、ビットマップ ストリップのスロットが含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Icon
- Icon element (VSCT XML schema)
ms.assetid: 73c58fe3-d53c-4f4e-b025-29567c6cbb7c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 52ccb8093b61e0458f7c3caefea6f826609aa51d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082141"
---
# <a name="icon-element"></a>Icon 要素
Icon タグの guid 属性は、定義されているビットマップの GUID です。 `id` 属性により、ビットマップ ストリップ内のスロットが選択されます。 この要素は省略可能です。 この要素が含まれていない場合は、暗黙で **guidOfficeIcon:msotcidNoIcon** の値が指定されます。

## <a name="syntax"></a>構文

```xml
<Icon guid="guidImages" id="bmpPic1" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|guid|必須。 定義されているビットマップの GUID。|
|id|必須。 ビットマップ ストリップ内のスロットを選択します。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[なし] :|なし。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Buttons 要素](../extensibility/buttons-element.md)||

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
