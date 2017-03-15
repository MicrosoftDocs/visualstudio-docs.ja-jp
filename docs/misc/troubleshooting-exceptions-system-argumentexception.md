---
title: "例外のトラブルシューティング : System.ArgumentException | Microsoft Docs"
ms.custom: ""
ms.date: "10/29/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ArgumentException 例外"
  - "System.ArgumentException 例外"
ms.assetid: d8052e62-bc73-4828-87e9-a84ef2a39a5b
caps.latest.revision: 14
caps.handback.revision: 14
author: "mikeblome"
ms.author: "mblome"
manager: "douge"
---
# 例外のトラブルシューティング : System.ArgumentException
<xref:System.ArgumentException> 例外は、メソッドに渡された引数の少なくとも 1 つが、メソッドのパラメーターの仕様に一致していない場合にスローされます。  
  
 次の例では、`DivideByTwo` メソッドに送信された引数が偶数ではない場合に例外がスローされます。  
  
```vb#  
Module Module1 Sub Main() ' ArgumentException is not thrown in DivideByTwo because 10 is ' an even number. Console.WriteLine("10 divided by 2 is {0}", DivideByTwo(10)) Try ' ArgumentException is thrown in DivideByTwo because 7 is ' not an even number. Console.WriteLine("7 divided by 2 is {0}", DivideByTwo(7)) Catch argEx As ArgumentException ' Tell the user which problem is encountered. Console.WriteLine("7 cannot be evenly divided by 2.") Console.WriteLine("Exception message: " & argEx.Message) End Try ' Uncomment the next statement to see what happens if you call ' DivideByTwo directly. 'Console.WriteLine(DivideByTwo(7)) End Sub Function DivideByTwo(ByVal num As Integer) As Integer ' If num is an odd number, throw an ArgumentException. The ' ArgumentException class provides a number of constructors ' that you can choose from. If num Mod 2 = 1 Then Throw New ArgumentException("Argument for num must be" & _ " an even number.") End If ' Value of num is even, so return half of its value. Return num / 2 End Function End Module  
```  
  
 `ArgumentException` クラスのすべてのインスタンスには、無効な引数と値の許容範囲を指定する情報が含まれる必要があります。 より正確な例外 \(<xref:System.ArgumentNullException> や <xref:System.ArgumentOutOfRangeException> など\) で状況が正確に示される場合は、`ArgumentException` ではなくこれを使用する必要があります。  
  
 この例外の詳細 \(他の言語の例を含む\) については、「<xref:System.ArgumentException>」を参照してください。 その他のコンストラクターの一覧については、「<xref:System.ArgumentException.%23ctor%2A>」を参照してください。  
  
## 参照  
 <xref:System.ArgumentException>   
 [Use the Exception Assistant](../Topic/How%20to:%20Use%20the%20Exception%20Assistant.md)