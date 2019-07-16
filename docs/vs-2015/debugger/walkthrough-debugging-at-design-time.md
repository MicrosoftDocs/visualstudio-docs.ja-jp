---
title: 'チュートリアル: デザイン時のデバッグ |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], design-time
- breakpoints, design-time debugging
- Immediate window, design-time debugging
- design-time debugging
ms.assetid: 35bfdd2c-6f60-4be1-ba9d-55fce70ee4d8
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 54466cc3561c194199bbad2b35cd00433da2b0f3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149430"
---
# <a name="walkthrough-debugging-at-design-time"></a>チュートリアル: デザイン時のデバッグ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio を使用する**イミディ エイト**ウィンドウで、アプリケーションが実行されていないときに、関数またはサブルーチンを実行します。 関数またはサブルーチンにブレークポイントが含まれているとき、適切なポイントで実行を中断します。 デバッガー ウィンドウを使用して、プログラムの状態を確認できます。 この機能は、デザイン時のデバッグと呼ばれます。  
  
 次に、この機能の操作手順を説明します。  
  
### <a name="to-hit-breakpoints-from-the-immediate-window"></a>[イミディエイト] ウィンドウからブレークポイントにヒットするには  
  
1. 次のコードを Visual Basic コンソール アプリケーションに貼り付けます。  
  
    ```  
    Module Module1  
  
        Sub Main()  
            MySub()  
        End Sub  
  
        Function MyFunction() As Decimal  
            Static i As Integer  
            i = i + 1  
            Dim s As String  
  
            s = "Add Breakpoint here"  
            Return 4  
        End Function  
  
        Sub MySub()  
            MyFunction()  
        End Sub  
    End Module  
    ```  
  
2. `s="Add BreakPoint Here"` という行にブレークポイントを設定します。  
  
3. 次の入力、**イミディ エイト**ウィンドウ。 `?MyFunction<enter>`  
  
4. ブレークポイントにヒットしたことと、呼び出し履歴が正確であることを確認します。  
  
5. **デバッグ** メニューのをクリックして**続行**、まだデザイン モードであることを確認します。  
  
6. 次の入力、**イミディ エイト**ウィンドウ。 `?MyFunction<enter>`  
  
7. 次の入力、**イミディ エイト**ウィンドウ。 `?MySub<enter>`  
  
8. ブレークポイントにヒットし、静的変数の値を確認することを確認`i`で、**ローカル**ウィンドウ。 3 という値が表示されます。  
  
9. 呼び出し履歴が正確であることを確認します。  
  
10. **デバッグ** メニューのをクリックして**続行**、まだデザイン モードであることを確認します。  
  
## <a name="see-also"></a>関連項目  
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [デバッガーの基本事項](../debugger/debugger-basics.md)
