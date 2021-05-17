---
title: デバッガーの起動 |Microsoft Docs
description: デバッガーを起動するために必要な、適切な属性を持つメソッドとイベントのシーケンスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], launching the debugger
- debugger [Debugging SDK], launching
ms.assetid: f24da1a1-f923-48b4-989f-18a22b581d1b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 67764a7f59c1b44e7e8cbc7a81befb120c541461
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094667"
---
# <a name="launch-the-debugger"></a>デバッガーを起動します
デバッガーを起動するには、適切な属性を持つメソッドとイベントの正しいシーケンスを送信する必要があります。

## <a name="sequences-of-methods-and-events"></a>メソッドとイベントのシーケンス

1. セッション デバッグ マネージャー (SDM) は、 **[デバッグ]** メニューを選択し、 **[開始]** をクリックすることで呼び出されます。 詳細については、[プログラムの起動](../../extensibility/debugger/launching-a-program.md)に関するページを参照してください。

2. SDM が [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドを呼び出します。

3. デバッグ エンジン (DE) のプロセス モデルに基づいて、`IDebugProgramNodeAttach2::OnAttach` メソッドから次のいずれかのメソッドが返され、次に実行する処理が決まります。

     `S_FALSE` が返される場合、デバッグ エンジン (DE) は仮想マシンのプロセスで読み込まれます。

     または

     `S_OK` が返される場合、DE は SDM のプロセスで読み込まれます。 その後、SDM は次のタスクを実行します。

    1. [GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md) を呼び出して、DE のエンジン情報を取得します。

    2. DE を共同作成します。

    3. [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) を呼び出します。

4. DE が、`EVENT_SYNC` 属性を使用して SDM に [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) を送信します。

5. DE が、`EVENT_SYNC` 属性を使用して SDM に [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) を送信します。

6. DE が、`EVENT_SYNC` 属性を使用して SDM に [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) を送信します。

7. DE が、`EVENT_SYNC` 属性を使用して SDM に [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) を送信します。

8. DE が、`EVENT_SYNC` 属性を使用して SDM に [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) を送信します。

## <a name="see-also"></a>関連項目
- [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
- [プログラムの起動](../../extensibility/debugger/launching-a-program.md)
