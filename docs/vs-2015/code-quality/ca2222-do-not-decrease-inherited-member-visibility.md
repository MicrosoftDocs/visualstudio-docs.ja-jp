---
title: CA2222:継承されたメンバーの可視性を縮小しません |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDecreaseInheritedMemberVisibility
- CA2222
helpviewer_keywords:
- DoNotDecreaseInheritedMemberVisibility
- CA2222
ms.assetid: 066c8675-381f-43cc-956c-d757cc494028
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ee6228359e84687023a713ee866ebfbb760b206b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68142454"
---
# <a name="ca2222-do-not-decrease-inherited-member-visibility"></a>CA2222:継承されたメンバーの参照範囲を縮小しません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotDecreaseInheritedMemberVisibility|
|CheckId|CA2222|
|Category|Microsoft.Usage|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 封印されていない型のプライベート メソッドには、基本データ型で宣言されたパブリック メソッドと同じである署名があります。 プライベート メソッドは、最終版ではありません。

## <a name="rule-description"></a>規則の説明
 継承メンバーのアクセス修飾子は変更しないでください。 継承メンバーをプライベートに変更しても、呼び出し元はメソッドの基本クラスの実装にアクセスできます。 メンバーがプライベートにする型が封印されていない場合は、継承する型と、メソッドの最後のパブリックの実装が継承階層で呼び出すことができます。 アクセス修飾子を変更する必要があります、メソッドは、最終的なマークする必要がありますか、またはメソッドがオーバーライドされることを防ぐためにその型をシールする必要があります。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を解決するには、プライベート以外へのアクセスを変更します。 または、使用するプログラミング言語がサポートする場合行うことができます、メソッド最終的です。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="example"></a>例
 次の例では、この規則に違反する型を示します。

 [!code-csharp[FxCop.Usage.InheritedPublic#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.InheritedPublic/cs/FxCop.Usage.InheritedPublic.cs#1)]
 [!code-vb[FxCop.Usage.InheritedPublic#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.InheritedPublic/vb/FxCop.Usage.InheritedPublic.vb#1)]
