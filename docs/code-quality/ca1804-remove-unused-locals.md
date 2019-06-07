---
title: CA1804:使用されていないローカルを削除します
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1804
- RemoveUnusedLocals
helpviewer_keywords:
- RemoveUnusedLocals
- CA1804
ms.assetid: cc332e67-6543-4813-bd8a-6f6fc75bf22a
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: c94f1b2709f3541692a0dfcd2a92559135639c2a
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66744586"
---
# <a name="ca1804-remove-unused-locals"></a>CA1804:使用されていないローカルを削除します

|||
|-|-|
|TypeName|RemoveUnusedLocals|
|CheckId|CA1804|
|カテゴリ|Microsoft.Performance|
|互換性に影響する変更点|なし|

## <a name="cause"></a>原因
 メソッドでローカル変数を宣言も使わないを除く変数可能性があります、代入ステートメントの受信者として。 このルールによって、分析するためには、デバッグ情報のテスト対象のアセンブリをビルドする必要があり、関連付けられているプログラム データベース (.pdb) ファイルは、使用可能なである必要があります。

## <a name="rule-description"></a>規則の説明
 使用されていないローカル変数や不要な引数があると、アセンブリのサイズが大きくなり、パフォーマンスが低下します。

## <a name="how-to-fix-violations"></a>違反の修正方法

この規則違反を修正するには、削除するか、ローカル変数を使用します。

> [!NOTE]
> C#コンパイラは、未使用のローカル変数を削除します。 ときに、`optimize`オプションを有効にします。

## <a name="when-to-suppress-warnings"></a>警告を抑制します。
 変数がコンパイラで生成された場合は、この規則による警告を抑制します。 パフォーマンスとコードのメンテナンスが主な懸念事項ではない場合にも、この規則による警告を抑制するか、ルールを無効にするには安全です。

## <a name="example"></a>例
 次の例では、未使用のローカル変数をいくつかを示します。

 [!code-vb[FxCop.Performance.UnusedLocals#1](../code-quality/codesnippet/VisualBasic/ca1804-remove-unused-locals_1.vb)]
 [!code-csharp[FxCop.Performance.UnusedLocals#1](../code-quality/codesnippet/CSharp/ca1804-remove-unused-locals_1.cs)]

## <a name="related-rules"></a>関連するルール
 [CA1809:過剰なローカルします。](../code-quality/ca1809-avoid-excessive-locals.md)

 [CA1811:呼び出されていないプライベート コードを避ける](../code-quality/ca1811-avoid-uncalled-private-code.md)

 [CA1812:インスタンス化されていない内部クラスを回避します。](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA 1801:未使用のパラメーターをレビューします](../code-quality/ca1801-review-unused-parameters.md)