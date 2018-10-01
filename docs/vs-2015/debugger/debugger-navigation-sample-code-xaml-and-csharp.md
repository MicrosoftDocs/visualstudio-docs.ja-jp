---
title: デバッガー ナビゲーションのサンプル コード (Xaml および c#) |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 8f4266bc-4597-43ab-b620-8b08ea988a8e
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4b047c783f685a10adedec4c5b9ccf7b1c2f8f9b
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47535609"
---
# <a name="debugger-navigation-sample-code-xaml-and-c"></a>デバッガーのナビゲーションのサンプル コード (Xaml および C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[デバッガー ナビゲーションのサンプル コード (Xaml および c#)](https://docs.microsoft.com/visualstudio/debugger/debugger-navigation-sample-code-xaml-and-csharp)します。  
  
このトピックのコードは、のサンプル ファイルは、 [(Xaml および c#) は、デバッグ セッションのナビゲート](../debugger/navigate-a-debugging-session-in-visual-studio-xaml-and-csharp.md)トピック。  
  
## <a name="sample-code"></a>サンプル コード  
  
```csharp  
public MainPage()  
{  
    InitializeComponent();  
    methodTrack = "Main Page";             
    Example1();  
}  
  
int Example1()  
{  
    int a = 1;  
    methodTrack += "->Example1 ";  
    int x = Example1_A();  
    return a;  
}  
  
int Example1_A()  
{  
    int b = 2;  
    methodTrack += "->Example1_B ";  
    return b;  
}  
  
void Example2()  
{  
    int c = 3;  
    methodTrack += "->Example2 ";  
    int x = Example2_A();  
    int y = Example2_A();  
    int z = Example2_B();  
}  
  
int Example2_A()  
{  
    int c = 3;  
    methodTrack += "->Example2_A ";  
    return c;  
}  
  
int Example2_B()  
{  
    int d = 3;  
    methodTrack += "->Example2_B ";  
    return d;  
}  
  
void Example3()  
{  
    string s = String.Empty;  
    for (int i = 0; i < 1000; i++)  
    {  
        s += i.ToString() + '\n';  
    }  
    methodTrack += "->Example3 ";  
  
}  
  
void Example4()  
{  
    int x = 0;  
    int y = 100;  
    if (x != 0)  
    {  
        x = 1;  
    }  
    double result = y / x;  
    methodTrack = "->Example4";  
}  
  
string methodTrack = String.Empty;  
  
```



