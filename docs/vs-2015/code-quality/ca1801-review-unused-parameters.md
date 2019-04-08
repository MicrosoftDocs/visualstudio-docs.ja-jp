---
title: CA1801:未使用のパラメーターの確認 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUnusedParameters
- CA1801
- ReviewUnusedParameters
helpviewer_keywords:
- CA1801
- ReviewUnusedParameters
ms.assetid: 5d73545c-e153-4b7c-a7b2-be6bf5aca5be
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: d1a3b0c7672af9cf10804c84db5103a93ff3ad80
ms.sourcegitcommit: 3201da3499051768ab59f492699a9049cbc5c3c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2019
ms.locfileid: "59003071"
---
# <a name="ca1801-review-unused-parameters"></a>CA1801:使用されていないパラメーターの確認
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新ドキュメントについては、次を参照してください。 [ca 1801。未使用のパラメーターをレビュー](https://docs.microsoft.com/visualstudio/code-quality/ca1801-review-unused-parameters) docs.microsoft.com でリリースされました。  
  
|||  
|-|-|  
|TypeName|ReviewUnusedParameters|  
|CheckId|CA1801|  
|カテゴリ|Microsoft.Usage|  
|互換性に影響する変更点|なし - メンバーが行った変更に関係なく、アセンブリの外部に表示されない場合<br /><br /> なし - の本体にあるパラメーターを使用するメンバーを変更する場合<br /><br /> あり - パラメーターを削除して、アセンブリの外側に表示される場合。|  
  
## <a name="cause"></a>原因  
 メソッドのシグネチャに、メソッドの本体で使用されていないパラメーターがあります。 このルールは、次の方法を確認できません。  
  
-   デリゲートによって参照されるメソッド。  
  
-   イベント ハンドラーとして使用されるメソッド。  
  
-   宣言されたメソッド、 `abstract` (`MustOverride` Visual Basic) 修飾子。  
  
-   宣言されたメソッド、 `virtual` (`Overridable` Visual Basic) 修飾子。  
  
-   宣言されたメソッド、 `override` (`Overrides` Visual Basic) 修飾子。  
  
-   宣言されたメソッド、 `extern` (`Declare` Visual Basic でのステートメント) 修飾子。  
  
## <a name="rule-description"></a>規則の説明  
 それらにアクセスする障害が回避の正確性が存在しないかどうかを確認するメソッドの本体で使用されていない非仮想メソッドのパラメーターを確認します。 使用されていないパラメーターには、メンテナンスとパフォーマンスのコストが発生します。  
  
 この規則違反は、メソッドの実装に関するバグをポイントできます。 たとえば、パラメーターがメソッドの本体で使用されているがする必要があります。 パラメーターに旧バージョンと互換性のために存在する場合は、この規則の警告を抑制します。  
  
## <a name="how-to-fix-violations"></a>違反の修正方法  
 このルールの違反を修正するには、未使用のパラメーター (重大な変更) を削除またはメソッドの本体 (互換性に影響しない変更) で、パラメーターを使用します。  
  
## <a name="when-to-suppress-warnings"></a>警告を抑制する状況  
 以前にリリース済みのコード修正が重大な変更をすると、この規則からの警告を抑制しても安全です。  
  
## <a name="example"></a>例  
 次の例では、2 つの方法を示します。 1 つのメソッドには、ルールに違反しているし、他のメソッドは、ルールを満たします。  
  
 [!code-csharp[FxCop.Usage.ReviewUnusedParameters#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ReviewUnusedParameters/cs/FxCop.Usage.ReviewUnusedPerameters.cs#1)]  
  
## <a name="related-rules"></a>関連規則  
 [CA1811:呼び出されていないプライベート コードを避ける](../code-quality/ca1811-avoid-uncalled-private-code.md)  
  
 [CA1812:インスタンス化されていない内部クラスを回避します。](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)  
  
 [CA 1804:使用されていないローカルを削除します](../code-quality/ca1804-remove-unused-locals.md)
