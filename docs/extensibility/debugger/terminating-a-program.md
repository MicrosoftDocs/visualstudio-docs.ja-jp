---
title: プログラムの終了 | Microsoft Docs
description: この記事では、IDE からデバッグ エンジンを使用して、スレッドが 1 つである 1 つのプログラムを終了する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debugging [Debugging SDK], terminating a program
ms.assetid: eedda0a3-5e05-44fe-841d-a2f4866ac72d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: db67e0a391f40fc17a80e616e10aa46a600337a4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057859"
---
# <a name="terminating-a-program"></a>プログラムの終了
次のセクションでは、スレッドが 1 つである 1 つのプログラムを終了する方法について説明します。

## <a name="termination-process"></a>終了プロセス

1. DE から有効な [IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md) を含む [IDebugThreadDestroyEvent2](../../extensibility/debugger/reference/idebugthreaddestroyevent2.md) が送信されます。

2. DE から有効な [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) を含む [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) が送信されます。

   IDE はデザイン モードに切り替わります。 デバッグ エンジンまたはランタイム環境から [IDebugPortNotify2::RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) が呼び出され、ポートからプログラムが削除されます。

## <a name="see-also"></a>関連項目
- [デバッガー イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
