---
title: コンテキスト演算子 (C++)、デバッガーで |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.operators
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- expressions [C++], native debugger
- evaluation
- format specifiers, expressions
- context operator, in expressions
- debugging [C++], expressions
- native expression evaluator
ms.assetid: 73cc9afe-f4a4-474e-bb89-5a33fb5e570c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 9222a36bd1e03a1f213a0d3ea0e86e269e912d12
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2019
ms.locfileid: "53889580"
---
# <a name="context-operator-in-the-visual-studio-debugger-c"></a>Visual Studio デバッガー (C++) でのコンテキスト演算子
C++ のコンテキスト演算子を使用して、ブレークポイントの場所、変数名、または式を修飾できます。 コンテキスト演算子は、ローカル名で隠されていてほかにアクセス方法がない外部スコープから名前を指定するために利用できます。  
  
##  <a name="BKMK_Using_context_operators_to_specify_a_symbol"></a> 構文  
 コンテキストを指定する 2 つの方法があります。  
  
1.  {,,[*module*] } *expression*  
  
     中かっこ内には、2 個のコンマとモジュール (実行可能ファイルまたは DLL) 名か完全パスが必要です。  
  
     たとえば、EXAMPLE.dll の `SomeFunction` 関数にブレークポイントを設定する場合は、次のようになります。  
  
    ```C++  
    {,,EXAMPLE.dll}SomeFunction  
    ```  
  
2.  *module*!*expression*  
  
    ```C++  
    EXAMPLE.dll!SomeFunction  
    ```  
  
- *module* は、モジュールの名前です。 完全パスを使用することで、同じ名前のモジュールのあいまいさを解消することができます。  
  
   *module* のパスにコンマ、埋め込みスペース、または中かっこが含まれる場合は、コンテキスト パーサーが文字列を適切に認識できるように、パスを引用符で囲む必要があります。 単一引用符は Windows ファイル名の一部として解釈されるので、二重引用符を使用する必要があります。 たとえば、オブジェクトに適用された  
  
  ```C++  
  {,,"a long, long, library name.dll"} g_Var  
  ```  
  
- *expression* は任意の有効な C++ 式で、 *module*内の関数名、変数名、ポインター アドレスなどの有効なターゲットに解決します。  
  
  式エバリュエーターが式に含まれる記号を見つけると、次の順序で記号を検索します。  
  
1.  構文のスコープの外部。現在のブロック (角かっこで囲まれた一連のステートメント) から、外側のブロックに進みます。 現在のブロックは、現在の場所 (命令ポインター アドレス) を含むコードです。  
  
2.  関数スコープ。 現在の関数です。  
  
3.  クラス スコープ。現在の場所が C++ メンバー関数内部の場合です。 クラス スコープにはすべての基底クラスが含まれます。 式エバリュエーターは、通常の優先順位規則を使用します。  
  
4.  現在のモジュール内のグローバル シンボル。  
  
5.  現在のプログラム内のパブリック シンボル。