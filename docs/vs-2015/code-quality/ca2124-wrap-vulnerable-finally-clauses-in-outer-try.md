---
title: CA2124:ラップの脆弱性のある finally 句の外側を try |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2124
- WrapVulnerableFinallyClausesInOuterTry
helpviewer_keywords:
- CA2124
- WrapVulnerableFinallyClausesInOuterTry
ms.assetid: 82efd224-9e60-4b88-a0f5-dfabcc49a254
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 1eb503e9f5a9251cb9a348d29c7cd9636389a080
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58975870"
---
# <a name="ca2124-wrap-vulnerable-finally-clauses-in-outer-try"></a>CA2124:脆弱性のある finally 句を外側の try でラップします
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|WrapVulnerableFinallyClausesInOuterTry|
|CheckId|CA2124|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 バージョン 1.0 および 1.1 では、 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]、public または protected のメソッドが含まれています、 `try` / `catch` / `finally`ブロックします。 `finally`ブロックをセキュリティの状態をリセットしてで囲まれていない、`finally`ブロックします。

## <a name="rule-description"></a>規則の説明
 このルールでは検索`try` / `finally`バージョン 1.0 および 1.1 を対象とするコードのブロック、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]呼び出し履歴に存在する悪意のある例外フィルターを受ける可能性があります。 偽装などの機密情報の操作が、try ブロックで発生して、例外がスローされた、フィルターが実行する前に、`finally`ブロックします。 権限借用の使用例、フィルターが権限を借用したユーザーとして実行されていることを意味します。 フィルターは、現在、Visual Basic でのみ実装できます。

> [!WARNING]
>  **注**2.0 以降のバージョンでは、 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]、ランタイムが自動的に保護を`try` / `catch` /  `finally`リセットが発生した場合、悪意のある例外フィルターからブロックメソッド内で直接には、例外ブロックが含まれています。

## <a name="how-to-fix-violations"></a>違反の修正方法
 配置、ラップされていない`try` / `finally` try ブロックの外側でします。 次の 2 つ目の例を参照してください。 これにより、`finally`フィルター コードの前に実行します。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="pseudo-code-example"></a>擬似コードの例

### <a name="description"></a>説明
 次の擬似コードでは、このルールにより検出されたパターンを示しています。

### <a name="code"></a>コード

```
try {
   // Do some work.
   Impersonator imp = new Impersonator("John Doe");
   imp.AddToCreditCardBalance(100);
}
finally {
   // Reset security state.
   imp.Revert();
}
```

## <a name="example"></a>例
 次の擬似コードでは、コードを保護して、このルールを満たすために使用できるパターンを示します。

```
try {
     try {
        // Do some work.
     }
     finally {
        // Reset security state.
     }
}
catch()
{
    throw;
}
```
