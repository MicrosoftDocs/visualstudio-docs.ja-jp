---
title: Print コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.print
helpviewer_keywords:
- Debug.Print command
- Print method
- Print command
ms.assetid: 0412d381-590a-483f-bab4-6e1cca095645
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 65d78387c6d60d0b432db9aab175fbfe8dc2869b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203559"
---
# <a name="print-command"></a>Print コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

式を評価するか、指定したテキストを表示します。  
  
## <a name="syntax"></a>構文  
  
```  
Debug.Print text  
```  
  
## <a name="arguments"></a>引数  
 `text`  
 必須です。 評価対象の式または表示対象のテキストです。  
  
## <a name="remarks"></a>解説  
 このコマンドのエイリアスとして疑問符 (?) を使用できます。 したがって、たとえば次のコマンド  
  
```  
>Debug.Print expA  
```  
  
 は、次のように記述することもできます。  
  
```  
>? expA  
```  
  
 どちらのコマンドでも、式 `expA` の現在の値が返されます。  
  
## <a name="example"></a>例  
  
```  
>Debug.Print varA  
```  
  
## <a name="see-also"></a>関連項目  
 [Evaluate Statement コマンド](../../ide/reference/evaluate-statement-command.md)   
 [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)   
 [コマンド ウィンドウ](../../ide/reference/command-window.md)   
 [[検索/コマンド] ボックス](../../ide/find-command-box.md)   
 [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
