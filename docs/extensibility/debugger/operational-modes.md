---
title: 操作モード | Microsoft Docs
description: IDE が動作する 3 つのモード (デザイン モード、実行モード、中断モード) について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, modes
ms.assetid: f69972d0-809d-40df-9da3-04738791391c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 563db644069731c5d74088dadf296933c36b0cc1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067843"
---
# <a name="operational-modes"></a>操作モード
IDE が動作するモードには、次の 3 つがあります。

- [デザイン モード](#vsconoperationalmodesanchor1)

- [実行モード](#vsconoperationalmodesanchor2)

- [中断モード](#vsconoperationalmodesanchor3)

  カスタム デバッグ エンジン (DE) をこれらのモード間でどのように移行させるかは実装上の決定であり、移行メカニズムについてよく理解しておく必要があります。 これらのモードには、DE によって直接実装される場合とされない場合があります。 これらのモードは、実際には、ユーザーの操作または DE からのイベントに基づいて切り替わるデバッグ パッケージ モードです。 たとえば、実行モードから中断モードへの移行は、DE からの停止イベントによって引き起こされます。 中断モードから実行モードまたはステップ モードへの移行は、ステップ実行や実行などのユーザーが行う操作によって引き起こされます。 DE の移行の詳細については、「[実行の制御](../../extensibility/debugger/control-of-execution.md)」を参照してください。

## <a name="design-mode"></a><a name="vsconoperationalmodesanchor1"></a> デザイン モード
 デザイン モードは、Visual Studio によるデバッグが実行されていない状態です。この間に、アプリケーションでデバッグ機能を設定できます。

 デザイン モードの場合、いくつかのデバッグ機能しか使用できません。 開発者は、ブレークポイントを設定するか、ウォッチ式を作成することができます。 IDE がデザイン モードの間は、DE が読み込まれたり呼び出されたりすることはありません。 DE との相互作用は、実行モードと中断モードでのみ行われます。

## <a name="run-mode"></a><a name="vsconoperationalmodesanchor2"></a> 実行モード
 IDE のデバッグ セッションでプログラムが実行されると、実行モードに移行します。 アプリケーションは、終了するまで、ブレークポイントにヒットするまで、または例外がスローされるまで実行されます。 アプリケーションの実行が終了すると、DE はデザイン モードに移行します。 ブレークポイントにヒットしたとき、または例外がスローされた場合、DE は中断モードに移行します。

## <a name="break-mode"></a><a name="vsconoperationalmodesanchor3"></a> 中断モード
 デバッグ プログラムの実行が中断されると、中断モードに移行します。 中断モードの場合、開発者は中断時のアプリケーションのスナップショットを取得したり、アプリケーションの状態を分析して、アプリケーションの実行方法を変更したりできます。 開発者は、コードの表示と編集、データの検査または変更、アプリケーションの再起動、実行の終了、または同じポイントからの実行の継続を行うことができます。

 DE から同期停止イベントが送信されると、中断モードに移行します。 同期停止イベントは、停止イベントとも呼ばれ、デバッグ中のアプリケーションによってコードの実行が停止されたことがセッション デバッグ マネージャー (SDM) と IDE に通知されます。 [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) インターフェイスと [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) インターフェイスは停止イベントの例です。

 停止イベントは、次のいずれかのメソッドを呼び出すことで継続されます。これにより、デバッガーが中断モードから実行モードまたはステップ モードに移行します。

- [実行](../../extensibility/debugger/reference/idebugprocess3-execute.md)

- [Step](../../extensibility/debugger/reference/idebugprocess3-step.md)

- [続行](../../extensibility/debugger/reference/idebugprocess3-continue.md)

### <a name="step-mode"></a><a name="vsconoperationalmodesanchor4"></a> ステップ モード
 プログラムで、次のコード行へのステップ実行、または関数に対するステップ イン、ステップ オーバー、ステップ アウトが実行されると、ステップ モードになります。 ステップは、[Step](../../extensibility/debugger/reference/idebugprocess3-step.md) メソッドを呼び出すことによって実行されます。 このメソッドには、入力パラメーターとして [STEPUNIT](../../extensibility/debugger/reference/stepunit.md) および [STEPKIND](../../extensibility/debugger/reference/stepkind.md) 列挙体を指定する `DWORD` が必要です。

 プログラムで、次のコード行または関数にステップ インした場合、またはカーソルまたは設定されたブレークポイントまで実行された場合、DE は自動的に中断モードに戻ります。

## <a name="see-also"></a>こちらもご覧ください
- [実行の制御](../../extensibility/debugger/control-of-execution.md)
