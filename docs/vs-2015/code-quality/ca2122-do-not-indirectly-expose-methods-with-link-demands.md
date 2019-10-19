---
title: 'CA2122: リンク確認要求を使用して間接的にメソッドを公開しません |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2122
- DoNotIndirectlyExposeMethodsWithLinkDemands
helpviewer_keywords:
- DoNotIndirectlyExposeMethodsWithLinkDemands
- CA2122
ms.assetid: 3eda58e7-c6ec-41c3-8112-ae0841109c6a
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 099e5f3f9a09eef57ce1b888601f61e85ceb97c5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72643403"
---
# <a name="ca2122-do-not-indirectly-expose-methods-with-link-demands"></a>CA2122: リンク確認要求で間接的にメソッドを公開しないでください
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotIndirectlyExposeMethodsWithLinkDemands|
|CheckId|CA2122|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 パブリックメンバーまたはプロテクトメンバーに[リンク確認要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)があり、セキュリティチェックを実行しないメンバーによって呼び出されています。

## <a name="rule-description"></a>規則の説明
 リンク確認要求では、直接の呼び出し元のアクセス許可しかチェックされません。 メンバー `X` が呼び出し元に対してセキュリティ要求を行わず、リンク確認要求によって保護されたコードを呼び出す場合、必要なアクセス許可を持たない呼び出し元は、`X` を使用して保護されたメンバーにアクセスできます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 セキュリティ[データとモデリング](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)またはリンク確認要求をメンバーに追加して、リンク確認要求で保護されたメンバーに安全にアクセスできないようにします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則からの警告を安全に抑制するには、破壊的な方法で使用できる操作またはリソースへの呼び出し元に対して、コードがアクセス権を付与しないようにする必要があります。

## <a name="example"></a>例
 次の例は、規則に違反するライブラリと、ライブラリの弱点を示すアプリケーションを示しています。 サンプルライブラリには、規則に違反する2つのメソッドが用意されています。 @No__t_0 メソッドは、環境変数に無制限にアクセスするためのリンク確認要求によって保護されます。 @No__t_0 メソッドは、`EnvironmentSetting` を呼び出す前に、その呼び出し元に対してセキュリティ要求を行いません。

 [!code-csharp[FxCop.Security.UnsecuredDoNotCall#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.UnsecuredDoNotCall/cs/FxCop.Security.UnsecuredDoNotCall.cs#1)]

## <a name="example"></a>例
 次のアプリケーションは、セキュリティで保護されていないライブラリメンバーを呼び出します。

 [!code-csharp[FxCop.Security.TestUnsecuredDoNot1#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestUnsecuredDoNot1/cs/FxCop.Security.TestUnsecuredDoNot1.cs#1)]

 この例を実行すると、次の出力が生成されます。

 **セキュリティで保護されていないメンバーからの値: seattle.corp.contoso.com**
## <a name="see-also"></a>参照
 [安全なコーディングのガイドライン](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)[リンク要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)[のデータとモデリング](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6)
