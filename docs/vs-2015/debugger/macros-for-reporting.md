---
title: レポート用マクロの |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.macros
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- macros, CRT reporting macros
- macros, debugging with
- _RPTFn macro
- CRT, reporting macros
- debugging [CRT], reporting macros
- _RPTn macro
ms.assetid: f2085314-a3a8-4caf-a5a4-2af9ad5aad05
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e4aee33d571f95e24a359fa2bc7e12ae8d64eae0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62431629"
---
# <a name="macros-for-reporting"></a>レポート用マクロの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

使用することができます、 **_RPTn**、および **_RPTFn** crtdbg マクロ。代わりに、H`printf`デバッグ ステートメント。 これらのマクロは、のリリースで自動的に消滅ビルド **_DEBUG**が定義されていないで囲む必要はありませんので **#ifdef**s。  
  
|マクロ|説明|  
|-----------|-----------------|  
|**_RPT0**、**_RPT1**、**_RPT2**、**_RPT3**、**_RPT4**|メッセージ文字列と、0 から 4 個の引数を出力します。 _RPT1 から **_RPT4** の場合、メッセージ文字列は、引数に対して printf 形式の書式設定文字列として機能します。|  
|**_RPTF0**, **_RPTF1**, **,_RPTF2**, **_RPTF4**|同じ **_RPTn**がこれらのマクロは、マクロが配置されているファイル名と行番号も出力します。|  
  
 次に例を示します。  
  
```  
#ifdef _DEBUG  
    if ( someVar > MAX_SOMEVAR )  
        printf( "OVERFLOW! In NameOfThisFunc( ),  
               someVar=%d, otherVar=%d.\n",  
               someVar, otherVar );  
#endif  
```  
  
 このコードは、`someVar` の値と `otherVar` の値を **stdout** に出力します。 次のように `_RPTF2` を呼び出すと、これらの値と一緒にファイル名と行番号も出力できます。  
  
```  
if (someVar > MAX_SOMEVAR) _RPTF2(_CRT_WARN, "In NameOfThisFunc( ), someVar= %d, otherVar= %d\n", someVar, otherVar );  
```  
  
 特定のアプリケーションでは、C ランタイム ライブラリのマクロで提供されているデバッグ レポートでは不十分な場合があります。その場合は、独自の要件を満たす専用のマクロを設計できます。 たとえば、ヘッダー ファイルの 1 つに、次のような **ALERT_IF2** というマクロを定義するコードを含めることができます。  
  
```  
#ifndef _DEBUG                  /* For RELEASE builds */  
#define  ALERT_IF2(expr, msg, arg1, arg2)  do {} while (0)  
#else                           /* For DEBUG builds   */  
#define  ALERT_IF2(expr, msg, arg1, arg2) \  
    do { \  
        if ((expr) && \  
            (1 == _CrtDbgReport(_CRT_ERROR, \  
                __FILE__, __LINE__, msg, arg1, arg2))) \  
            _CrtDbgBreak( ); \  
    } while (0)  
#endif  
```  
  
 1 回の呼び出しに**ALERT_IF2**のすべての機能を実行する可能性があります、 **printf**このトピックの冒頭にあるコード。  
  
```  
ALERT_IF2(someVar > MAX_SOMEVAR, "OVERFLOW! In NameOfThisFunc( ),   
someVar=%d, otherVar=%d.\n", someVar, otherVar );  
```  
  
 カスタム マクロは、目的に応じて出力情報の量を増減したり、出力先を変更したりなどの変更を簡単に実現できるため、デバッグ要件が複雑さを増してくる段階で使用すると便利です。  
  
## <a name="see-also"></a>関連項目  
 [CRT のデバッグ技術](../debugger/crt-debugging-techniques.md)
