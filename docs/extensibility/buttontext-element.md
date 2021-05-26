---
title: ButtonText 要素 | Microsoft Docs
description: ButtonText 要素を使用すると、さまざまなメニューに表示されるテキストを指定できます。 他のテキスト フィールドが指定されている場合でも、ButtonText 要素を空白することはできません。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ButtonText element (VSCT XML schema)
- VSCT XML schema elements, ButtonText
ms.assetid: 56aba884-0356-4894-ae4e-32d3938f6865
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4fa9ad6aab9d42113f3e01760e191184e168b62d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068116"
---
# <a name="buttontext-element"></a>ButtonText 要素
このフィールドを使用すると、さまざまなメニューに表示されるテキストを指定できます。 既定では、`ButtonText` 要素はメニュー コントローラーに表示されます。 また、他のテキスト フィールドが空白である場合も `ButtonText` 要素が既定値になります。 他のテキスト フィールドが指定されている場合でも、`ButtonText` 要素を空白することはできません。

## <a name="syntax"></a>構文

```xml
<ButtonText>My Command</ButtonText>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[ 要素](../extensibility/strings-element.md)|テキスト要素 (`ButtonText` や `CommandName` など) をグループ化します。|

## <a name="text-value"></a>テキスト値
 `ButtonText` 要素のテキスト値は、表示されるテキストを持つメニュー項目、コンボ、その他のユーザー インターフェイス (UI) 要素に表示されるテキストを提供します。

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
