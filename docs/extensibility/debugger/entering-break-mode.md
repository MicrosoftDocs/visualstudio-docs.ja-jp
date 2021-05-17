---
title: 中断モードの開始 | Microsoft Docs
description: 関数内で検出されたブレークポイント、カーソル位置のソース コード行までの実行、またはブレークポイントまでの実行で発生するプロセスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- break mode
- debugging [Debugging SDK], entering break mode
ms.assetid: e9a8a241-cd21-4d4e-999a-283554c288b1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6e8af8aa2765e199e8e278982669f68b3019b6c2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097215"
---
# <a name="enter-break-mode"></a>中断モードに入る
次の情報では、関数にステップインし、カーソルがあるソース コードの行まで実行するか、またはブレークポイントまで実行した後に、ブレークポイントが検出されたときに発生するプロセスについて説明します。

## <a name="break-mode-process"></a>中断モード プロセス

1. デバッグ エンジン (DE) によって、[IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md)、[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)、またはその他の何らかの停止イベントが送信され、IDE が中断モードになります。

2. SDM では、次のように、スレッドから呼び出し履歴情報が取得されます。

    - [IDebugThread2::EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)

    - [IEnumDebugFrameInfo2::GetCount](../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)

    - [IEnumDebugFrameInfo2::Next](../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)

    - ソース コード情報を取得する [IDebugStackFrame2::GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)

    - ファイル名を取得する [IDebugDocumentContext2::GetName](../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)

    - ステートメント範囲を取得する [IDebugDocumentContext2::GetStatementRange](../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)

    - メモリ情報を取得する [IDebugStackFrame2::GetCodeContext](../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)

## <a name="see-also"></a>関連項目
- [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
