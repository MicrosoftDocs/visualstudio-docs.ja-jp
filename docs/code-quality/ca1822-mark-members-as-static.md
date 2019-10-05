---
title: CA1822:メンバーを static に設定します
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MarkMembersAsStatic
- CA1822
helpviewer_keywords:
- MarkMembersAsStatic
- CA1822
ms.assetid: 743f0af7-41d1-4852-8d97-af0688b31118
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7ebbbbe01f1dd23dfc560e019133dacd3517b388
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71253460"
---
# <a name="ca1822-mark-members-as-static"></a>CA1822:メンバーを static に設定します

|||
|-|-|
|TypeName|MarkMembersAsStatic|
|CheckId|CA1822|
|カテゴリ|Microsoft.Performance|
|互換性に影響する変更点|非重大-変更に関係なく、メンバーがアセンブリの外部で参照できない場合。 非互換性- `this`キーワードを使用してメンバーをインスタンスメンバーに変更するだけです。<br /><br /> 中断-メンバーをインスタンスメンバーから静的メンバーに変更し、アセンブリの外部から参照できる場合。|

## <a name="cause"></a>原因
インスタンスデータにアクセスしないメンバーは、static (では[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]Shared) とマークされていません。

## <a name="rule-description"></a>規則の説明
インスタンス データにアクセスしない、またはインスタンス メソッドを呼び出さないメンバーは、静的 ([!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] では共有) としてマークできます。 メソッドを静的としてマークすると、コンパイラはこれらのメンバーに対する非仮想呼び出しサイトを出力します。 非仮想呼び出しサイトを出力すると、現在のオブジェクトポインターが null でないことを確認する呼び出しごとに、実行時にチェックが行われなくなります。 これにより、パフォーマンスを重視するコードに対して、測定可能なパフォーマンスの向上を実現できます。 場合によっては、現在のオブジェクトインスタンスにアクセスできなかった場合、正確性の問題が発生することがあります。

## <a name="how-to-fix-violations"></a>違反の修正方法
メンバーを静的 (またはで[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]共有) としてマークするか、メソッド本体で ' this '/' Me ' を使用します (該当する場合)。

## <a name="when-to-suppress-warnings"></a>警告を非表示にする場合
以前に出荷されたコードについては、この修正プログラムが互換性に影響する変更になるという警告を抑制するのは安全です。

## <a name="related-rules"></a>関連するルール
[CA1811呼び出されるプライベートコードを避ける](../code-quality/ca1811-avoid-uncalled-private-code.md)

[CA1812インスタンス内部クラスを回避する](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

[CA1804未使用のローカルの削除](../code-quality/ca1804-remove-unused-locals.md)