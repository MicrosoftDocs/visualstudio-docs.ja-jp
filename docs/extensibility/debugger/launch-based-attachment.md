---
title: 起動ベースのアタッチ |Microsoft Docs
description: プログラムへの起動ベースのアタッチについて説明します。自動で、手動アタッチのようなパスに従います。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, launching
- debug engines, attaching to programs
ms.assetid: 362f00ac-1909-4a3a-bacb-c0ceb5549816
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fe698d8d1b29f02ae3971fc95a66c4823f7252c7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059718"
---
# <a name="launch-based-attachment"></a>起動ベースのアタッチ
プログラムへの起動ベースのアタッチは自動的に実行されます。 プログラムをホストするプロセスが SDM によって起動されると、起動ベースのアタッチは、手動アタッチ方法と同様のパスに従います。 詳細については、[プログラムへのアタッチ](../../extensibility/debugger/attaching-to-the-program.md)に関するページを参照してください。

## <a name="the-attaching-process"></a>アタッチ プロセス
 主な違いは、次のように、**Attach** 呼び出しの後のイベントのシーケンスです。

1. **IDebugEngineCreateEvent2** イベント オブジェクトを SDM に送信します。 詳細については、「[イベントの送信](../../extensibility/debugger/sending-events.md)」を参照してください。

2. **Attach** メソッドに渡された **IDebugProgram2** インターフェイスで `IDebugProgram2::GetProgramId` メソッドを呼び出します。

3. **IDebugProgramCreateEvent2** イベント オブジェクトを送信して、DE に対してプログラムを表すローカルの **IDebugProgram2** オブジェクトが作成されたことを SDM に通知します。

4. [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) イベント オブジェクトを送信して、起動したプロセスに対して新しいスレッドが作成されたことを SDM に通知します。

## <a name="see-also"></a>関連項目
- [必要なイベントを送信する](../../extensibility/debugger/sending-the-required-events.md)
- [デバッグされるプログラムの有効化](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
