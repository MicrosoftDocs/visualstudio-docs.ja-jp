---
title: CA1715:識別子は正しいプレフィックスを含むこと |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1715
- IdentifiersShouldHaveCorrectPrefix
helpviewer_keywords:
- IdentifiersShouldHaveCorrectPrefix
- CA1715
ms.assetid: cf45f8df-6855-4cb6-a4e2-7cfed714cf2f
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 37c8193a166849f1361a66c640b1a414d3900fca
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59667327"
---
# <a name="ca1715-identifiers-should-have-correct-prefix"></a>CA1715:識別子は正しいプレフィックスを含んでいなければなりません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新ドキュメントについては、次を参照してください[CA1715:。識別子は正しいプレフィックスを含むこと](https://docs.microsoft.com/visualstudio/code-quality/ca1715-identifiers-should-have-correct-prefix)します。  
  
|||  
|-|-|  
|TypeName|IdentifiersShouldHaveCorrectPrefix|  
|CheckId|CA1715|  
|Category|Microsoft.Naming|  
|互換性に影響する変更点|– インターフェイスで発生した場合。<br /><br /> 改行のジェネリック型パラメーターで発生したときにします。|  
  
## <a name="cause"></a>原因  
 外部から参照できるインターフェイスの名前の先頭が大文字の 'I' でありません。  
  
 - または -  
  
 外部から参照できる型またはメソッドのジェネリック型パラメーターの名前値で始まらない大文字 ' T '。  
  
## <a name="rule-description"></a>規則の説明  
 慣例により、特定のプログラミング要素の名前は固有のプレフィックスで開始します。  
  
 インターフェイス名は、大文字、もう 1 つの大文字が続く 'I' で始める必要があります。 このルールは、'MyInterface' や 'IsolatedInterface' などのインターフェイス名の違反を報告します。  
  
 ジェネリック型パラメーターの名前が大文字で始まる、' T ' 必要に応じて、もう 1 つの大文字が続く可能性があります。 このルールは、'V' と 'Type' などのジェネリック型パラメーターの名前の違反を報告します。  
  
 名前付け規則では、共通言語ランタイムをターゲットとするライブラリの統一的な名前の付け方が規定されています。 これにより、新しいソフトウェア ライブラリを習得するまでの時間を短縮でき、マネージド コード開発の専門家によってライブラリが開発されたという信頼を顧客に与えることができます。  
  
## <a name="how-to-fix-violations"></a>違反の修正方法  
 識別子の名前を変更して、プレフィックスが正しくようにします。  
  
## <a name="when-to-suppress-warnings"></a>警告を抑制する状況  
 この規則による警告は抑制しないでください。  
  
## <a name="example"></a>例  
 **次の例では、不適切な名前のインターフェイスを示します。**  
  
 [!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix/cpp/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix.cpp#1)]
 [!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix/cs/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix.cs#1)]
 [!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix/vb/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix.vb#1)]  
  
## <a name="example"></a>例  
 **次の例では、'I' とインターフェイスを付けることで以前の違反を修正します。**  
  
 [!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2/cpp/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2.cpp#1)]
 [!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2/cs/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2.cs#1)]
 [!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2/vb/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2.vb#1)]  
  
## <a name="example"></a>例  
 **次の例は、不適切な名前のジェネリック型パラメーターを示します。**  
  
 [!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3/cpp/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3.cpp#1)]
 [!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3/cs/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3.cs#1)]
 [!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3/vb/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3.vb#1)]  
  
## <a name="example"></a>例  
 **次の例では、' T のジェネリック型パラメーターを付けることで、前の違反を修正する '。**  
  
 [!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4/cpp/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4.cpp#1)]
 [!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4/cs/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4.cs#1)]
 [!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4/vb/FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4.vb#1)]  
  
## <a name="related-rules"></a>関連規則  
 [CA1722:識別子には、不適切なプレフィックスはありません。](../code-quality/ca1722-identifiers-should-not-have-incorrect-prefix.md)
