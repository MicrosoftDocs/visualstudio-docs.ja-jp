---
title: '&lt;Schedules&gt; 要素 (ブートストラップ) |Microsoft Docs'
description: Schedules 要素には、Command 要素で定義されたコマンドを実行する特定の時刻を定義する Schedule 要素が含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <Schedules> element [bootstrapper]
ms.assetid: 28d094cf-64f5-42b1-bd8a-3697082aab4f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0154816985076373c3ced4981aa714971a9ded29
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99949650"
---
# <a name="ltschedulesgt-element-bootstrapper"></a>&lt;Schedules &gt; 要素 (ブートストラップ)
`Schedules` 要素には、`Command` 要素で定義されたコマンドを実行する特定の時刻を定義する `Schedule` 要素が含まれます。

## <a name="syntax"></a>構文

```xml
<Schedules>
    <Schedule
        Name
    >
        <BuildList />
        <BeforePackage />
        <AfterPackage />
    </Schedule>
</Schedules>
```

## <a name="elements-and-attributes"></a>要素と属性
 `Schedules` 要素は、`Product` 要素の子です。 各 `Product` 要素には、最大で 1 つの `Schedules` 要素が含まれます。 `Schedules` 要素に属性はありません。

## <a name="schedule"></a>スケジュール
 `Schedule` 要素は、`Schedules` 要素の子です。 `Schedules` 要素には `Schedule` 要素が少なくとも 1 つ必要です。

 `Schedule` には、以下の属性があります。

|属性|説明|
|---------------|-----------------|
|`Name`|必須。 スケジュール項目の名前。 これは、`Command` 要素の `ScheduleName` プロパティに対応します。 `Command` が指定されたスケジュールを参照する場合、`Schedule` 要素によって示される時刻にのみ実行されます。 スケジュールは、`FailIf` および `BypassIf` 要素と関連付けることもできます。これにより、これらの条件付きのテストは指定されたスケジュールで実行するように制限されます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|

 特定の `Schedule` 要素には、次の子のいずれかのみを含めることができます。

## <a name="buildlist"></a>BuildList
 `BuildList` 要素は、ブートストラップ アプリケーションが起動された直後にコマンドを実行するようインストーラーに指示します。

## <a name="beforepackage"></a>BeforePackage
 `BeforePackage` 要素は、指定されたパッケージがインストールされる前にコマンドを実行するようインストーラーに指示します。

## <a name="afterpackage"></a>AfterPackage
 `AfterPackage` 要素は、指定されたパッケージがインストールされた後にコマンドを実行するようインストーラーに指示します。

## <a name="see-also"></a>関連項目
- [\<Product> 要素](../deployment/product-element-bootstrapper.md)
- [製品およびパッケージ スキーマ リファレンス](../deployment/product-and-package-schema-reference.md)