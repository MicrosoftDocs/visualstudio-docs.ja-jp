---
title: 割り当てフック関数と C ランタイムのメモリ割り当て
description: Visual Studio のデバッグでの割り当てフックと C ランタイムのメモリ割り当てについて説明します。 割り当てフック関数では、_CRT_BLOCK ブロックを明示的に無視する必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.hooks
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [C++], hook functions
- memory allocation, troubleshooting allocation hooks
- allocation hooks
- hooks, allocation
ms.assetid: cc34ee96-3d91-41bd-a019-aa3759139e7e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 49739a0c07426329dc20f7fd459febcc70866ec9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866061"
---
# <a name="allocation-hooks-and-c-run-time-memory-allocations"></a>割り当てフック関数と C ランタイムのメモリ割り当て
割り当てフック関数に課せられている非常に重大な制限は、`_CRT_BLOCK` ブロックを明示的に無視する必要があることです。 これらのブロックは、内部メモリを割り当てる C ランタイム ライブラリ関数を呼び出した場合に、C ランタイム ライブラリ関数によって内部的に行われるメモリ割り当てです。 割り当てフック関数の先頭に次のコードを追加することで、`_CRT_BLOCK` ブロックを無視できます。

```cpp
if ( nBlockUse == _CRT_BLOCK )
    return( TRUE );
```

割り当て用のフック関数で `_CRT_BLOCK` 型のブロックを無視しないと、このフック関数から C ランタイム ライブラリ関数を呼び出した場合に、プログラムが無限ループに陥ることがあります。 たとえば、`printf` は内部的にメモリを割り当てます。 フック コードで `printf` を呼び出すと、その結果行われる割り当てによって再びフックが呼び出され、それによって、スタック オーバーフローが発生するまで、再び **printf** が呼び出されるという繰り返しが発生します。 `_CRT_BLOCK` 型の割り当て処理をレポートする必要がある場合は、この制限事項を回避するために、C ランタイム関数ではなく Windows API 関数を使用して書式設定や出力を行う方法があります。 Windows API は C ランタイム ライブラリのヒープを使用しないため、割り当て用のフック関数を使用しても無限ループに陥る心配はありません。

ランタイム ライブラリのソース ファイルを調べる場合、既定の割り当て用のフック関数 **CrtDefaultAllocHook** (これは単に **TRUE** を返します) が独自の個別のファイル (DBGHOOK.C) の中にあることがわかります。 アプリケーションの **main** 関数の前に実行されるランタイムのスタートアップ コードによる割り当て時にも割り当てのフックが呼び出されるようにするには、[_CrtSetAllocHook](/cpp/c-runtime-library/reference/crtsetallochook) を使用する代わりに、この既定の関数を独自の関数に置き換えることができます。

## <a name="see-also"></a>関連項目
- [デバッグ用フック関数の作成](../debugger/debug-hook-function-writing.md)
