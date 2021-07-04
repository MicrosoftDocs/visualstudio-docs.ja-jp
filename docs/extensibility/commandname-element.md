---
title: CommandName 要素 | Microsoft Docs
description: CommandName 要素では、[オプション] ダイアログ ボックスのキーボード カテゴリ、および [ユーザー設定] ダイアログ ボックスの [コマンド] 一覧に表示されるテキストを指定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- CommandName element (VSCT XML schema)
- VSCT XML schema elements, CommandName
ms.assetid: a338b767-aa7e-4536-9908-e19a50ab60ac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 193e97880fbc543568636e1979a847877e42db14
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902008"
---
# <a name="commandname-element"></a>CommandName 要素
`CommandName` 要素では、 **[オプション]** ダイアログ ボックスのキーボード カテゴリ、および **[ユーザー設定]** ダイアログ ボックスの **[コマンド]** 一覧に表示されるテキストを指定します。

## <a name="syntax"></a>構文

```
<CommandName>MyCommand</CommandName>
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
|[Strings 要素](../extensibility/strings-element.md)|`ButtonText` や `CommandName` などのテキスト要素をグループ化します。|

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
