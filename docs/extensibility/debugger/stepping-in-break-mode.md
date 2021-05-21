---
title: 中断モードでのステップ実行 | Microsoft Docs
description: デバッガーが中断モードのときに発生するプロセスについて学習します。 その後、デバッガーでコードをステップ実行する必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode, stepping
- stepping, in break mode
- debugging [Debugging SDK], stepping in break mode
ms.assetid: b08dc8ee-6c63-4462-a097-6f525cfbb35a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0ed11d05e4351ac6ba76bc9aa10531a8a96ddf23
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075407"
---
# <a name="stepping-in-break-mode"></a>中断モードでのステップ実行
次のセクションでは、デバッガーが中断モードであり、コードをステップ実行する必要がある場合に発生するプロセスについて説明します。

## <a name="stepping-process"></a>ステップ実行プロセス

1. [STEPKIND](../../extensibility/debugger/reference/stepkind.md) および [STEPUNIT](../../extensibility/debugger/reference/stepunit.md) 引数を指定して [IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md) を呼び出し、ステップ実行します。

2. ステップ実行が終了したら、停止イベントとして [IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md) を送信します。

## <a name="see-also"></a>関連項目
- [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
