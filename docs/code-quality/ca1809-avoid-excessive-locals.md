---
title: CA1809:ローカルを使用しすぎないでください
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1809
- AvoidExcessiveLocals
helpviewer_keywords:
- AvoidExcessiveLocals
- CA1809
ms.assetid: 5c81ea43-cb49-448f-980f-a1dd9764043c
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f4ac6947f8424c3b9aa7429ee378b4bb89be73ca
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62545242"
---
# <a name="ca1809-avoid-excessive-locals"></a>CA1809:ローカルを使用しすぎないでください

|||
|-|-|
|TypeName|AvoidExcessiveLocals|
|CheckId|CA1809|
|カテゴリ|Microsoft.Performance|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メンバーには、64 を超えるローカル変数、一部のコンパイラによって生成された可能性がありますが含まれています。

## <a name="rule-description"></a>規則の説明
 一般的なパフォーマンスの最適化と呼ばれるメモリ内の代わりにプロセッサのレジスタに値を格納する、*レジスタ格納*値。 共通言語ランタイムでは、最大 64 個のローカル変数の enregistration と見なします。 レジスタではない変数をスタックに配置され、操作する前に、レジスタに移動する必要があります。 可能性を許可するすべてのローカル変数がレジスタ格納、64 をローカル変数の数を制限します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、64 個のローカル変数を使用する実装をリファクタリングします。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。
 パフォーマンスに問題がない場合、この規則による警告を抑制するか、ルールを無効にするには安全です。

## <a name="related-rules"></a>関連するルール
 [CA 1804:使用されていないローカルを削除します](../code-quality/ca1804-remove-unused-locals.md)