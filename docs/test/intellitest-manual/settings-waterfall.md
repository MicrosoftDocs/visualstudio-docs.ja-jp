---
title: 設定ウォーターフォール | Microsoft IntelliTest 開発者テスト ツール
description: アセンブリ、フィクスチャ、および探索レベルで設定を整理する設定ウォーターフォールについて説明します。
ms.custom: SEO-VS-2020
ms.date: 05/02/2017
ms.topic: conceptual
helpviewer_keywords:
- IntelliTest, Settings waterfall
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 283cb7b4a485389fa19e3756e79c35f1cec1041a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99920495"
---
# <a name="settings-waterfall"></a>設定ウォーターフォール

設定ウォーターフォールの概念とは、ユーザーが **アセンブリ**、**フィクスチャ**、**探索** レベルで設定を指定できることを意味します。

* アセンブリ - [PexAssemblySettings](attribute-glossary.md#pexassemblysettings)
* フィクスチャ - [PexClass](attribute-glossary.md#pexclass)
* 探索 - [PexExplorationAttributeBase](attribute-glossary.md#pexexplorationattributebase)

**アセンブリ** レベルで指定された設定は、そのアセンブリの下にあるすべてのフィクスチャと探索に影響を与えます。 **フィクスチャ** レベルで指定された設定は、そのフィクスチャの下にあるすべての探索に影響を与えます。 子設定 win &mdash; 設定が **アセンブリ** レベルと **フィクスチャ** レベルで定義されている場合、**フィクスチャ** 設定が使用されます。

一部の設定は **アセンブリ** レベルまたは **フィクスチャ** レベルに固有となります。

**例**

```csharp
using Microsoft.Pex.Framework;

[assembly: PexAssemblySettings(MaxBranches = 1000)] // we override the default value of maxbranches

namespace MyTests
{
    [PexClass(MaxBranches = 500)] // we override the 1000 value and set maxbranches to 500
    public partial class MyTests
    {
        [PexMethod(MaxBranches = 100)] // we override again, maxbranches = 100
        public void MyTest(...) { ... }
    }
}
```

## <a name="got-feedback"></a>フィードバックが欲しい場合

ご意見や機能に関するご要望を[開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)で投稿してください。
