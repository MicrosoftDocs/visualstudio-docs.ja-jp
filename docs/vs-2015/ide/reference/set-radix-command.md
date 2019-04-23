﻿---
title: SetRadix コマンド | Microsoft ドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.setradix
helpviewer_keywords:
- Set Radix command
- Debug.SetRadix command
ms.assetid: 6ffd1554-7530-4da4-b5f5-e276a5034f3b
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bee6368931dc47b78186ec870039ab292960fa77
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59654075"
---
# <a name="set-radix-command"></a>SetRadix コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

整数値を表示するために使用する基数値を設定または返します。  
  
## <a name="syntax"></a>構文  
  
```  
Debug.SetRadix [10 | 16 | hex | dec]  
```  
  
## <a name="arguments"></a>引数  
 `10` または `16`、あるいは `hex` または `dec`  
 任意。 10 (10 または dec) 進数または 16 (16 または hex) 進数を示します。 引数を省略すると、現在の基数値が返されます。  
  
## <a name="example"></a>例  
 この例では、整数値を 16 進形式で表示するための環境を設定します。  
  
```  
>Debug.SetRadix hex  
```  
  
## <a name="see-also"></a>関連項目
 [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)   
 [コマンド ウィンドウ](../../ide/reference/command-window.md)   
 [[検索/コマンド] ボックス](../../ide/find-command-box.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
