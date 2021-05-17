---
title: プログラムへのアタッチとデタッチ | Microsoft Docs
description: デバッガーをアタッチするために適切な属性を使用してメソッドとイベントの正しいシーケンスを送信する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, attaching to programs
- debug engines, detaching from programs
ms.assetid: 79dcbb9b-c7f8-40fc-8a00-f37fe1934f51
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fb51cb3e6c16916e3778dde06fb2ac274608ed70
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055311"
---
# <a name="attaching-and-detaching-to-a-program"></a>プログラムへのアタッチとデタッチ
デバッガーをアタッチするには、適切な属性を使用してメソッドとイベントの正しいシーケンスを送信する必要があります。

## <a name="sequence-of-methods-and-events"></a>メソッドとイベントのシーケンス

1. セッション デバッグ マネージャー (SDM) で、[OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドを呼び出します。

    デバッグ エンジン (DE) のプロセス モデルに基づいて、`IDebugProgramNodeAttach2::OnAttach` メソッドから次のいずれかのメソッドが返され、次に実行する処理が決まります。

    `S_FALSE` が返された場合、デバッグ エンジンはプログラムに正常にアタッチされています。 それ以外の場合は、アタッチ プロセスを完了させるために [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドが呼び出されます。

    `S_OK` が返された場合、DE は SDM と同じプロセスに読み込まれます。 SDM で次のタスクを実行します。

   1. [GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md) を呼び出して、DE のエンジン情報を取得します。

   2. DE を共同作成します。

   3. [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) を呼び出します。

2. DE が、`EVENT_SYNC` 属性を使用して SDM に [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) を送信します。

3. DE が、`EVENT_SYNC` 属性を使用して SDM に [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) を送信します。

4. DE が、`EVENT_SYNC_STOP` 属性を使用して SDM に [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) を送信します。

   プログラムからのデタッチは、次のように簡単な 2 段階のプロセスです。

5. SDM で、[Detach](../../extensibility/debugger/reference/idebugprogram2-detach.md) を呼び出します。

6. DE で、[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) を送信します。

## <a name="see-also"></a>関連項目
- [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
