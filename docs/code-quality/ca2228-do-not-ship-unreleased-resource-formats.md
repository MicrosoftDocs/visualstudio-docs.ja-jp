---
title: CA2228:未公開のリソース形式を出荷しません
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DoNotShipUnreleasedResourceFormats
- CA2228
helpviewer_keywords:
- CA2228
- DoNotShipUnreleasedResourceFormats
ms.assetid: 2c614edc-4e94-4b4f-8067-eea677a75cd9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4355db8b15a3869e785589170bec3f80e8f08fbb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62541719"
---
# <a name="ca2228-do-not-ship-unreleased-resource-formats"></a>CA2228:未公開のリソース形式を出荷しません

|||
|-|-|
|TypeName|DoNotShipUnreleasedResourceFormats|
|CheckId|CA2228|
|カテゴリ|Microsoft.Usage|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 リソース ファイルは、現在サポートされていない .NET Framework のバージョンを使用して構築されました。

## <a name="rule-description"></a>規則の説明
 .NET Framework のプレリリース バージョンを使用してビルドされたリソース ファイルは、サポートされているバージョンの .NET Framework で使用できるしない場合があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、サポートされているバージョンの .NET Framework を使用して、リソースをビルドします。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。
 この規則による警告は抑制しないでください。
