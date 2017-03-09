---
title: "コンパイラの警告 (レベル 3) CS0414 | Microsoft Docs"
ms.custom: ""
ms.date: "11/17/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CS0414"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0414"
ms.assetid: 6a0a80be-799b-4d9c-a7e0-6b91e9ce7be0
caps.latest.revision: 11
caps.handback.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラの警告 (レベル 3) CS0414
private フィールド 'field' は割り当てられていますが、その値が使用されていません  
  
 この警告は、コンパイラで、変数が参照されていないことを確認できるいくつかのシナリオで発生する可能性があります。  
  
-   private フィールドに定数値が割り当てられていますが、これ以降に一切読み取られていません。 不要な割り当ては、パフォーマンスに影響する可能性があります。 フィールドの削除を検討してください。  
  
-   private または内部の静的フィールドの初期化子にのみ、定数値が割り当てられています。 フィールドを const に変更することを検討してください。  
  
-   private または内部フィールドに定数値が割り当てられており、\#ifdef ディレクティブによって除外されたブロック内でのみ使用されています。 \#ifdef ブロック内にフィールドを配置することを検討してください。  
  
-   private または内部フィールドの複数の場所に定数値が割り当てられていますが、それ以外はアクセスされていません。 フィールドが不要な場合は、削除することを検討してください。 削除しない場合は、何らかの適切な方法でこのフィールドを使用します。  
  
 その他の場合、または提案されている回避策が受け入れ不可の場合は、\#pragma 0414 を使用します。  
  
 次の例では、CS0414 が生成される仕組みの 1 つを示しています。  
  
```  
// CS0414 // compile with: /W3 class C { private int i = 1;  // CS0414 public static void Main() { } }  
```  
  
 **メモ** 変数 `i` が `protected or public` として宣言されている場合、エラーは生成されません。これは、派生クラスでこの変数が使用されるのか、その他のクライアント コードによってクラスがインスタンス化され、変数が参照されるのかどうかが、コンパイラで認識できないためです。  
  
## 参照  
 [C\# Compiler Errors](/dotnet/csharp/language-reference/compiler-messages/index)   
 [C\# Compiler Options](/dotnet/csharp/language-reference/compiler-options/index)