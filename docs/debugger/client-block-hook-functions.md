---
title: クライアント ブロック用のフック関数 |Microsoft Docs
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
- client blocks, validating and reporting data
- debugging [C++], hook functions
- _CrtSetDumpClient function
- client blocks, hook functions
- hooks, client block
ms.assetid: f21c197e-565d-4e3f-9b27-4c018c9b87fc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7b0e70e559dc75abd6b8de1b325b9ac300055792
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2019
ms.locfileid: "55039268"
---
# <a name="client-block-hook-functions"></a>Client ブロック用のフック関数
`_CLIENT_BLOCK` 型のブロックに格納されているデータの内容を検証したりレポートしたりするために、専用の関数を作成できます。 作成する関数には、CRTDBG.H で定義されている次のようなプロトタイプが必要です。  

```cpp
void YourClientDump(void *, size_t)  
```  

 つまり、独自のフック関数は、対象となる割り当てブロックの先頭への **void** ポインターと、割り当てサイズを示す **size_t** 型の値を受け取り、`void` を返すようにする必要があります。 それ以外の内容については、自由に決定できます。  

 作成したフック関数を [_CrtSetDumpClient](/cpp/c-runtime-library/reference/crtsetdumpclient) を使用して組み込むと、`_CLIENT_BLOCK` 型のブロックがダンプされるたびに、このフック関数が呼び出されます。 [_CrtReportBlockType](/cpp/c-runtime-library/reference/crtreportblocktype) を使用すると、ダンプされたブロックの型や、その細分化された型に関する情報を取得できます。  

 `_CrtSetDumpClient` に渡す独自の関数へのポインターは **_CRT_DUMP_CLIENT** 型です。これらは、CRTDBG.H で次のように定義されています。  

```cpp
typedef void (__cdecl *_CRT_DUMP_CLIENT)  
   (void *, size_t);  
```  

## <a name="see-also"></a>「  
 [デバッグ用フック関数の作成](../debugger/debug-hook-function-writing.md)   
 [crt_dbg2 サンプル](https://msdn.microsoft.com/library/21e1346a-6a17-4f57-b275-c76813089167)   
 [_CrtReportBlockType](/cpp/c-runtime-library/reference/crtreportblocktype)
