---
title: "CRT のデバッグ手法 |Microsoft ドキュメント"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- c.runtime.debugging
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [CRT]
- CRT, debugging
- debugging [C++], CRT debug support
ms.assetid: 9be561f6-14a8-44ff-925d-d911d5b8e6ff
caps.latest.revision: 
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.workload:
- multiple
ms.openlocfilehash: 52f1847112741e90634ce0e68acbcfdd11b837db
ms.sourcegitcommit: 32f1a690fc445f9586d53698fc82c7debd784eeb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2017
---
# <a name="crt-debugging-techniques"></a>CRT のデバッグ技術
C ランタイム ライブラリを使用したプログラムをデバッグする場合は、次のデバッグ技術が役立ちます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [CRT デバッグ ライブラリの使用方法](../debugger/crt-debug-library-use.md)  
 C ランタイム ライブラリによって提供されるデバッグ サポートについて説明し、ツールにアクセスするための手順を示します。  
  
 [レポート用マクロの使用](../debugger/macros-for-reporting.md)  
 に関する情報を提供、 **_RPTn**と**_RPTFn**マクロ (CRTDBG で定義されます。H) これの代わりに`printf`デバッグ用のステートメント。  
  
 [デバッグ バージョンのヒープ割り当て関数](../debugger/debug-versions-of-heap-allocation-functions.md)  
 ヒープ割り当て関数の特別なデバッグ バージョンについて説明します。CRT が呼び出しを割り当てる方法、明示的な呼び出しの利点、変換の回避方法、クライアント ブロック内の各割り当て型の追跡、_DEBUG を定義しなかった場合の結果などを扱います。  
  
 [CRT デバッグ ヒープの詳細](../debugger/crt-debug-heap-details.md)  
 メモリ管理とデバッグ ヒープ、デバッグ ヒープ上のブロックの型、デバッグ ヒープの使用法、ヒープ状態レポート関数、およびヒープ割り当て要求の追跡について説明するリンクを提供します。  
  
 [デバッグ用フック関数の作成](../debugger/debug-hook-function-writing.md)  
 クライアント ブロック用のフック関数、割り当てフック関数、割り当てフック関数と CRT メモリ割り当て、およびレポート用のフック関数について説明するリンクを提供します。  
  
 [CRT ライブラリを使用したメモリ リークの検出](../debugger/finding-memory-leaks-using-the-crt-library.md)  
 デバッガーと C ランタイム ライブラリを使用してメモリ リークを検出および分離する手法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)  
 C および C++ アプリケーションのデバッグ時に発生する一般的な問題や共通のデバッグ技術について説明します。  
  
 [デバッガーのセキュリティ](../debugger/debugger-security.md)  
 デバッグをより安全に行うための推奨事項について説明します。