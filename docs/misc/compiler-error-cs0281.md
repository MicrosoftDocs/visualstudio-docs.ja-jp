---
title: "コンパイラ エラー CS0281 | Microsoft Docs"
ms.custom: ""
ms.date: "11/16/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "CS0281"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "CS0281"
ms.assetid: 3b886510-6e4d-45bc-b885-3ab7f6b6b2c6
caps.latest.revision: 18
caps.handback.revision: 18
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# コンパイラ エラー CS0281
フレンド アクセスは 'AssemblyName1' に許可されましたが、出力アセンブリは 'AssemblyName2' という名前です。 'AssemblyName1' への参照を追加するか、または出力アセンブリ名が一致するように変更してください。  
  
 フレンド アクセスは、アセンブリが別のアセンブリのパブリックでない型を参照できるようにする新しい共通言語ランタイム \(CLR\) 機能です。 このエラーは、フレンド アクセスを許可するアセンブリが、許可されるアセンブリに間違った名前を指定した場合に発生します。 詳細については、「[フレンド アセンブリ](../Topic/Friend%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)」を参照してください。  
  
## 使用例  
 次の一連のコード サンプルでは、CS0281 が生成されます。  
  
 厳密な名前付きアセンブリの作成に使用されるファイルは、次のように生成されます。  
  
-   sn \-d CS0281.snk  
  
-   sn \-k CS0281.snk  
  
-   sn \-i CS0281.snk CS0281.snk  
  
-   sn \-pc CS0281.snk key.publickey  
  
-   sn \-tp key.publickey  
  
```  
// CS0281.cs // compile with: /target:library /keyfile:CS0281.snk public class A {}  
```  
  
## 使用例  
  
```  
// CS0281_b.cs // compile with: /target:library /keyfile:CS0281.snk /reference:CS0281.dll [assembly:System.Runtime.CompilerServices.InternalsVisibleTo("CS0281 , PublicKey=00240000048000009400000006020000002400005253413100040000010001004b2d4d56af7c50be2fcbbf97cb880b9e73ad84467a587191fef63aadc118a96cecf9d508cd679c907b6e20f71684300bdc2c0a851019af0c96b29bf8f1339753276041aefd67db46139e6348b3a12f29537b4dc6c2c19829df2c9ed6803f3c63c3b84cfa2728849386aea575c543a5f70fa85793d2946f15f7fe1ccb0c5e8fe0")] class B : A {}  
```  
  
## 使用例  
 次の例では CS0281 が生成されます。  
  
 この例では、最初の例の出力ファイルと同じ名前の出力ファイルが作成されることに注意してください。 解決するには、コンポーネントのアセンブリ属性を変更したり、クラス C を追加したりしないでください。  
  
```  
// CS0281_c.cs // compile with: /target:library /out:CS0281.dll /keyfile:CS0281.snk /reference:CS0281_b.dll // CS0281 expected [assembly:System.Reflection.AssemblyVersion("3")] [assembly:System.Reflection.AssemblyCulture("en-us")] class C : B {} public class A {}  
```