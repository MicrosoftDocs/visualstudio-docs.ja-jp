---
title: CA2004:GC.KeepAlive への呼び出しを削除します
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
helpviewer_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
ms.assetid: bc543b5b-23eb-4b45-abc2-9325cd254ac2
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a716da8eb0fb1b741c302ed32408e63a4933567b
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921132"
---
# <a name="ca2004-remove-calls-to-gckeepalive"></a>CA2004:GC.KeepAlive への呼び出しを削除します

|||
|-|-|
|TypeName|RemoveCallsToGCKeepAlive|
|CheckId|CA2004|
|Category|Microsoft.Reliability|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
クラスは`SafeHandle`を使用しますが`GC.KeepAlive`、の呼び出しは引き続き含まれます。

## <a name="rule-description"></a>規則の説明
使用法に`SafeHandle`変換する場合は、(object) `GC.KeepAlive`へのすべての呼び出しを削除します。 この場合、クラスは、ファイナライザーを持たない`GC.KeepAlive`ものの、OS ハンドルを完了`SafeHandle`するために依存していることを前提として、を呼び出す必要はありません。  を呼び出したままにする`GC.KeepAlive`と、パフォーマンスによって測定されるのではなく、の`GC.KeepAlive`呼び出しが必要か、または存在しなくなった可能性のある有効期間の問題を解決するのに十分であるという認識は、コードがより困難になります。保存.

## <a name="how-to-fix-violations"></a>違反の修正方法
の呼び出しを`GC.KeepAlive`削除します。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
この警告を非表示にすることができるのは、クラスの`SafeHandle`使用法への変換が技術的に適切でない場合のみです。