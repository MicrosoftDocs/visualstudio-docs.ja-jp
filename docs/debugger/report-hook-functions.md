---
title: レポート用のフック関数 |Microsoft Docs
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
- hooks, report
- _CrtDbgReport function
- debugger, report hook functions
- memory allocation, debug heap
- debugging [C++], hook functions
- _CrtSetReportHook function
- report hook functions
ms.assetid: 1854bca7-d7eb-4502-89bf-b1ee64cb50ef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a0bb14b47fb17c4d59089aafa123115b85ab9342
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72729871"
---
# <a name="report-hook-functions"></a>レポート用のフック関数
[_CrtSetReportHook](/cpp/c-runtime-library/reference/crtsetreporthook) を使用してインストールされたレポート用のフック関数は、[_CrtDbgReport](/cpp/c-runtime-library/reference/crtdbgreport-crtdbgreportw) がデバッグ レポートを生成するたびに呼び出されます。 レポート用のフック関数を使用して、特定の割り当て型に関するレポートだけを出力できます。 レポート用のフック関数には、次のようなプロトタイプが必要です。

```cpp
int YourReportHook(int nRptType, char *szMsg, int *retVal);
```

 **_CrtSetReportHook**に渡すポインターの型は **_CRT_REPORT_HOOK**で、crtdbg.h で定義されています。始め

```cpp
typedef int (__cdecl *_CRT_REPORT_HOOK)(int, char *, int *);
```

 ランタイム ライブラリが独自のフック関数を呼び出す場合は、引数 *nRptType* には、レポートのカテゴリ ( **_CRT_WARN**、 **_CRT_ERROR**、または **_CRT_ASSERT**) が含まれます。引数 *szMsg* には、レポート用の完全にアセンブルされたメッセージ文字列へのポインターが含まれます。また、*retVal* には、`_CrtDbgReport` がレポート作成後に通常どおり実行を継続するのか、デバッガーを起動するのかを示す値が含まれます。 (*retVal* の値が 0 の場合は実行を継続し、1 の場合はデバッガーを起動します。)

 フック関数でメッセージを完全に処理できたため、それ以上レポートを出力する必要がない場合は、**TRUE** を返すようにします。 **FALSE** を返した場合は、`_CrtDbgReport` は通常どおりにレポート メッセージを出力します。

## <a name="see-also"></a>関連項目
- [デバッグ用フック関数の作成](../debugger/debug-hook-function-writing.md)
- [crt_dbg2 サンプル](https://github.com/Microsoft/VCSamples/tree/master/VC2010Samples/crt/crt_dbg2)
