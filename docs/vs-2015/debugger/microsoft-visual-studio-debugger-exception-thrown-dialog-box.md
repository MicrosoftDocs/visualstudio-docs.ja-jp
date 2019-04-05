---
title: Microsoft Visual Studio デバッガー (例外がスローされます) ダイアログ ボックス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.exceptions.thrown
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Microsoft Visual Studio Debugger (Exception Thrown) dialog box
- exception handling, during debugging
- debugger, exceptions
- throwing exceptions, during debugging
ms.assetid: 1fe98d10-c8f9-4b39-a920-99169bfd542e
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d0968c5ee67df10bad99ae31a3f0d812251ad818
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58978057"
---
# <a name="microsoft-visual-studio-debugger-exception-thrown-dialog-box"></a>[Microsoft Visual Studio デバッガー (例外がスローされました)] ダイアログ ボックス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プログラムに例外が発生しました。 このダイアログ ボックスには、スローされた例外の種類が報告されます。 コードでは、この例外を処理する必要があります。 この例外を処理するには、次のオプションから選択できます。  
  
 **Break**  
 デバッガーの実行を中断できます。 中断するまで、例外ハンドラーは起動されません。 中断した位置から継続すると、例外ハンドラーが起動されます。  
  
 **Continue**  
 実行が継続され、例外ハンドラーによって例外が処理されます。 このオプションは、特定の種類の例外に対しては使用できません。 **[継続]** によってアプリケーションは実行を継続できます。 ネイティブ アプリケーションでは、例外が再スローされます。 マネージド アプリケーションでは、プログラムが終了するか、または例外がホスト アプリケーションによって処理されます。  
  
> [!NOTE]
>  未処理の例外がマネージド コードで発生した後には実行を継続できません。 マネージド コードで未処理の例外が発生した後に **[継続]** をクリックすると、デバッグが停止します。  
  
 **無視**  
 実行が継続されますが、例外ハンドラーは起動されません。 例外ハンドラーが起動されないため、例外やエラーなどが続けて発生することがあります。 このオプションは、特定の種類の例外に対しては使用できません。  
  
## <a name="see-also"></a>関連項目  
 [デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)   
 [例外の推奨事項](http://msdn.microsoft.com/library/f06da765-235b-427a-bfb6-47cd219af539)   
 [例外処理](http://msdn.microsoft.com/library/ccb11fe8-6938-41ac-b477-a183e85865b9)
