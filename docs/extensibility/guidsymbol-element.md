---
title: GuidSymbol 要素 | Microsoft Docs
description: GuidSymbol 要素には、メニュー、グループ、またはコマンドを表す GUID:ID ペアの GUID が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, GuidSymbol
- GuidSymbol element (VSCT XML schema)
ms.assetid: 11fb3545-8974-4776-9a54-6b6e7739ae31
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7c30c7a48b03b5deed3267e106e926d3cb5114c1
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902762"
---
# <a name="guidsymbol-element"></a>GuidSymbol 要素
`GuidSymbol` 要素には、メニュー、グループ、またはコマンドを表す GUID:ID ペアの GUID が含まれています。 ID は、`GuidSymbol` 要素の `IDSymbol` 要素から取得されます。 `GuidSymbol` 要素には、`value` 属性に含まれている GUID のフレンドリ名を提供する `name` 属性があります。

## <a name="syntax"></a>構文

```xml
<GuidSymbol name="guidMyCommandSet" value="{xxxxxxxxxxxxx-xxxx-xxxx-xxxxxxxxxxxx}">
  <IDSymbol>... </IDSymbol>
  <IDSymbol>... </IDSymbol>
</GuidSymbol>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|name|必須。 GUID シンボルの名前。|
|value|必須。 GUID シンボルの GUID。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[IDSymbol 要素](../extensibility/idsymbol-element.md)|メニュー、グループ、またはコマンドを表す GUID:ID ペアの ID が含まれています。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Symbols 要素](../extensibility/symbols-element.md)|*.vsct* ファイル内の `GuidSymbol` 要素をグループ化します。|

## <a name="remarks"></a>解説
 通常、 *.vsct* ファイルには、`Symbols` セクションに 3 つの `GuidSymbol` 要素が含まれています。1 つはパッケージ自体用、もう 1 つはコマンド セット (パッケージにより使用可能になるメニュー、グループ、コマンドのコレクション)、もう 1 つはボタンとその他のビジュアル コンポーネントのアイコンを提供するビットマップ用です。 所与の `GuidSymbol` 要素内のすべての `IDSymbol` 要素は、一意の `value` を持つ必要があります。ただし、同一の値を持つ `IDSymbol` 要素は、異なる親を持つ限り、パッケージ内に存在することができます。

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
