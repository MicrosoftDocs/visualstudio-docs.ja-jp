---
title: CA2004:GC への呼び出しを削除します。KeepAlive |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
helpviewer_keywords:
- RemoveCallsToGCKeepAlive
- CA2004
ms.assetid: bc543b5b-23eb-4b45-abc2-9325cd254ac2
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: e75ab22212945e5a6b4465e1e1f64ca48a9daa4a
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58973531"
---
# <a name="ca2004-remove-calls-to-gckeepalive"></a>CA2004:GC.KeepAlive への呼び出しを削除します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|RemoveCallsToGCKeepAlive|
|CheckId|CA2004|
|カテゴリ|Microsoft.Reliability|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 クラスの使用`SafeHandle`への呼び出しがまだ含まれているが`GC.KeepAlive`します。

## <a name="rule-description"></a>規則の説明
 変換する場合`SafeHandle`使用状況、呼び出しをすべて削除`GC.KeepAlive`(オブジェクト)。 この場合は、クラス必要はありませんを呼び出す`GC.KeepAlive`、ファイナライザーはありませんが、依存するいると仮定すると`SafeHandle`して OS ハンドルを完了します。  呼び出しで保持するためのコスト`GC.KeepAlive`ごくわずかであり、パフォーマンスの認識によって測定される場合がありますがへの呼び出し`GC.KeepAlive`必要であるか、または有効期間がコードになりますが困難になりますが、存在しなくなった問題を解決するためには維持します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 呼び出しを削除`GC.KeepAlive`します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 変換する技術的には位置が正しくない場合にのみ、この警告を抑制できます`SafeHandle`クラスで使用します。
