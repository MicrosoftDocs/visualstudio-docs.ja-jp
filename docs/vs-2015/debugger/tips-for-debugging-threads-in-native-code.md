---
title: ネイティブ コード内のスレッドをデバッグするためのヒント |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- threading [Visual Studio], debugging
- debugging [Visual Studio], threads
ms.assetid: 0374c8c6-57a3-4cfe-8047-2effef5ff5dc
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4a0a72f9846add13f2f57581a0b836a9f57f8150
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "58963095"
---
# <a name="tips-for-debugging-threads-in-native-code"></a>ネイティブ コード内のスレッドのデバッグのヒント
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ここでは、ネイティブ コード内のスレッドをデバッグするときに役立つヒントを紹介します。  
  
-   **[ウォッチ]** ウィンドウまたは **[クイック ウォッチ]** ダイアログ ボックスで「`@TIB`」と入力すると、[スレッド情報ブロック] の内容を表示できます。  
  
-   **[ウォッチ]** ウィンドウまたは **[クイック ウォッチ]** ダイアログ ボックスで「`@Err`」と入力すると、現在のスレッドの最終エラー コードを表示できます。  
  
-   マルチスレッド アプリケーションのデバッグには、C ランタイム ライブラリ (CRT) 関数を使用できます。 詳細については、「[_malloc_dbg](http://msdn.microsoft.com/library/c97eca51-140b-4461-8bd2-28965b49ecdb)」をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [マルチスレッド アプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)
