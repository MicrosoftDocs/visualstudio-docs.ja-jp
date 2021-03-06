---
title: 割り当てフック関数 | Microsoft Docs
description: Visual Studio で C ランタイム (CRT) デバッグを実行する必要があるとき、_CrtSetAllocHook を利用してインストールされる割り当てフック関数を使用する方法について説明します。
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
- memory allocation, logging allocation information
- insufficient memory
- debugging [C++], hook functions
- _CrtSetAllocHook function
- allocation hooks
- hooks, allocation
ms.assetid: 6bfbdb65-8cb1-4c21-8c45-7194a2b77c1e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3c032ca57e5a046a9f2dd2295226263ffe20f99e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858008"
---
# <a name="allocation-hook-functions"></a>割り当てフック関数
[_CrtSetAllocHook](/cpp/c-runtime-library/reference/crtsetallochook) を使用して組み込まれたメモリ割り当て用のフック関数は、メモリの割り当て、再割り当て、および解放のたびに呼び出されます。 この種類のフックは、さまざまな目的で使用できます。 メモリ不足の状況がアプリケーションでどのように処理されるかをテストする場合、たとえば、割り当てパターンを調査する場合や、後から分析するために割り当て情報をログに記録する場合に使用します。

> [!NOTE]
> 割り当てフック関数の中で C ランタイム ライブラリの関数を使用する場合は、「[割り当てフック関数と C ランタイムのメモリ割り当て](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md)」で説明する制限事項があるので注意してください。

 割り当て用のフック関数には、次の例のようなプロトタイプが必要です。

```cpp
int YourAllocHook(int nAllocType, void *pvData,
        size_t nSize, int nBlockUse, long lRequest,
        const unsigned char * szFileName, int nLine )
```

 [_CrtSetAllocHook](/cpp/c-runtime-library/reference/crtsetallochook) に渡すポインターは **_CRT_ALLOC_HOOK** 型です。これらは、CRTDBG.H で次のように定義されています。

```cpp
typedef int (__cdecl * _CRT_ALLOC_HOOK)
    (int, void *, size_t, int, long, const unsigned char *, int);
```

 ランタイム ライブラリからフックが呼び出されるときに、引数 *nAllocType* には、これから行われる割り当て処理の種類 ( **_HOOK_ALLOC**、 **_HOOK_REALLOC**、または **_HOOK_FREE**) が指定されます。 解放または再割り当ての場合、`pvData` には、これから解放されるブロックのユーザー アーティクルへのポインターが格納されます。 ただし、割り当ての場合、割り当てが行われていないため、このポインターは null です。 その他の引数には、対象の割り当てのサイズ、そのブロックの種類、それに関連付けられている連番の要求番号、およびファイル名へのポインターが格納されます。 該当する場合、引数には、割り当てが行われた行番号も格納されます。 フック関数は、分析などの必要なタスクを実行した後で、割り当て処理を継続できる場合は **TRUE**、継続できない場合は **FALSE** を返すようにします。 この種のフック関数の簡単なものとしては、それまでに割り当てられたメモリの総量をチェックし、その量が少なめに設定した上限を超えている場合は **FALSE** を返す関数が考えられます。 この関数を使用すると、メモリがかなり不足している場合だけに発生するメモリ割り当てエラーを意図的に発生させることができます。 さらに複雑なフック関数としては、割り当てパターンを追跡したり、メモリの使用状況を分析したり、特定の状態が発生したときにレポートを作成したりする関数が考えられます。

## <a name="see-also"></a>関連項目

- [割り当てフック関数と C ランタイムのメモリ割り当て](../debugger/allocation-hooks-and-c-run-time-memory-allocations.md)
- [デバッグ用フック関数の作成](../debugger/debug-hook-function-writing.md)