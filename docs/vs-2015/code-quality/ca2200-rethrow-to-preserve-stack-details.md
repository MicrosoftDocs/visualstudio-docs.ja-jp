---
title: 'CA2200: スタックの詳細を保持するための再スロー |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- RethrowToPreserveStackDetails
- CA2200
helpviewer_keywords:
- CA2200
- RethrowToPreserveStackDetails
ms.assetid: 046e1b98-c4dc-4515-874f-9c0de2285621
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d20407d7cc708ac785e4a792bf8e64768ea58540
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667385"
---
# <a name="ca2200-rethrow-to-preserve-stack-details"></a>CA2200: スタック詳細を保持するために再度スローします
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|RethrowToPreserveStackDetails|
|CheckId|CA2200|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 例外が再スローされ、`throw` ステートメントで例外が明示的に指定されます。

## <a name="rule-description"></a>規則の説明
 例外がスローされると、それに含まれる情報の一部がスタックトレースになります。 スタックトレースは、例外をスローするメソッドで始まり、例外をキャッチするメソッドで終了するメソッド呼び出し階層のリストです。 @No__t_0 ステートメントで例外を指定して例外が再スローされた場合、現在のメソッドでスタックトレースが再開され、例外をスローした元のメソッドと現在のメソッドとの間のメソッド呼び出しのリストが失われます。 例外と共に元のスタックトレース情報を保持するには、例外を指定せずに `throw` ステートメントを使用します。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、例外を明示的に指定せずに例外を再スローします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例は、規則に違反する `CatchAndRethrowExplicitly` というメソッドを示しています。このメソッドは、規則を満たす `CatchAndRethrowImplicitly` です。

 [!code-csharp[FxCop.Usage.Rethrow#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.Rethrow/cs/FxCop.Usage.Rethrow.cs#1)]
 [!code-vb[FxCop.Usage.Rethrow#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.Rethrow/vb/FxCop.Usage.Rethrow.vb#1)]
