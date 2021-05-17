---
title: 例外処理 (Visual Studio SDK) | Microsoft Docs
description: 例外がスローされたときに発生するプロセスについて説明します。 この記事では、関連するすべての手順について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], exception handling
ms.assetid: 7279dc16-db14-482c-86b8-7b3da5a581d2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f74337964b73683a71b180699da626121a4d3067
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097020"
---
# <a name="exception-handling-visual-studio-sdk"></a>例外処理 (Visual Studio SDK)
次に、例外がスローされた場合に発生するプロセスについて説明します。

## <a name="exception-handling-process"></a>例外処理プロセス

1. 例外が最初にスローされたとき、ただし、デバッグ中のプログラムの例外ハンドラーによって処理される前に、デバッグ エンジン (DE) によって、[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) が停止イベントとして、セッション デバッグ マネージャー (SDM) に送信されます。 `IDebugExceptionEvent2` は、例外の設定 (デバッグ パッケージの [例外] ダイアログボックスで指定された) で、ユーザーが初回例外通知で停止するように指定した場合にのみ送信されます。

2. SDM によって、[IDebugExceptionEvent2::GetException](../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md) が呼び出され、例外のプロパティが取得されます。

3. デバッグ パッケージによって、[IDebugExceptionEvent2::CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) が呼び出され、ユーザーに提示するオプションが決定されます。

4. デバッグ パッケージによって、初回例外ダイアログ ボックスが開かれ、例外を処理する方法がユーザーに尋ねられます。

5. ユーザーが続行するように選択した場合、SDM によって、[IDebugExceptionEvent2::CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) が呼び出されます。

    - メソッドで S_OK が返された場合、[IDebugExceptionEvent2::PassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md) が呼び出されます。

         または

         メソッドで S_FALSE が返された場合、デバッグ中のプログラムには、例外を処理するための二度目の機会が与えられます。

6. デバッグ中のプログラムに二度目の機会の例外用のハンドラーがない場合、DE によって `IDebugExceptionEvent2` が **EVENT_SYNC_STOP** として SDM に送信されます。

7. デバッグ パッケージによって、初回例外ダイアログ ボックスが開かれ、例外を処理する方法がユーザーに尋ねられます。

8. デバッグ パッケージによって、[IDebugExceptionEvent2::CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) が呼び出され、ユーザーに提示するオプションが決定されます。

9. デバッグ パッケージによって、二度目の機会の例外ダイアログ ボックスが開かれ、例外を処理する方法がユーザーに尋ねられます。

10. メソッドで S_OK が返された場合、`IDebugExceptionEvent2::PassToDebuggee` が呼び出されます。

## <a name="see-also"></a>関連項目
- [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
