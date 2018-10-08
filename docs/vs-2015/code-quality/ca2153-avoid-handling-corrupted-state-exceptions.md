---
title: 'Ca 2153: 破損状態例外の処理を避けるため |Microsoft Docs'
ms.custom: ''
ms.date: 2018-06-30
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 418cc9cb-68ad-47e9-a6c8-a48b9c35db45
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ff16046a115a7a21939ef33fa06f6a81ec56921c
ms.sourcegitcommit: 99d097d82ee4f9eff6f588e5ebb6b17d8f724b04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "47591950"
---
# <a name="ca2153-avoid-handling-corrupted-state-exceptions"></a>CA2153: 破損状態例外の処理を回避する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[ca 2153: 回避破損状態例外を処理](https://docs.microsoft.com/visualstudio/code-quality/ca2153-avoid-handling-corrupted-state-exceptions)します。

|||
|-|-|
|TypeName|AvoidHandlingCorruptedStateExceptions|
|CheckId|CA2153|
|カテゴリ|Microsoft.Security|
|互換性に影響する変更点|中断なし|

## <a name="cause"></a>原因
 [破損状態例外 (CSE)](https://msdn.microsoft.com/magazine/dd419661.aspx)そのメモリ破損がプロセス内に存在します。 プロセスをクラッシュさせるのではなくこれらの例外をキャッチすることは、攻撃者が破損したメモリ領域にセキュリティ上の弱点を見出すことができた場合に、セキュリティ上の脆弱性となる可能性があります。

## <a name="rule-description"></a>規則の説明
 CSE は、プロセスが破損状態にあり、システムによってキャッチされていないことを示します。 破損した状態のシナリオでは、適切な `HandleProcessCorruptedStateExceptions` 属性でメソッドをマークした場合に、汎用ハンドラーのみがこの例外をキャッチします。 既定で、[共通言語ランタイム (CLR)](https://msdn.microsoft.com/library/8bs2ecf4.aspx) Cse の catch ハンドラーは呼び出されません。

 コードをログに記録しても攻撃者はメモリ破損のバグを悪用できるため、このような例外をキャッチせずにプロセスをクラッシュさせるほうが安全な方法です。

 catch(exception) や catch(no exception specification) などすべての例外をキャッチする汎用ハンドラーを使用して CSE をキャッチすると、この警告がトリガーされます。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この警告を解決するには、次のいずれかを行う必要があります。

 1. 削除、`HandleProcessCorruptedStateExceptions`属性。 これにより、CSE を catch ハンドラーに渡さない既定の実行時の動作に戻ります。

 2. 特定の例外の種類をキャッチするハンドラーではなく汎用 catch ハンドラーを削除します。  ハンドラー コードが安全に処理できたと仮定した場合 (非常にまれ)、これに CSE が含まれることがあります。

 3. 例外が呼び出し元に渡され、実行中のプロセスを終了させる catch ハンドラーで CSE を再スローします。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 この規則による警告は抑制しないでください。

## <a name="pseudo-code-example"></a>擬似コードの例

### <a name="violation"></a>違反
 次の擬似コードでは、このルールにより検出されたパターンを示しています。

```
[HandleProcessCorruptedStateExceptions]
//method to handle and log CSE exceptions
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (Exception e)
    {
        // Handle error
    }
}
```

### <a name="solution-1"></a>解決方法 1
 HandleProcessCorruptedExceptions 属性を削除することにより、例外が処理されないようにします。

```
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (IOException e)
    {
        // Handle error
    }
    catch (UnauthorizedAccessException e)
    {
        // Handle error
    }
}
```

### <a name="solution-2"></a>解決方法 2
 汎用 catch ハンドラーを削除し、特定の例外の種類のみをキャッチします。

```
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (IOException e)
    {
        // Handle error
    }
    catch (UnauthorizedAccessException e)
    {
        // Handle error
    }
}
```

### <a name="solution-3"></a>解決方法 3
 例外を再スローします。

```
void TestMethod1()
{
    try
    {
        FileStream fileStream = new FileStream("name", FileMode.Create);
    }
    catch (Exception e)
    {
        // Handle error
        throw;
    }
}
```



