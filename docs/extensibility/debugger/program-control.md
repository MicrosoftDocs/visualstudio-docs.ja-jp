---
title: プログラムの制御 | Microsoft Docs
description: プログラム レベルで実行される Visual Studio デバッグのルーチン (スレッドの実行、ステップ実行、続行、中断/再開など) について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 6be80904-e66c-4cae-8891-1113b799fb01
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7b2946309c72fbdddf2794c1da1e773e9a529368
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900714"
---
# <a name="program-control"></a>プログラムの制御
Visual Studio のデバッグでは、次のステップ実行と続行のルーチンがすべてプログラム レベルで実行されます。

- 次のステートメントを設定する。つまり、特定のフレーム環境で実行される次の命令にコンピューターを設定する

- 実行する。つまり、ステップ実行モードの終了を続行する

- 次の命令にステップ実行する

- 現在のステップ実行モードを続行する

- プログラムに含まれているスレッドを中断する

- プログラムに含まれているスレッドを再開する

> [!NOTE]
> 呼び出し履歴の表示は、スレッド レベルで実装されます。 スレッドの呼び出し履歴を表示するときにフレーム情報を列挙するには、[IEnumDebugFrameInfo2](../../extensibility/debugger/reference/ienumdebugframeinfo2.md) インターフェイスのすべてのメソッドを実装する必要があります。

## <a name="methods-of-program-control"></a>プログラムの制御のメソッド
 次の表は、最小限機能するデバッグ エンジン (DE) と実行制御のために実装する必要がある [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) のメソッドを示しています。

|メソッド|説明|
|------------|-----------------|
|[IDebugProgram2::Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)|プログラムに含まれるすべてのスレッドの実行を停止状態から続行します。 実行の制御に必要です。|
|[IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)|プログラムに含まれるすべてのスレッドの実行を停止状態から続行します。 実行の制御に必要です。|
|[IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md)|指定されたスレッドでステップを実行します。 プログラムに含まれる他のすべてのスレッドの実行を続行します。 実行の制御に必要です。|

 マルチスレッド プログラムの場合は、[IDebugProgram2::EnumThreads](../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) メソッドと [IEnumDebugThreads2](../../extensibility/debugger/reference/ienumdebugthreads2.md) インターフェイスのすべてのメソッドを実装する必要もあります。

## <a name="see-also"></a>関連項目
- [実行の制御と状態の評価](../../extensibility/debugger/execution-control-and-state-evaluation.md)
